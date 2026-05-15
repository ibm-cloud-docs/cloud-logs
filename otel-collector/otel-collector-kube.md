---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Deploying the OTel collector in an orchestrated environment by using a Helm chart
{: #otel-collector-kube}

You can use a Helm chart to deploy the OTel collector in a Kubernetes or OpenShift cluster.
{: shortdesc}

Complete the following steps to deploy the OTel collector:

## Prereqs
{: #otel-collector-kube-prereqs}

Learn about the OTel collector. For more information, see [About the OTel collector](/docs-draft/cloud-logs?topic=cloud-logs-otel-collector).

Review the requirements to deploy the collector. For more information, see [Requirements to deploy the collector](/docs-draft/cloud-logs?topic=cloud-logs-otel-collector&interface=ui#otel-collector-requirements-orchestrated).

Make sure you have access to the {{site.data.keyword.logs_full_notm}} instance where you plan to deploy the collector and send the metrics. You will need the region where the {{site.data.keyword.logs_full_notm}} instance is deployed and the service instance ID.

[{{site.data.keyword.containershort}}]{: tag-iks} Complete the following tasks before you deploy the OTel collector in a Kubernetes cluster:
- Make sure you have access to a Kubernetes cluster with permissions to create namespaces and deploy the OTel collector.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to metrics OTel collector in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Kubernetes CLI to manage the cluster by using `kubectl` commands. [Learn more](/docs/containers?topic=containers-cli-install).

[{{site.data.keyword.openshiftshort}}]{: tag-roks} Complete the following tasks before you deploy the OTel collector in an OpenShift cluster:
- Make sure you have access to an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster with permissions to create namespaces and deploy the OTel collector.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Openshift CLI to manage the cluster from the command line. [Learn more](/docs/openshift?topic=openshift-cli-install).


## Step 1. Define the authentication method
{: #otel-collector-kube-step1}

Choose the type of identity and the authentication method for the OTel collector. Then, create a trusted profile or an API key. The role that is required for sending logs to {{site.data.keyword.logs_full_notm}} is `Sender`.

You can use a service ID or a trusted profile as the identity that is used by the OTel collector to authenticate with the {{site.data.keyword.logs_full}} service. For more information, see [Granting IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).


Choose one of the following options:

### Option 1: Authentication using a trusted profile
{: #otel-collector-kube-step1-1}

Create a Trusted Profile. For more information, see [Generating a Trusted Profile for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-trusted-profile).

### Option 2: Authentication using a service ID API key
{: #otel-collector-kube-step1-2}

Generate an API Key for service ID authentication. For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).


## Step 2. Login to the cluster
{: #otel-collector-kube-step2}

[{{site.data.keyword.containershort}}]{: tag-iks} Log into your Kubernetes cluster. For more information, see [Accessing clusters](/docs/containers?topic=containers-access_cluster).

[{{site.data.keyword.openshiftshort}}]{: tag-roks} Log into your OpenShift cluster. For more information, see [Accessing Red Hat OpenShift clusters](/docs/openshift?topic=openshift-access_cluster).


## Step 3. Create the namespace
{: #otel-collector-kube-step3}

Create the `ibm-observe` namespace in your cluster.

[{{site.data.keyword.containershort}}]{: tag-iks} Run the following command:
```text
kubectl create namespace ibm-observe
```
{: codeblock}

[{{site.data.keyword.openshiftshort}}]{: tag-roks} Run the following command:
```text
oc new-project ibm-observe
```
{: codeblock}

## Step 4. Create the secret
{: #otel-collector-kube-step4}

[{{site.data.keyword.containershort}}]{: tag-iks} Run the following command to add the API key as a secret in the cluster:

```text
kubectl create secret generic ibmcloud-api-key \
  --from-literal=api-key=<your-api-key> \
  --namespace ibm-observe
```
{: codeblock}

[{{site.data.keyword.openshiftshort}}]{: tag-roks} Run the following command to add the API key as a secret in the cluster:

```text
oc create secret generic ibmcloud-api-key \
  --from-literal=api-key=<your-api-key> \
  --namespace ibm-observe
```
{: codeblock}

## Step 5. Customize the Helm chart
{: #otel-collector-kube-step5}

You can customize the Helm chart by modifying the `values.yaml` file.

Complete the following steps:
1. Download the Helm chart. For more information, see [Downloading the Helm chart](/docs-draft/cloud-logs?topic=cloud-logs-helm-chart-otel-download).
2. Open the `values.yaml` file.
3.

## Step 6. Install the Helm chart
{: #otel-collector-kube-step6}

If you are using the `iamMode` as `IAMAPIKey` then the apikey needs to be present in a Kubernetes secret named `icl-otel-collector` with the key name `IAM_API_KEY`.  The secret can be created using the Helm chart by including the `--set secret.iamAPIKey=<your iamAPIKey>` option when running the helm install.  If the secret has been created manually or if you are using `iamMode=TrustedProfile` then do not include this option.
{: important}

Complete the following steps when you use an API key as the authentication method:

[{{site.data.keyword.containershort}}]{: tag-iks} Complete the following steps to deploy the OTel collector for a Kubernetes cluster in the `ibnm-observe` namespace:

```sh
helm install ibm-otel-collector oci://<CHART_PATH> \
  --set openshift.enabled=false \
  --set global.metricsEndpoint==<METRICS_ENDPOINT> \
  --namespace ibm-observe \
  --set global.clusterName=<CLUSTER_NAME> \
  --set global.region=<REGION> \
  --set global.serviceInstanceId=<INSTANCE_ID> \
  --set global.iamUrl=<IAM_URL> \
  --set auth.apiKeySecretRef.name=<API_KEY> \
  --version <VERSION> --wait
```
{: codeblock}

[{{site.data.keyword.openshiftshort}}]{: tag-roks} Complete the following steps to deploy the OTel collector for an OpenShift cluster in the `ibnm-observe` namespace:

```sh
helm install ibm-otel-collector oci://<CHART_PATH> \
  --set openshift.enabled=true \
  --set global.metricsEndpoint==<METRICS_ENDPOINT> \
  --namespace ibm-observe \
  --set global.clusterName=<CLUSTER_NAME> \
  --set global.region=<REGION> \
  --set global.serviceInstanceId=<INSTANCE_ID> \
  --set global.iamUrl=<IAM_URL> \
  --set auth.apiKeySecretRef.name=<API_KEY> \
  --version <VERSION> --wait
```
{: codeblock}

Where

- `METRICS_ENDPOINT`: Custom metrics endpoint. When this parameter is set, it overrides the region-based URL. The format of this parameter is the following:

    For private endpoints, use:

    ```text
    https://<InstanceID>.ingress.private.<REGION>.logs.cloud.ibm.com:<PORT>/v1/metrics
    ```
    {: codeblock}

    For public endpoints, use:

    ```text
    https://<InstanceID>.ingress.<REGION>.logs.cloud.ibm.com:3443/v1/metrics
    ```
    {: codeblock}

    `PORT`: Use 443 when using a VPE.  Use port 3443 when using a CSE.

- `CLUSTER_NAME`: Name of the cluster where the OTel collector is deployed.

- `REGION`: Region where the {{site.data.keyword.logs_full_notm}} instance is deployed.

- `INSTANCEID`: Instance GUID of the {{site.data.keyword.logs_full_notm}} instance where you plan to send metrics.

- `APIKEY`: API key that is includes the credentials to authorize the OTel collector to send metrics to the {{site.data.keyword.logs_full_notm}} instance.

- `IAM_URL`: Custom IAM URL. The default value is `https://iam.cloud.ibm.com`.

- `CHART_PATH`: Path to Helm chart. The default value is `./helm/otel-ibmcloud`.

    The helm chart URL is the following: `oci://icr.io/icl-charts/ibm-otel-collector-charts`

- `VERSION`: [Optional] Helm chart version. By default, uses `latest` if this parameter is not specified. For more information, see [Checking the available Helm chart versions](/docs-draft/cloud-logs?topic=cloud-logs-helm-chart-otel-versions).

- `--set openshift.enabled`: Set to true for OpenShift clusters. It enables the OpenShift security mode.


## Step 7. Verify the OTel collector is successfully deployed
{: #otel-collector-kube-step7}

When the collector is deployed, you can verify the deployment:

- Check the `ibm-observe` namespace is available.

    Run the following command to list the namespaces in the cluster and check that the `ibm-observe` is listed.

    ```sh
    kubectl get namespace
    ```
    {: codeblock}

-  Check the resources that are configured:

    ```sh
    kubectl get deployment --namespace ibm-observe
    ```
    {: codeblock}

- Check the deployment status:

    ```sh
    kubectl rollout status deployment --namespace ibm-observe --selector app.kubernetes.io/name=icl-otel-collector;
    ```
    {: codeblock}

- Check the pods that are deployed:

    ```sh
    kubectl get pods ibm-observe -o wide -l app.kubernetes.io/name=ibm-cloud-logs-shipper
    ```
    {: codeblock}

    ```text
    NAME                                         READY   STATUS    RESTARTS   AGE
    icl-shipper-agent-xxxxx                      1/1     Running   0          2m
    icl-shipper-agent-yyyyy                      1/1     Running   0          2m
    icl-shipper-collector-0                      1/1     Running   0          2m
    icl-shipper-collector-1                      1/1     Running   0          2m
    icl-shipper-target-allocator-zzzzz           1/1     Running   0          2m
    ```
    {: screen}

    The `READY` column shows `1/1` for all pods, with a `STATUS` of `Running`. Verify that an OTel collector pod is ready for each node in your cluster.

    To check how many workers are available in your cluster, you can run the following command:

    ```sh
    kubectl get nodes
    ```
    {: codeblock}

    ```text
    NAME           STATUS   ROLES           AGE   VERSION
    192.168.0.10   Ready    master,worker   8d    v1.20.0+558d959
    192.168.32.4   Ready    master,worker   8d    v1.20.0+558d959
    192.168.16.4   Ready    master,worker   8d    v1.20.0+558d959
    ```
    {: screen}

    The number of items in each of these two lists need to be the same, and you can match the IP addresses in the node names with the values in the `NODE` column of the pod listing.

    If your nodes are not named by their IP, you can append the `-o wide` option and compare the values in the `INTERNAL-IP` column instead.

- Check the logs by component type:

    To check the logs of the agent (deployed as a deamonSet), run the following command:

    ```sh
    kubectl logs -n ibm-observe -l app.kubernetes.io/component=agent --tail=50
    ```
    {: codeblock}

    To check the logs of the collector (deployed as a StatefulSet), run the following command:

    ```sh
    kubectl logs -n ibm-observe -l app.kubernetes.io/component=collector --tail=50
    ```
    {: codeblock}

    To check the logs of the target allocator, run the following command:

    ```sh
    kubectl logs -n <namespace> -l app.kubernetes.io/component=target-allocator --tail=50
    ```
    {: codeblock}


- To check the helm chart deployed, run `helm list -n ibm-observe`


If you encounter a problem, you can run the `Automated Diagnostics Script` to troubleshoot what is happening:

1. Get the troubleshooting script in the following URL: [OTel collector troublshooting script](https://github.com/observability-c/icl-otelcol-shipper/blob/main/scripts/troubleshoot.sh){: external}

2. Run the following command:

    ```sh
    ./scripts/troubleshoot.sh -n ibm-observe [-r RELEASE_NAME] [--full]
    ```
    {: codeblock}



## Step 8. Verify logs are being delivered to your target destination
{: #otel-collector-kube-step8}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Check that you can see metrics.
