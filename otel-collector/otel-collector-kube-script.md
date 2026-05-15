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

You can use a Helm chart to deploy the {{site.data.keyword.collector}} v1.6.x to collect and route infrastructure and application metrics collector from a Kubernetes cluster to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

Complete the following steps to deploy an collector on an Kubernetes cluster:

## Prereqs
{: #otel-collector-kube-script-prereqs}

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

Review the requirements to deploy the collector:

-Agent (DaemonSet):

    CPU: 200m request, 1000m limit

    Memory: 512Mi request, 1Gi limit

-Collector (StatefulSet):

    Minimum 2 replicas for high availability

    CPU: 500m request per replica

    Memory: 1Gi request per replica

-Persistent storage:

    10Gi per replica (for queue persistence)

-Target Allocator (Deployment):

    Minimum 2 replicas for high availability

    CPU: 100m request

    Memory: 256Mi request

Other prereqs:
- The latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases)

- Make sure you have access to the {{site.data.keyword.logs_full_notm}} instance where you plan to send the metrics. You will need the region where the {{site.data.keyword.logs_full_notm}} instance is deployed and the service instance ID.


## Step 1. Create the API key for authentication
{: #otel-collector-kube-script-step1}


You can use a service ID as the identity that is used by the collector to authenticate with the {{site.data.keyword.logs_full}} service.

- For more information, see [Granting IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).

- The role that is required for sending metrics to {{site.data.keyword.logs_full_notm}} is `Sender`.

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
