---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-16"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Updating the {{site.data.keyword.agent}} IAM APIKey by using a Helm chart
{: #agent-helm-credential-rotation}

You can use Helm to update the {{site.data.keyword.agent}} IAM APIKey that is deployed in the cluster. Updating the IAM APIKey might be required if you need to rotate the IAM APIKey or update the IAM APIKey for other reasons.
{: shortdesc}

Complete the following steps to update the agent version that is deployed in the cluster:

## Before you begin
{: #agent-helm-credential-rotation-prereqs}

Before you begin, complete the prerequisite tasks.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key. For more information, see [Getting started with the IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started).

    - The [Kubernetes CLI](/docs/containers?topic=containers-cli-install) to manage Kubernetes clusters by using `kubectl` commands.

    - The [Openshift CLI](/docs/openshift?topic=openshift-cli-install) to manage OpenShift clusters from the command line.
- Read about [the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about).
- Generate an API Key for service ID authentication. For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).



## Update the agent with a new API key
{: #aagent-helm-credential-rotation-step2}
{: step}

If the secret has been created manually or if you are using `iamMode=TrustedProfile` then do not refer to this document for updating the IAM APIKey.
{: important}

Complete the following steps to update the agent with new APIKey:

1. Log in to the cluster. For more information, see [Access your cluster](/docs/containers?topic=containers-access_cluster).

2. Log in to the Helm registry. Choose one of the following options:

    Option 1: Login to the Helm registry by running the `helm registry login` command:

    ```sh
    helm registry login -u iambearer -p $(ibmcloud iam oauth-tokens --output json | jq -r .iam_token | cut -d " " -f2) icr.io
    ```
    {: codeblock}

    [Windows]{: tag-windows} Windows PowerShell users should use this command instead:

    ```sh
    helm registry login -u iambearer -p ((ibmcloud iam oauth-tokens --output json | ConvertFrom-Json).iam_token -replace 'Bearer ', '') icr.io
    ```
    {: codeblock}

    For more information, see [Using Helm charts in Container Registry: Pulling charts from another registry or Helm repository](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_pull)

    Option 2:  Log in to the Helm registry in {{site.data.keyword.registryshort}} by running the `ibmcloud cr login` command.

    You can use the `[ibmcloud cr login](/docs/Registry?topic=Registry-containerregcli#bx_cr_login)` command before you perform a Helm dry run or install. For more information, see [Accessing {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_access).

    Run the following commands:

    ```sh
    ibmcloud cr region-set global
    ```
    {: codeblock}

    ```sh
    ibmcloud cr login [--client CLIENT]
    ```
    {: codeblock}

2. Update the agent.

    ```sh
    helm upgrade <install-name> oci://icr.io/ibm-observe/logs-agent-helm --version <chart-version> --values <PATH>/logs-values.yaml -n ibm-observe --create-namespace --set secret.iamAPIKey=<APIKey-value>
    ```
    {: codeblock}

    where:

    - `<install-name>` is the name of the Helm installation (`logging-agent`)
    - `<chart-version>` is the version of the helm chart. The Helm chart version should match the agent image version. For more information, see [Helm chart versions](/docs/cloud-logs?topic=cloud-logs-agent-helm-template-clusters).
    - `<PATH>` is the directory path where the `logs-values.yaml` file is located.
    - `<APIKey-value>` is the new IAM APIKey associated with the ServiceID.

    For example, you can run the following command from the directory where the `logs-values.yaml` file is available:

    ```sh
    helm upgrade logging-agent oci://icr.io/ibm-observe/logs-agent-helm --version 1.5.0 --values ./logs-values.yaml -n ibm-observe --set secret.iamAPIKey=<secret>
    ```
    {: screen}

    To see installed agent name and chart version you can run `helm list -n NAMESPACE`.
    {: tip}

3. Restart the agent pods.

    For Kubernetes clusters, run:

    ```sh
    kubectl -n ibm-observe rollout restart ds/logs-agent
    ```
    {: codeblock}

    For OpenShift clusters, run:

    ```sh
    oc -n ibm-observe rollout restart ds/logs-agent
    ```
    {: codeblock}


## Verify that logs are being delivered to your target destination
{: #aagent-helm-credential-rotation-step3}
{: step}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view. The {{site.data.keyword.agent}} tags log records with a kubernetes object that includes the cluster name.

    ```text
    kubernetes.cluster_name:<CLUSTER_NAME>
    ```
    {: codeblock}

    You can run the query `kubernetes.cluster_name:<YOUR_CLUSTER_NAME>` in your {{site.data.keyword.logs_full_notm}} instance to search for logs that are generated by your cluster.
