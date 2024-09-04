---

copyright:
  years:  2024
lastupdated: "2024-09-04"

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

In this tutorial, you set up {{site.data.keyword.containerlong}} to send logs directly to {{site.data.keyword.logs_full_notm}} bypassing {{site.data.keyword.logs_routing_full_notm}} processing. These logs help you troubleshoot issues and improve the health and performance of your Kubernetes clusters and apps.
{: shortdesc}

## Goals
{: #kube2logs_goals}

In this tutorial you will:

 - Deploy the [{{site.data.keyword.logs_routing_full_notm}} agent](/docs/logs-router?topic=logs-router-agent-about) in an existing {{site.data.keyword.containerlong_notm}} cluster.

 - Verify that log data is flowing to your [{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs) instance.

## Before you begin
{: #kube2logs_prereqs}

Before you begin, make sure you have the prerequisites.

 - Create an [{{site.data.keyword.containerlong}}](/docs/containers?topic=containers-getting-started), and provisioned an instance of [{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-getting-started).

 - Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

 - Install The Kubernetes command-line tool, [kubectl](https://kubernetes.io/docs/tasks/tools/){: external}.

 - Install the JSON CLI processor [(`jq`)](https://jqlang.github.io/jq/download/){: external}.

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

Before you provision the {{site.data.keyword.logs_routing_full_notm}} agent as a daemonset, you need an IAM API key and a logging ingestion endpoint. The {{site.data.keyword.cloud_notm}} CLI is used to obtain this information.

First, obtain your IAM API key.

1. Create an IAM API key by running the following command. You can customize the key name (`kubernetes-cloud-logs-key`), description (`--d`), and file name (`--file`) parameters if needed.

 	  ```text
	  ibmcloud iam api-key-create kubernetes-cloud-logs-key --d 'API key for sending  Kubernetes cluster log data to Cloud Logs' --file kubernetes-cloud-logs-key
	  ```
    {: pre}

2. Extract the API key from the file.

 	  ```sh
	  jq .apikey kubernetes-cloud-logs-key
	  ```
    {: pre}

	  The output is similar to:

	  ```text
	  EaTtox-pcYzKo5Xa859DobiRmoChgEI5Q2wIpXA8cjtZ
	  ```
    {: screen}

    Protect the [API key](/docs/account?topic=account-manapikey&interface=ui). Anyone who can access the API key can impersonate your user.
    {: attention}

Note:

* Each time that you create an API key, a new IAM secret is generated.

* Make sure that you securely store the API key file, since it contains sensitive information.

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

In this step, download and modify the YAML file that is used to configure the agent daemonset.

1. Run the following command to download the agent configuration file:

   ```sh
   curl -sSL https://ibm.biz/iclr-agent-iks-yaml -o logger-agent-iks.yaml
   ```
   {: pre}

2. Modify the configuration to meet your requirements.

   Information about configuring the `logger-agent-iks.yaml` file can be found in the [{{site.data.keyword.logs_routing_full_notm}} documentation](/docs/logs-router?topic=logs-router-agent-fluentbit). In this tutorial, you configure the system to send all container logs, which is a safe default. The YAML file includes multiple sections. You need to modify the `ConfigMap` section.

   Edit the `logger-agent-iks.yaml` file and search for `input-kubernetes.conf` to locate the relevant section. The section to modify looks like:

   ```yaml
     input-kubernetes.conf: |
       [INPUT]
           Name              tail
           Tag               kube.*
           Path              /var/log/containers/logger-agent-ds-*.log
           Path_Key          file
           Exclude_Path      /var/log/at/**
           DB                /var/log/fluent-bit/fluent-bit.DB
           Buffer_Chunk_Size 32KB
           Buffer_Max_Size   256KB
           Parser            cri
           Skip_Long_Lines   On
           Refresh_Interval  10
           storage.type      filesystem
           storage.pause_on_chunks_overlimit on
   ```
   {: codeblock}

   Change the `Path` value to include all log files under `/var/log/containers/`:

   ```yaml
   Path              /var/log/containers/*.log
   ```
   {: codeblock}

   With this modification, all container logs are captured.


## Deploying the daemonset
{: #kube2logs_deploy}
{: step}

Using the API key, endpoint URL, and modified YAML file, deploy the agent to your cluster.

1. [Determine the current version of the agent](/docs/logs-router?topic=logs-router-check-agent-versions&interface=cli) in the {{site.data.keyword.registrylong_notm}}.

   1. Install the {{site.data.keyword.registrylong_notm}} CLI plug-in.

      ```text
      ibmcloud plugin install cr  
      ```
      {: pre}

   2. Set the region to global.

      ```text
      ibmcloud cr region-set global
      ```
      {: pre}

   3. List the available agent versions. Select the highest number as the most current.

      ```text
      ibmcloud cr images --restrict ibm/observe/logger-agent-plugin
      ```
      {: pre}
      
This output indicates that 1.2.3 is the most current version:

```text
Repository                               Tag     Digest         Namespace   Created        Size     Security status
icr.io/ibm/observe/logger-agent-plugin   1.1.1   80b538cf5a90   ibm         2 months ago   106 MB   -
icr.io/ibm/observe/logger-agent-plugin   1.2.0   886882f03ed0   ibm         1 month ago    91 MB    -
icr.io/ibm/observe/logger-agent-plugin   1.2.2   0e4a7fbbf01c   ibm         1 month ago    97 MB    -
icr.io/ibm/observe/logger-agent-plugin   1.2.3   92163c1328aa   ibm         2 weeks ago    97 MB    -
```
{: screen}

2. Deploy the agent by running a single command.

   Review your command carefully, since it contains values that were gathered previously. Be sure to make the necessary substitutions for the command to work as expected.
   {: important}

   ```sh
   curl -sSL https://ibm.biz/logs-router-setup | bash -s -- \
   -v 1.2.3  \
   -m IAMAPIKey  \
   -k <iam_api_key>  \
   -t Kubernetes \
   -r eu-de  \
   --send-directly-to-icl  \
   -h <ingestion_endpoint>
   -p 443  \
   -d <directory>\
   ```
   {: pre}

| Parameter  |  Description |
| ------------ | ------------ |
|  `-sSL https://ibm.biz/logs-router-setup` |  Gets the `logs-router-setup` script. You might want to review this file to better understand the details of what is processed. At a high level, the script uses the set of parameters that are provided along with the YAML file, API key, and URL. |
|  `-v 1.2.3` | Specifies the agent version as `1.2.3`.  |
| `-m IAMAPIKey` | Indicates that we intend to use an API key for authentication.  |
| `-k <iam_api_key>` | Specifies the IAM API key that we obtained. Replace `<iam_api_key>` with the value.  |
| `-t Kubernetes` | Specifies that the cluster type is an {{site.data.keyword.containerlong}} cluster.  |
| `--send-directly-to-icl`  | Indicates that logs bypass {{site.data.keyword.logs_routing_full_notm}} and are sent directly to the {{site.data.keyword.logs_full_notm}} instance.  |
| `-r eu-de`  | Specifies that the `eu-de` (Frankfurt) region is where the {{site.data.keyword.logs_routing_full_notm}} ingestion endpoint is located.  |
| `-p  443`  | Sets the target port (443) for log ingestion.  |
| `-h <ingestion_endpoint>`  | Specifies the {{site.data.keyword.logs_routing_full_notm}} ingress endpoint that was determined in previous steps.  |
| `-d <directory>`  |  Specifies the directory where the `logger-agent-iks.yaml` file is stored.  |
{: caption="Deployment parameters" caption-side="bottom"}



## Verify that logs are being sent
{: #kube2logs_verify}
{: step}

To help ensure that your {{site.data.keyword.containerlong}} logs are successfully flowing to {{site.data.keyword.logs_full_notm}}, do the following steps:

1. Access the [{{site.data.keyword.logs_full_notm}} UI](/docs/cloud-logs?topic=cloud-logs-instance-launch) and click ![Livetail icon](/icons/livetail.svg "Livetail") **Livetail**.

2. Click `Start` to watch the logs as they arrive in real-time.

A continuous flow of log data from the `kube-system` application should be seen. These logs are coming from your cluster.

