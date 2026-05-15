---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Deploying the OTel collector in an orchestrated environment by using a Helm chart
{: #otel-collector-kube-script}

You can use a Helm chart to deploy the OTel collector in a Kubernetes or OpenShift cluster.
{: shortdesc}

Complete the following steps to deploy the OTel collector:

## Prereqs
{: #otel-collector-kube-script-prereqs}

Learn about the OTel collector. For more information, see [About the OTel collector](/docs-draft/cloud-logs?topic=cloud-logs-otel-collector).

Review the requirements to deploy the collector. For more information, see [Requirements to deploy the collector](/docs-draft/cloud-logs?topic=cloud-logs-otel-collector&interface=ui#otel-collector-requirements-orchestrated).

Make sure you have access to the {{site.data.keyword.logs_full_notm}} instance where you plan to deploy the collector and send the metrics. You will need the region where the {{site.data.keyword.logs_full_notm}} instance is deployed and the service instance ID.

[{{site.data.keyword.containershort}}]{: tag-iks} Complete the following tasks before you deploy the OTel collector in a Kubernetes cluster:
- Make sure you have access to a Kubernetes cluster with permissions to create namespaces and deploy the collector.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to metrics collector in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Kubernetes CLI to manage the cluster by using `kubectl` commands. [Learn more](/docs/containers?topic=containers-cli-install).

[{{site.data.keyword.openshiftshort}}]{: tag-roks} Complete the following tasks before you deploy the OTel collector in an OpenShift cluster:
- Make sure you have access to an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster with permissions to create namespaces and deploy the collector.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Openshift CLI to manage the cluster from the command line. [Learn more](/docs/openshift?topic=openshift-cli-install).




## Step 1. Define the authentication method
{: #otel-collector-kube-script-step1}

Choose the type of identity and the authentication method for the agent. Then, create a trusted profile or an API key. The role that is required for sending logs to {{site.data.keyword.logs_full_notm}} is `Sender`.

You can use a service ID or a trusted profile as the identity that is used by the agent to authenticate with the {{site.data.keyword.logs_full}} service. For more information, see [Granting IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).


Choose one of the following options:

### Option 1: Authentication using a trusted profile
{: #otel-collector-kube-script-step1-1}

Create a Trusted Profile. For more information, see [Generating a Trusted Profile for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-trusted-profile).

### Option 2: Authentication using a service ID API key
{: #otel-collector-kube-script-step1-2}

Generate an API Key for service ID authentication. For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).

## Step 2. Deploy the collector
{: #otel-collector-kube-script-step2}

Get the deployment script in the following URL: [icl-otelcol-shipper](https://github.com/observability-c/icl-otelcol-shipper/blob/main/scripts/install.sh){: external}
{: note}

To deploy the collector in an interactive mode, you can run the following command:

```sh
./install.sh
```
{: codeblock}

To deploy the collector in a non-interactive mode, you can run the following command:


[{{site.data.keyword.containershort}}]{: tag-iks} Complete the following steps to deploy the OTel collector for a Kubernetes cluster in the `ibnm-observe` namespace:

```sh
./scripts/install.sh \
    --metrics-endpoint "${METRICS_ENDPOINT}" \
    --cluster-name "${CLUSTER_NAME}" \
    --release-name "${RELEASE_NAME}" \
    --instance-id "${INSTANCE_ID}" \
    --api-key "${API_KEY}" \
    --iam-url "${IAM_URL}" \
    --chart-path "${CHART_PATH}" \
    --version "${VERSION}"
```
{: codeblock}


[{{site.data.keyword.openshiftshort}}]{: tag-roks} Complete the following steps to deploy the OTel collector for an OpenShift cluster in the `ibnm-observe` namespace:

```sh
./scripts/install.sh \
    --openshift \
    --metrics-endpoint "${METRICS_ENDPOINT}" \
    --cluster-name "${CLUSTER_NAME}" \
    --release-name "${RELEASE_NAME}" \
    --instance-id "${INSTANCE_ID}" \
    --api-key "${API_KEY}" \
    --iam-url "${IAM_URL}" \
    --chart-path "${CHART_PATH}" \
    --version "${VERSION}"
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

- `RELEASE_NAME`: Helm release name. The default value is `ibm-otel-collector`.

- `CLUSTER_NAME`: Name of the cluster where the OTel collector is deployed.

- `REGION`: Region where the {{site.data.keyword.logs_full_notm}} instance is deployed.

- `INSTANCEID`: Instance GUID of the {{site.data.keyword.logs_full_notm}} instance where you plan to send metrics.

- `APIKEY`: API key that is includes the credentials to authorize the OTel collector to send metrics to the {{site.data.keyword.logs_full_notm}} instance.

- `IAM_URL`: Custom IAM URL. The default value is `https://iam.cloud.ibm.com`.

- `CHART_PATH`: Path to Helm chart. The default value is `./helm/otel-ibmcloud`.

    The helm chart URL is the following: `oci://icr.io/icl-charts/ibm-otel-collector-charts`

- `VERSION`: [Optional] Helm chart version. By default, uses `latest` if this parameter is not specified. For more information, see [Checking the available Helm chart versions](/docs-draft/cloud-logs?topic=cloud-logs-helm-chart-otel-versions).

- `--openshift`: Set for OpenShift clusters. It enables the OpenShift security mode.

For example, this is a sample output when you run the script in interactive mode:

```text
╔═══════════════════════════════════════════════════════════════╗
║         IBM Cloud Logs Shipper - Quick Start Installer        ║
╚═══════════════════════════════════════════════════════════════╝

[INFO] Checking prerequisites...
[OK] Prerequisites satisfied

This installer will help you deploy IBM Cloud Logs Shipper.
You'll need:
  - IBM Cloud region (e.g., us-south) OR a custom metrics endpoint
  - IBM Cloud Logs instance ID (from IBM Cloud console)
  - IBM Cloud API key

Use custom endpoints? [y/N]: y
Enter custom metrics endpoint (e.g., https://metrics.example.com): xxxxxxxx-xxxx-xxxx-xxxx-5802f6289e70.ingress.preprod.br-sao.logs.cloud.ibm.com
Enter custom IAM URL (press Enter for default https://iam.cloud.ibm.com): https://iam.cloud.ibm.com
Enter IBM Cloud region (optional for custom endpoint, press Enter to skip):
Enter IBM Cloud Logs instance ID: 2156cb53-e5e1-49eb-b811-5802f6289e70
Enter IBM Cloud API key:
Enter cluster name (optional, press Enter to skip): mycluster

[INFO] Configuration summary:
  Instance ID:      xxxxxxxx-xxxx-xxxx-xxxx-5802f6289e70
  Namespace:        ibm-observe
  Release:          ibm-otel-collector
  Cluster:          mycluster
  IAM URL:          https://iam.cloud.ibm.com
  Metrics Endpoint: xxxxxxxx-xxxx-xxxx-xxxx-5802f6289e70.ingress.preprod.br-sao.logs.cloud.ibm.com

Proceed with installation? [Y/n] y
[INFO] Creating namespace ibm-observe...

[WARN] Namespace ibm-observe already exists
[INFO] Creating API key secret...
secret/ibmcloud-api-key created
[OK] Secret ibmcloud-api-key created
[INFO] Installing Helm chart...
Error: INSTALLATION FAILED: path "./helm/otel-ibmcloud" not found
```
{: codeblock}

## Step 3. Verify the OTel collector is successfully deployed
{: #otel-collector-kube-script-step3}

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




## Step 4. Verify logs are being delivered to your target destination
{: #otel-collector-kube-script-step4}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Check that you can see metrics.
