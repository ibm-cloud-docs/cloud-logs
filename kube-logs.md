---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-18"

keywords:

subcollection: cloud-logs

content-type: tutorial
services: containers, cloud-logs, logs-router
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}


# Send {{site.data.keyword.containerlong_notm}} log data to {{site.data.keyword.logs_full_notm}}
{: #kube2logs}
{: toc-content-type="tutorial"}
{: toc-services="containers, cloud-logs, logs-router"}
{: toc-completion-time="30m"}

In this tutorial, you set up {{site.data.keyword.containerlong}} to send logs directly to {{site.data.keyword.logs_full_notm}}. These logs help you troubleshoot issues and improve the health and performance of your Kubernetes clusters and apps.
{: shortdesc}

## Goals
{: #kube2logs_goals}

In this tutorial you will:

 - Deploy the [{{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about) in an existing {{site.data.keyword.containerlong_notm}} cluster.

 - Verify that log data is flowing to your [{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs) instance.

## Before you begin
{: #kube2logs_prereqs}

Before you begin, make sure you have the prerequisites.

 - Create an [{{site.data.keyword.containerlong}}](/docs/containers?topic=containers-getting-started), and provisioned an instance of [{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-getting-started).

 - Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

 - Install The Kubernetes command-line tool, [kubectl](https://kubernetes.io/docs/tasks/tools/){: external}.

 - Install the JSON CLI processor [(`jq`)](https://jqlang.org/download/){: external}.

 - Install the YAML CLI processor [(`yq`)](https://github.com/mikefarah/yq/){: external}.

 An alternative to installing the {{site.data.keyword.cloud_notm}} CLI, `kubectl`, `jq`, and `yq` would be to use the [{{site.data.keyword.cloud_notm}} Shell](http://cloud.ibm.com/shell){: external}
 {: tip}

## Connect to your cluster
{: #kube2logs_connect}
{: step}

Connect to your {{site.data.keyword.containerlong_notm}} cluster. Connecting to the cluster enables `kubectl` commands to be run on the cluster.

1. Log in to your {{site.data.keyword.cloud_notm}} account. Include the `--sso` option if you are using a federated ID.

   ```text
   ibmcloud login
   ```
   {: pre}

2. Install the [{{site.data.keyword.containerlong_notm}} CLI plug-in](/docs/containers?topic=containers-cli-install)

   ```text
   ibmcloud plugin install ks
   ```
   {: pre}

3. List the available clusters and make note of the cluster to be connected.

   ```text
   ibmcloud ks clusters
   ```
   {: pre}

4. Connect to your cluster. Replace `<cluster_name>` with the name of your cluster.

   ```text
   ibmcloud ks cluster config --cluster <cluster_name>
   ```
   {: pre}

5. Verify that you are connected to your cluster and can run `kubectl` commands by listing all pods that are running in all namespaces.

   ```sh
   kubectl get pods --all-namespaces
   ```
   {: pre}

## Creating your API key
{: #kube2logs_key}
{: step}

Before you provision the {{site.data.keyword.agent}} as a daemonset, you need an IAM API key and a logging ingestion endpoint. The {{site.data.keyword.cloud_notm}} CLI is used to obtain this information.

First, create a service ID and obtain an API key.

1. Create a [service ID](/docs/account?topic=account-serviceids&interface=ui) by running the following command.

   ```text
   ibmcloud iam service-id-create kubernetes-logs-agent --description "Service ID for sending logs from IKS"
   ```
   {: pre}

2. Grant the `Sender` role for {{site.data.keyword.logs_full_notm}} to the created service ID by running the following command.

   ```text
   ibmcloud iam service-policy-create kubernetes-logs-agent --service-name logs --roles Sender
   ```
   {: pre}

3. Create an IAM API key by running the following command. You can customize the key name (`kubernetes-logs-agent-apikey`) and description (`--d`) if needed.

 	 ```text
    ibmcloud iam service-api-key-create kubernetes-logs-agent-apikey kubernetes-logs-agent --description "API key for sending logs to the IBM Cloud Logs service"
   ```
   {: pre}

   The API key is returned in the output following `API Key`:

   ```text
   ID            ApiKey-xxxxxxxx-b815-46c7-bc9f-516115bc31c6
   Name          kubernetes-logs-agent-apikey
   Description   API key for sending logs to the IBM Cloud Logs service
   Created At    2024-09-18T17:17+0000
   API Key       <apikey is displayed here>
   Locked        false
   ```
   {: screen}

Note:

* Each time that you create an API key, a new IAM secret is generated.

* Make sure that you securely store the API key, since it contains sensitive information.

## Determining your logging endpoint
{: #kube2logs_endpoint}
{: step}

The second piece of information that is needed is the ingestion endpoint for your {{site.data.keyword.logs_full_notm}} instance. Use this command to retrieve the URL:

```text
ibmcloud resource service-instances --service-name logs --long --output JSON | jq '[.[] | {name: .name, id: .id, region: .region_id, ingestion_endpoint: .extensions.external_ingress}]'
```
{: pre}

The endpoint is similar to:

```text
ingestion_endpoint: 3a622101-7521-4002-bf91-8c26e17eedcf.ingress.eu-de.logs.cloud.ibm.com
```
{: screen}

## Creating the agent YAML file
{: #kube2logs_yaml}
{: step}

In this step, create the YAML file that is used to configure the agent daemonset.

1. Create a file named `logs-values.yaml` with the following content:

    This file contains the configurations that are specific to your deployment.{: note}

    ```yaml
    metadata:
      name: "logs-agent"
    image:
      version: "1.4.0"  # required

    clusterName: ""     # Enter the name of your cluster. This information is used to improve the metadata and help with your filtering.

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
      trustedProfileID: "Profile-yyyyyyyy-xxxx-xxxx-yyyy-zzzzzzzzzzzz" # required if iamMode is set to TrustedProfile
    ```
    {: codeblock}

2. Update the fields in the yaml file with values specific to your environment.



## Deploying the daemonset
{: #kube2logs_deploy}
{: step}

Using the API key, endpoint URL, and YAML file, deploy the agent to your cluster.

1. Log in to the Helm registry by running the `helm registry login` command:

    ```sh
    helm registry login -u iambearer -p $(ibmcloud iam oauth-tokens --output json | jq -r .iam_token | cut -d " " -f2) icr.io
    ```
    {: codeblock}

    [Windows]{: tag-windows} Windows PowerShell users should use this command instead:

    ```sh
    helm registry login -u iambearer -p ((ibmcloud iam oauth-tokens --output json | ConvertFrom-Json).iam_token -replace 'Bearer ', '') icr.io
    ```
    {: codeblock}

    For more information, see [Using Helm charts in Container Registry: Pulling charts from another registry or Helm repository](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_pull).

2. Deploy the agent.

    If you are using a service ID API key (`iamMode`=`IAMAPIKey`), run the following command:

    ```sh
    helm install <install-name> oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version> --values <PATH>/logs-values.yaml -n ibm-observe --create-namespace --set secret.iamAPIKey=<APIKey-value>
    ```
    {: codeblock}

    where:

    - `<install-name>` is the name of the Helm installation (`logging-agent`)
    - `<chart-version>` is the version of the helm chart. The Helm chart version should match the agent image version. For more information, see [Helm chart versions](/docs/cloud-logs?topic=cloud-logs-agent-helm-template-clusters).
    - `<PATH>` is the directory path where the `logs-values.yaml` file is located.
    - `<APIKey-value>` is the IAM apikey associated with the ServiceID [setup in Step 1](/docs/cloud-logs?topic=cloud-logs-kube2logs#kube2logs_key)

    You can also deploy the agent using a trusted profile. For more information, see [Deploying the Logging agent for Kubernetes clusters using a Helm chart](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy).
    {: tip}

## Verify that logs are being sent
{: #kube2logs_verify}
{: step}

To help ensure that your {{site.data.keyword.containerlong}} logs are successfully flowing to {{site.data.keyword.logs_full_notm}}, do the following steps:

1. Access the [{{site.data.keyword.logs_full_notm}} UI](/docs/cloud-logs?topic=cloud-logs-instance-launch) and click ![Livetail icon](/icons/livetail.svg "Livetail") **Livetail**.

2. Click `Start` to watch the logs as they arrive in real-time.

A continuous flow of log data from the `kube-system` application should be seen. These logs are coming from your cluster.
