---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-23"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}


# Reviewing service, API server, and worker node logs
{: #kubernetes-audit-logs-worker-node-logs}

With audit logs, you're able to understand better what operations are initiated by users in your cluster, which can help you troubleshoot issues or report compliance to industry and internal standards.
{: shortdesc}


## Kubernetes API server audit logs
{: #kubernetes-audit-logs-API-server}

To monitor user-initiated, Kubernetes administrative activity made within your cluster, you can collect and forward audit events that are passed through your Kubernetes API server to {{site.data.keyword.logs_full}} or an external server.


## Considerations and prerequisites
{: #kubernetes-audit-logs-prereq}

Before you set up a Kubernetes API audit configuration, review the following information.

   * **VPC clusters versions 4.15 and later**: Audit logs use the Red Hat OpenShift audit policy profile `default` (for default) and `WriteRequestBodies`(for verbose). For more information, see the [Audit log policy](https://docs.redhat.com/en/documentation/openshift_container_platform/4.15/html/security_and_compliance/audit-log-policy-config).

   * **All other cluster versions**: Audit logs use the `openshift-audit` policy in the [kube-sample repo](https://github.com/IBM-Cloud/kube-samples/blob/master/kube-audit/openshift-audit-policy.yaml).
 
You can't modify the default policy or apply your own custom policy.
{: note}
 
   * For Kubernetes audit logs and verbosity, see the [Kubernetes documentation](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/). 

    * Only one audit webhook can be created in a cluster.

    * You must have the [Administrator IBM Cloud IAM platform access role](https://cloud.ibm.com/docs/openshift?topic=openshift-iam-platform-access-roles)for the Red Hat OpenShift on IBM Cloud cluster.

To get started, follow the instructions to send Kubernetes API audit logs [to a resource in the IBM Cloud private network](https://cloud.ibm.com/docs/openshift?topic=openshift-health-audit#audit-api-server-priv) to a resource in the IBM Cloud private network.


## Forwarding Kubernetes API audit logs to Cloud Logs
{: #kubernetes-audit-logs-API-audit-logs}

To forward audit logs to {{site.data.keyword.logs_full}}, you can create a Kubernetes audit system by using the provided image and deployment.

The following example uses the icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs image to forward logs to IBM Cloud Logs. If you only need a proof of concept, you may skip the secure setup step. For a more automated solution, configure and maintain your own log forwarding image.
{: important}

The Kubernetes audit system in your cluster consists of an audit webhook, a log collection service and web server app, and a logging agent. The webhook collects the Kubernetes API server events from your cluster master. The log collection service is a Kubernetes `ClusterIP` service that is created from an image from the public IBM Cloud registry. This service exposes a simple HTTP web server app that is exposed only on the cluster's network. The web server app parses the log data from the audit webhook and creates each log as a unique JSON line. Finally, the logging agent forwards the logs from the web server app to IBM Cloud Logs, where you can view the logs.

**Before you begin**: Ensure that you reviewed the [considerations and prerequisites](https://cloud.ibm.com/docs/openshift?topic=openshift-health-audit#prereqs-apiserver-logs) and that you have the [Administrator IBM Cloud IAM platform access role](https://cloud.ibm.com/docs/openshift?topic=openshift-iam-platform-access-roles) for {{site.data.keyword.logs_full}}.

1. Target the global container registry for public IBM Cloud images.

 ```sh
ibmcloud cr region-set global
```
{: codeblock}

2. Optional: For more information about the `kube-audit image`, inspect `icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs`.

```sh
ibmcloud cr image-inspect icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs
```
{: codeblock}

3. Set up your kubeconfig to access your cluster with

```sh
ibmcloud ks cluster config -c CLUSTER
```
{: codeblock}

4. Create a configuration file named `ibmcloud-kube-audit.yaml`. This configuration file creates a log collection service and a deployment that pulls the `icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs` image to create a log collection container.

```sh
apiVersion: v1
kind: List
metadata:
  name: ibmcloud-kube-audit
items:
  - apiVersion: v1
    kind: Namespace
    metadata:
      name: ibm-kube-audit
      labels:
        pod-security.kubernetes.io/enforce: restricted
        pod-security.kubernetes.io/enforce-version: latest
        pod-security.kubernetes.io/audit: restricted
        pod-security.kubernetes.io/audit-version: latest
        pod-security.kubernetes.io/warn: restricted
        pod-security.kubernetes.io/warn-version: latest
        security.openshift.io/scc.podSecurityLabelSync: "false"
  - apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: ibmcloud-kube-audit
      namespace: ibm-kube-audit
      labels:
        app: ibmcloud-kube-audit
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: ibmcloud-kube-audit
      template:
        metadata:
          labels:
            app: ibmcloud-kube-audit
        spec:
          containers:
            - name: ibmcloud-kube-audit
              image: 'icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs:latest'
              imagePullPolicy: Always
              ports:
                - containerPort: 3000
                - containerPort: 4443
              securityContext:
                allowPrivilegeEscalation: false
                runAsNonRoot: true
                capabilities:
                  drop:
                  - ALL
                seccompProfile:
                  type: RuntimeDefault
              volumeMounts:
                - mountPath: /certificates
                  name: certificates
                  readOnly: true
          volumes:
            - name: certificates
              secret:
                secretName: audit-webhook
                optional: true
  - apiVersion: v1
    kind: Service
    metadata:
      name: ibmcloud-kube-audit-service
      namespace: ibm-kube-audit
      labels:
        app: ibmcloud-kube-audit
    spec:
      selector:
        app: ibmcloud-kube-audit
      ports:
        - name: http
          protocol: TCP
          port: 80
          targetPort: 3000
        - name: https
          protocol: TCP
          port: 443
          targetPort: 4443
      type: ClusterIP
  - kind: NetworkPolicy
    apiVersion: networking.k8s.io/v1
    metadata:
      name: ibmcloud-kube-audit
      namespace: ibm-kube-audit
    spec:
      podSelector:
        matchLabels:
          app: ibmcloud-kube-audit
      policyTypes:
      - Ingress
      ingress:
      - ports:
        - protocol: TCP
          port: 3000
        - protocol: TCP
          port: 4443
        from:
        - namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: kube-system
          podSelector:
            matchLabels:
              app: konnectivity-agent
        - namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: kube-system
          podSelector:
            matchLabels:
              app: vpn
```
{: codeblock}

5. Create the deployment in the `ibm-kube-audit` namespace of your cluster.

```sh
kubectl apply -f ibmcloud-kube-audit.yaml
```
{: codeblock}

6. Wait for the `ibmcloud-kube-audit` deployment to reach Available.

```sh
kubectl wait --for condition=Available --namespace ibm-kube-audit --timeout 5m deploy/ibmcloud-kube-audit
```
{: codeblock}

Example output

deployment.apps/ibmcloud-kube-audit condition met

7. Verify that the `ibmcloud-kube-audit-service` service is deployed in your cluster.

```sh
kubectl get svc -n ibm-kube-audit -l app=ibmcloud-kube-audit
```
{: codeblock}

Example output

| NAME                 | TYPE   | ClUSTER IP   | EXTERNAL IP   | PORT (S)   | AGE         |
|--------------|------------|---------------- |---------------|-----------|----------------|
| ibmcloud-kube-audit-service | ClusterIP     | 172.21.xxx.xxx. |  <none>  | 80/TCP   | 1m   | 
{: caption="Example output" caption-side="bottom"}

8. [Encrypt traffic in transit with HTTPS](https://cloud.ibm.com/docs/openshift?topic=openshift-health-audit#secure-setup). If you only need a proof of concept audit log forwarder, skip this step.

9. Check the certificate authority status. If your certificates are nearing expiration, follow the steps to [rotate your certifications](https://cloud.ibm.com/docs/openshift?topic=openshift-cert-rotate).

```sh
ibmcloud oc cluster ca status -c CLUSTER
```
{: codeblock}

10. Save the `certificate-authority` of the cluster to file `cluster-ca.pem`.

```sh
ibmcloud oc cluster ca get -c CLUSTER --output json | jq -r .caCert | base64 -D > cluster-ca.pem
```
{: codeblock}

11. Log in to [your account. If applicable, target the appropriate resource group. Set the context](/docs/openshift?topic=openshift-health-audit#audit-api-server-priv) for your cluster. Prepare a certificate-based kubeconfig and save it to `kubeconfig.json`. Make sure to specify the `--admin` option to download the `client-certificate` and the `client-key` data to your local machine. This data is used later to configure the audit webhook.

```sh
ibmcloud oc cluster config --cluster CLUSTER --admin --output json > kubeconfig.json

```

If the owner of the kubeconfig is removed or its permissions are revoked, the kubernetes API server won't be able to send audit logs anymore. To prevent this scenario, we recommend using a service ID for this operation as that's directly coupled to the account and not to a specific user.
{: important}


12. Extract the kubeconfig's client certificate to file `kubeconfig-cert.pem.`

```sh
jq -r '.users[].user."client-certificate-data"' kubeconfig.json | base64 -D > kubeconfig-cert.pem

```

13. Extract the kubeconfig's client key to file `kubeconfig-key.pem.`

```sh
jq -r '.users[].user."client-key-data"' kubeconfig.json | base64 -D > kubeconfig-key.pem


```

14. Configure the audit webhook and specify the  `certificate-authority`,  `client-certificate`, and  `client-key`. The  `certificate-authority` was retrieved in step 10 and the  `client-certificate` and  `client-key` were retrieved in the previous two steps. Optionally configure the `policy` to a different value.


```sh
ibmcloud oc cluster master audit-webhook set \
    --cluster CLUSTER \
    --remote-server https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/http:ibmcloud-kube-audit-service:http/proxy/post \
    --ca-cert cluster-ca.pem \
    --client-cert kubeconfig-cert.pem \
    --client-key kubeconfig-key.pem \
    --policy default


```

If you configured HTTPS in step 8, set remote-server to this https URL instead:
{: note}

```sh

https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/https:ibmcloud-kube-audit-service:https/proxy/post

```

15. Verify that the audit webhook is created in your cluster.

```sh

ibmcloud oc cluster master audit-webhook get --cluster CLUSTER

```

Example output:

Server: https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/http:ibmcloud-kube-audit-service:
Policy: default 

16. Apply the webhook to your Kubernetes API server by refreshing the cluster master. It might take several minutes for the master to refresh.

```sh

ibmcloud oc cluster master refresh --cluster CLUSTER

```

17. While the master refreshes, [provision an instance of IBM Cloud Logs and deploy a logging agent to every worker node in your cluster](/docs/cloud-logs?topic=cloud-logs-kube2logs) provision an instance of {{site.data.keyword.logs_full}} and deploy a logging agent to every worker node in your cluster. The logging agent is required to forward logs from inside your cluster to the {{site.data.keyword.logs_full}} service. If you already set up logging agents in your cluster, you can skip this step.

18. View the cluster's state and wait for the `Master State` to indicate `updating`, then wait for state `deployed`. It might take several minutes to complete.

```sh

ibmcloud ks cluster get -c CLUSTER

```
Example output:

...
Master: 
Status: Refresh in progress. (2 seconds ago)
State: updating

...
Master
Status: Ready (2 seconds ago)
State: deployed 

19. After the master refresh completes and the logging agents are running on your worker nodes, you can [view your Kubernetes API audit logs in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-instance-launch). 

After you set up the audit webhook in your cluster, you can monitor version updates to the ibmcloud-kube-audit-to-ibm-cloud-logs image by running ibmcloud cr image-list --include-ibm | grep ibmcloud-kube-audit-to-ibm-cloud-logs. To see the version of the image that currently runs in your cluster, run oc get pods | grep ibmcloud-kube-audit-to-ibm-cloud-logs to find the audit pod name, and run kubectl describe pod <pod_name> to see the image version. Update the pod to the latest available on the current tag with kubectl rollout restart --namespace ibm-kube-audit deploy/ibmcloud-kube-audit and wait for the new pods to become available with kubectl rollout status --timeout 1m --namespace ibm-kube-audit deploy/ibmcloud-kube-audit.
{: tip}

## Manage updates, rotate certificates, and encrypt in transit with HTTPS
{: #kubernetes-audit-logs-manage-updates}

A few important things to note before preparing to forward logs:

1. The image tag `icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs:latest`  does receive vulnerability and bug fix updates. However, the deployment must be restarted manually to pick up those changes. Use `kubectl rollout restart -n ibm-kube-audit deploy/ibmcloud-kube-audit` to pull the latest image and gracefully restart.

2. This deployment is manually installed and managed. Switching from this deployment to another may result in audit log downtime.

3. The certificate generated in the following steps can be rotated. Rotation requires manual steps to replace the secret and restart the deployment.

To secure the deployment with encryption in transit, a private key and TLS certificate signed by the kube-apiserver are required.

1. After applying the YAML file in step 4, wait for the Service resource to populate the cluster IP. Save that to the shell variable `$cluster_ip`.


```json

    cluster_ip=$(
    kubectl wait         --for jsonpath='{.spec.clusterIP}'         --namespace ibm-kube-audit         --output jsonpath='{.spec.clusterIP}'         --timeout 5m         svc/ibmcloud-kube-audit-service
)

```

2. Generate a private key and save to server.key

```sh

openssl genrsa -out server.key 4096

```

3. Generate a Certificate Signing Request configuration file `server-csr.conf`. This is used to generate the certificate Kubernetes will sign.


```sh

cat <<EOF > server-csr.conf
[ req ]
default_bits = 2048
prompt = no
default_md = sha256
req_extensions = req_ext
distinguished_name = dn

[ dn ]
CN = system:node:ibmcloud-kube-audit-service.ibm-kube-audit.svc
O = system:nodes

[ req_ext ]
subjectAltName = @alt_names

[ alt_names ]
DNS.1 = ibmcloud-kube-audit-service.ibm-kube-audit.svc.cluster.local
DNS.2 = ibmcloud-kube-audit-service.ibm-kube-audit.svc
IP.1 = ${cluster_ip}
EOF
```
4. Generate the Certificate Signing Request payload for Kubernetes to sign.

```sh

openssl req -new -config server-csr.conf -key server.key -out server.csr

```

5. Insert the payload into a Kubernetes CertificateSigningRequest (CSR) resource

```sh

kubectl apply -f - <<EOF
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: ibmcloud-kube-audit-service.ibm-kube-audit
spec:
  request: $(base64 < server.csr | tr -d '\n')
  signerName: kubernetes.io/kubelet-serving
  usages:
  - digital signature
  - key encipherment
  - server auth
EOF

```

6. Approve the request

```sh

kubectl certificate approve ibmcloud-kube-audit-service.ibm-kube-audit

```

7. Wait for the certificate to be signed

```sh

kubectl wait     
--for jsonpath='{.status.certificate}'     --output go-template='{{.status.certificate | base64decode}}'     
--timeout 5m     
csr/ibmcloud-kube-audit-service.ibm-kube-audit > server.crt

```

8. Create a Secret from the certificate and private key

```sh

kkubectl create secret tls     
--cert server.crt     
--key server.key     
--namespace ibm-kube-audit     
audit-webhook

```

9. Restart the deployment to pick up the new secret.

```sh

kubectl rollout restart --namespace ibm-kube-audit deploy/ibmcloud-kube-audit

```

10. Wait for the new pods to become available


```sh

kubectl rollout status --timeout 1m --namespace ibm-kube-audit deploy/ibmcloud-kube-audit

```

11. The audit webhook is now ready to receive events over an encrypted connection. When configuring the audit webhook in the [Forwarding Kubernetes API audit logs to Cloud Logs](/docs/openshift?topic=openshift-health-audit#audit-api-server-la) section, you must use the `https` version of the `--remote-server` URL instead:

```sh

https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/https:ibmcloud-kube-audit-service:https/proxy/post`

```

## Forwarding Kubernetes API audit logs to a resource in the IBM Cloud private network
{: #kubernetes-audit-logs-resouce}

Forward audit logs to a resource other than IBM Cloud Logs that is outside of your cluster and accessible in the IBM Cloud private network.

The following example uses the haproxytech/haproxy-alpine:2.6 image to forward logs. This image is for demonstration purposes only and should not be used in production environments. For a production solution, configure and maintain your own log forwarding image.
{: important}

Before you begin, ensure that you reviewed the [considerations and prerequisites](/docs/openshift?topic=openshift-health-audit#prereqs-apiserver-logs).

1. Create a new directory `kube-audit-forwarder` and create a file `haproxy.cfg` in it with the following contents. Do not forget to replace `<REMOTE-IP>:<REMOTE-PORT>` in the file to the IP address and port of your remote log consumer.


```sh

global
  log stdout format raw local0 info
defaults
  mode http
  timeout client 10s
  timeout connect 5s
  timeout server 10s
  timeout http-request 10s
  log global
frontend myfrontend
  bind :3000
  default_backend remotelogstash
# Use remote log consumer IP and port here
backend remotelogstash
  server s1 <REMOTE-IP>:<REMOTE-PORT> check

```

If your log consumer server is enforcing secure connection (TLS), you can add your certificate files to this directory and change the backend section in haproxy.cfg to use these files. For more information, see the [HAProxy documentation](https://haproxy-ingress.github.io/docs/).
{: tip}

2. Create a configmap from the contents of `kube-audit-forwarder` directory.

```sh

kubectl create namespace ibm-kube-audit; kubectl create configmap -n ibm-kube-audit kube-audit-forwarder-cm --from-file=kube-audit-forwarder

```

3. Create a configuration file that is named `kube-audit-forwarder-remote-private-ip.yaml`. This configuration file creates a deployment and a service that forwards audit logs from the cluster to the IP address of the remote resource through the IBM Cloud private network.

```sh

kind: Deployment
apiVersion: apps/v1
metadata:
  labels:
    app: kube-audit-forwarder
  name: kube-audit-forwarder
  namespace: ibm-kube-audit
spec:
  revisionHistoryLimit: 2
  selector:
    matchLabels:
      app: kube-audit-forwarder
  strategy:
    rollingUpdate:
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: kube-audit-forwarder
    spec:
      containers:
      - image: haproxytech/haproxy-alpine:2.6
        imagePullPolicy: IfNotPresent
        name: haproxy
        volumeMounts:
        - name: config-volume
          mountPath: /usr/local/etc/haproxy/haproxy.cfg
          subPath: haproxy.cfg
      volumes:
      - name: config-volume
        configMap:
          name: kube-audit-forwarder-cm
---
apiVersion: v1
kind: Service
metadata:
  name: kube-audit-forwarder
  namespace: ibm-kube-audit
spec:
  selector:
    app: kube-audit-forwarder
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
---
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: kube-audit-forwarder
  namespace: ibm-kube-audit
spec:
  podSelector:
    matchLabels:
      app: kube-audit-forwarder
  policyTypes:
  - Ingress
  ingress:
  - ports:
    - protocol: TCP
      port: 3000
    from:
    - namespaceSelector:
        matchLabels:
          kubernetes.io/metadata.name: kube-system
      podSelector:
        matchLabels:
          k8s-app: konnectivity-agent
    - namespaceSelector:
        matchLabels:
          kubernetes.io/metadata.name: kube-system
      podSelector:
        matchLabels:
          app: konnectivity-agent
    - namespaceSelector:
        matchLabels:
          kubernetes.io/metadata.name: kube-system
      podSelector:
        matchLabels:
          app: vpn

```

If you added certificate files to the kube-audit-forwarder in the previous step, do not forget to list those files in volumeMounts section as a subPath.
{: tip}

4. Create the deployment and service.

```sh

kubectl create -f kube-audit-forwarder-remote-private-ip.yaml

```

5. Verify that the kube-audit-forwarder deployment and service is deployed in your cluster.

```sh

kubectl get svc -n ibm-kube-audit

```

Example output:

| NAME                 | TYPE   | ClUSTER IP   | EXTERNAL IP   | PORT (S)   | AGE         |
|--------------|------------|---------------- |---------------|-----------|----------------|
| kube-audit-forwarder | ClusterIP     | 10.xxx.xx.xxx |  <none>  | 80/TCP   | 1m   | 
{: caption="Example output" caption-side="bottom"}


```sh

kubectl get deployment -n ibm-kube-audit

```

Example output:

| NAME         | READY       | UP-TO_DATE   | AVAILABLE    | AGE        |
|--------------|------------|---------------|---------------|-----------|
| kube-audit-forwarder | 1/1     | 1       |         1       |    6m27s | 
{: caption="Example output" caption-side="bottom"}


6. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster](/docs/containers?topic=containers-access_cluster). Make sure to specify the  `--admin` option to download the `client-certificate` and the  `client-key`  files to your local machine. These files are used later to configure the audit webhook.

```sh

ibmcloud oc cluster config --cluster CLUSTER --admin

```

7. Check the certificate authority status. If your certificates are nearing expiration, follow the steps to [rotate your certifications](https://cloud.ibm.com/docs/openshift?topic=openshift-cert-rotate).

```sh

ibmcloud oc cluster ca status -c CLUSTER

```

8. Query the `certificate-authority` of the cluster and save it into a file.

```sh

ibmcloud oc cluster ca get -c CLUSTER --output json | jq -r .caCert | base64 -D > CERTIFICATE_AUTHORITY

```

9. View your current config by running the `oc config` view command and review the output for the `client-certificate` and `client-key`.

``sh

oc config view --minify

```

Example output

```sh

clusters:
- cluster:
    ...
    ...
    client-certificate: /Users/user/.bluemix/plugins/container-service/clusters/cluster-name-a111a11a11aa1aa11a11-admin/admin.pem
    client-key: /Users/user/.bluemix/plugins/container-service/clusters/cluster-name-a111a11a11aa1aa11a11-admin/admin-key.pem

```

10. Configure the audit webhook and specify the `certificate-authority`, `client-certificate`, and `client-key` that you retrieved in the steps 5-7.

```sh

ibmcloud oc cluster master audit-webhook set --cluster CLUSTER --remote-server https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/kube-audit-forwarder/proxy/post --ca-cert CERTIFICATE_AUTHORITY --client-cert CLIENT_CERTIFICATE --client-key CLIENT_KEY [--policy default|verbose]

```

11. Verify that the audit webhook is created in your cluster.

```sh

ibmcloud oc cluster master audit-webhook get --cluster CLUSTER_NAME_OR_ID

```

Example output:

OK
Server: https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/kube-audit-forwarder/proxy/post
Policy: default

12. Apply the webhook to your Kubernetes API server by refreshing the cluster master. The master might take several minutes to refresh.

```sh

ibmcloud oc cluster master refresh --cluster CLUSTER_NAME_OR_ID

```

After the master refresh completes, your logs are sent to the private IP address of your logging resource.

## Worker node audit logs
{: #kubernetes-audit-logs-worker-node}

Red Hat OpenShift on IBM Cloud uses the Linux Auditing System component, `auditd`, to monitor and log activity on the worker nodes. Although worker node auditing is enabled by default, no auditing data is available until you set up log forwarding to an {{site.data.keyword.logs_full}} instance or external server.

## Understanding the worker node audit configuration
{: #kubernetes-audit-logs-audit-configure}

The logs are stored in the `/var/log/audit` directory on the worker nodes. You can view the logs in {{site.data.keyword.logs_full}} or your external server after you set up log forwarding.

`Auditd collects logs on various events, including the following:

  * Linux system calls (`syscalls`)
  * SELinux denials
  * SELinux policy modifications
  * Software modifications through the `yum package installer
  * `Systemd` operations
  * Linux user and group modifications
  * `Netfilter` change modifications
  * SSH Logins


## Setting up log forwarding for worker nodes
{: #kubernetes-audit-logs-worder-codes}

See [Forwarding logs to an IBM Cloud Logs instance](/docs/containers?topic=containers-health).


## Service audit logs
{: #kubernetes-audit-logs-service-audit-logs}

By default, Red Hat OpenShift on IBM Cloud generates and sends events to {{site.data.keyword.logs_full}}. To see these events, you must create an {{site.data.keyword.logs_full}} instance. For more information, see [IBM Cloud Logs events](/docs/containers?topic=containers-health).


## Viewing AuditWebhookError alerts in auditing-enabled clusters
{: #kubernetes-audit-logs-auditing-clusters}

Red Hat OpenShift on IBM Cloud clusters version have an `AuditWebhookError` alert that fires when the audit webhook crashes or is deleted.

To view the alert:

[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)


1. From the Red Hat OpenShift on IBM Cloud, select the **Administrator** view.
2. Click **Observe** > **Alerting** > **AuditWebhookError**.
To create a notification for this alert, see [Sending notifications to external systems](https://docs.redhat.com/en/documentation/openshift_container_platform/4.10/html/monitoring/managing-alerts#sending-notifications-to-external-systems_managing-alerts) .
