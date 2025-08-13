---

copyright:
  years:  2024, 2025
lastupdated: "2025-08-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Updating the {{site.data.keyword.agent}} version by using a Helm chart
{: #agent-helm-update}

You can use Helm to update the {{site.data.keyword.agent}} version.
{: shortdesc}

If you deployed the logging agent by using a Helm chart, and later on made manual updates to the config map configuration, when you do the upgrade, manual updates are lost. Check that the logs-values.yaml file that contains the information for the upgrade includes the configuration for manual updates.

Complete the following steps to update the agent version that is deployed in the cluster:

## Before you begin
{: #agent-helm-update-prereqs}

- Make sure you have access to Kubernetes cluster with permissions to create namespaces and deploy the agent.

- Take a copy of the current config map for the logging agent. Run: `kubectl get cm logs-agent -n ibm-observe -o yaml > logging-agent-backup-cm.yaml`

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Kubernetes CLI to manage Kubernetes clusters by using `kubectl` commands. [Learn more](/docs/containers?topic=containers-cli-install).

    - The Openshift CLI to manage OpenShift clusters from the command line. [Learn more](/docs/openshift?topic=openshift-cli-install).

- Read about [the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about).

- Check the agent versions that are available. For more information, see [Checking the available agent versions](/docs/cloud-logs?topic=cloud-logs-check-agent-versions).  Note that the version of the Helm chart will match the version of the agent - for example, if you are using version 1.3.0 of the agent there's a Helm chart with version 1.3.0 that accompanies that version.


## Step 1. Update the Helm chart values file for the {{site.data.keyword.agent}}
{: #agent-helm-update-step1}

Complete the following steps to modify the Helm chart with the agent version that you plan to deploy:

1. Update the file named `logs-values.yaml` with the following content:

    This file contains the configurations that are specific to your deployment.{: note}

    ```yaml
    metadata:
      name: "logs-agent"
    image:
      version: "1.5.0"  # Modify the agent version and enter the version that you want to deploy

    clusterName: "ENTER_CLUSTER_NAME"     # Enter the name of your cluster. This information is used to improve the metadata and help with your filtering.

    # enableMultiline: true   # Set to true to enable multiline support for applications, like Java or Python, where errors and stack traces can span several lines, and each line is sent as a separate log entry.

    additionalMetadata: # add additional metadata, for example:
      region: au-syd
      env: production
      logs-agent-version: 1.5.0     # Enter the agent version that you want to deploy

    env:
      # ingestionHost is a required field. For example:
      # ingestionHost: "<logs instance>.ingress.us-east.logs.cloud.ibm.com"
      ingestionHost: "" # required

      # If you are using private CSE proxy, then use port number "3443"
      # If you are using private VPE Gateway, then use port number "443"
      # If you are using the public endpoint, then use port number "443"
      ingestionPort: "" # required

      iamMode: "TrustedProfile"
      # trustedProfileID - trusted profile id - required for iam trusted profile mode
      trustedProfileID: "" # required if iamMode is set to TrustedProfile

    ```
    {: codeblock}


## Step 2. Update the agent
{: #agent-helm-update-step2}

If you are using the `iamMode` as `IAMAPIKey` then the apikey needs to be present in a Kubernetes secret named `logs-agent` with the key name `IAM_API_KEY`.  The secret can be created using the Helm chart by including the `--set secret.iamAPIKey=<your iamAPIKey>` option when running the helm install.  If the secret has been created manually or if you are using `iamMode=TrustedProfile` then do not include this option.
{: important}

Complete the following steps:

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

    You can use the `ibmcloud cr login` command before you perform a Helm dry run or install. For more information, see [Accessing {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_access) and [ibmcloud cr login](/docs/Registry?topic=Registry-containerregcli#bx_cr_login).

    Run the following commands:

    ```sh
    ibmcloud cr region-set global
    ```
    {: codeblock}

    ```sh
    ibmcloud cr login [--client CLIENT]
    ```
    {: codeblock}

3. Update the agent.

   If you have installed a previous version of the {{site.data.keyword.agent}} and have updated the agent configuration by modifying the config map directly in the cluster, make a copy of your config map from the cluster before running the `helm upgrade` command. When the {{site.data.keyword.agent}} is updated, any changes made to the config map will be overwritten.
    {: attention}

    If you are using the `iamMode`=`TrustedProfile` then the complete command is:

    ```sh
    helm upgrade <install-name> oci://icr.io/ibm-observe/logs-agent-helm --version <chart-version> --values <PATH>/logs-values.yaml -n ibm-observe
    ```
    {: codeblock}

    If you are using the `iamMode`=`IAMAPIKey` then the complete command is:

    ```sh
    helm upgrade <install-name> oci://icr.io/ibm-observe/logs-agent-helm --version <chart-version> --values <PATH>/logs-values.yaml -n ibm-observe --create-namespace --set secret.iamAPIKey=<APIKey-value>
    ```
    {: codeblock}

    where:

    - `<install-name>` is the name of the Helm installation (`logs-agent`)
    - `<chart-version>` is the version of the helm chart. The Helm chart version should match the agent image version. For more information, see [Helm chart versions](/docs/cloud-logs?topic=cloud-logs-agent-helm-template-clusters).
    - `<PATH>` is the directory path where the `logs-values.yaml` file is located.
    - `<APIKey-value>` is the IAM apikey associated with the ServiceID.

    For example, you can run the following command from the directory where the `logs-values.yaml` file is available:

    ```sh
    helm upgrade logs-agent oci://icr.io/ibm-observe/logs-agent-helm --version 1.5.0 --values ./logs-values.yaml -n ibm-observe --set secret.iamAPIKey=<secret>
    ```
    {: screen}

    To see installed agent name and chart version you can run `helm list -n NAMESPACE`.
    {: tip}

4. Restart the agent pods.

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


## Step 3. Verify logs are being delivered to your target destination
{: #agent-helm-update-step3}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view. The {{site.data.keyword.agent}} tags log records with a kubernetes object that includes the cluster name.

    ```text
    kubernetes.cluster_name:<CLUSTER_NAME>
    ```
    {: codeblock}

    You can run the query `kubernetes.cluster_name:<YOUR_CLUSTER_NAME>` in your {{site.data.keyword.logs_full_notm}} instance to search for logs that are generated by your cluster.
