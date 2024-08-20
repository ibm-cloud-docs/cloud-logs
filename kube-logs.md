---

copyright:
  years: 2014, 2024
lastupdated: "2024-07-31"


keywords: kubernetes,cloud-logs,logs

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}





# Send Kubernetes Service log data to IBM Cloud Logs
{: #health}

Set up logging in {{site.data.keyword.containerlong_notm}} to help you troubleshoot issues and improve the health and performance of your Kubernetes clusters and apps.
{: shortdesc}

## Objective
 - Deploy the [IBM Cloud Logs Routing agent](/docs/logs-router?topic=logs-router-agent-about) in an existing {{site.data.keyword.containerlong_notm}} cluster

 - Verify that log data is flowing to your {{site.data.keyword.logs_full_notm}}(/cloud-logs?topic=cloud-logs-getting-started)

## Prerequisites

 - You should have created a {{site.data.keyword.containerlong}}, and provisioned an instance of {{site.data.keyword.logs_full_notm}}(/cloud-logs?topic=cloud-logs-getting-started).

 - Install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

 - IBM Cloud [Kubernetes Service CLI plugin](/docs/containers?topic=containers-cli-install)

 - The Kubernetes command-line tool, [kubectl](https://kubernetes.io/docs/tasks/tools/){: external}.

 - [jq](https://jqlang.github.io/jq/download/){: external} JSON CLI processor.

 - [yq](https://github.com/mikefarah/yq/){: external} YAML CLI Processor.
 
## Step 1 - Connect to your cluster
1. To get started, log in to your IBM Cloud account. Include the --sso option if using a federated ID.
```$ ibmcloud login ```
2. Install the IBM Cloud [Kubernetes Service CLI plugin](/docs/containers?topic=containers-cli-install)
```$ ibmcloud plugin install ks ```
3. List all available clusters to identify the one you want to connect to. Note the cluster name.
``` $ ibmcloud ks clusters ```
4. Connect to your cluster with the following command, replacing <cluster_name> with the name of your cluster.
```$ ibmcloud ks cluster config --cluster <cluster_name>```
This will enable kubectl commands to be executed against your cluster. 
5. To verify that you are connected to your cluster and can execute kubectl commands, list all pods running in all namespaces: ``` $ kubectl get pods --all-namespaces ```

## Step 2 - API Key and logging endpoint

Before provisioning the log agent as a daemon set, we willl need to gather an IAM API key and a logging ingestion endpoint. Again, we will use the CLI to perform these actions.

1. **Create an IAM API Key**

	To create your IAM API key run the following command. You can customize customize the key NAME `(kubernetes-cloud-logs-key)`, --d `(description)`, and --file `(file name)` parameters if desired.

	```
	$ ibmcloud iam api-key-create kubernetes-cloud-logs-key --d 'API key for sending Kubernetes cluster log data to Cloud Logs' --file kubernetes-cloud-logs-key
	```

	We will now extract from the file the API key 
	```
	$ jq .apikey kubernetes-cloud-logs-key
	```
	The output should look something like
	```
	EaTtox-pcYzKo5Xa859DobiRmoChgEI5Q2wIpXA8cjtZ
	```
	**Important notes**

	* Each time you create an API key, a new IAM secret is generated.

	* Ensure you store the API key file securely, as it contains sensitive information.

2. **Logging ingestion endpoint**

The second piece of information needed is the ingestion endpoint for your IBM Cloud Logs instance. Use this command to retrieve the URL
```
$ ibmcloud resource service-instances --service-name logs --long --output JSON | jq '[.[] | {name: .name, id: .id, region: .region_id, ingestion_endpoint: .extensions.external_ingress}]'
```
It will look something like:
```
ingestion_endpoint: 3a622101-7521-4002-bf91-8c26e17eedcf.ingress.eu-de.logs.cloud.ibm.com
```

## Step 3 – Agent YAML

In this step, we willl download and modify the YAML file that configures the agent daemonset.

Download the agent configuration

Run the following command to download the agent configuration file:
```
$ curl -sSL https://ibm.biz/iclr-agent-iks-yaml -o logger-agent-iks.yaml
```

Modify the configuration

Information on configuring this file `(logger-agent-iks.yaml)` can be found in the documentation. For this tutorial, we will adjust the configuration to send all container logs, which is a safe default. The YAML file includes multiple sections, and we need to modify the ConfigMap section containing the agent configuration.

Open `logger-agent-iks.yaml` and search for `input-kubernetes.conf` to locate the relevant section. The section we want to modify will look like:

```
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
Change the Path value to include all log files under /var/log/containers/:
```
Path              /var/log/containers/*.log
```
That's it, you've now modified the YAML file to capture all container logs.

##Step 4 - Deploy the daemonset

Deploying the daemonset. In this section we will use the API key, endpoint URL and modified YAML file to deploy the agent to our cluster.

**Agent version**

We will make one more check before we proceed, and [determine the latest version of the agent](/docs/logs-router?topic=logs-router-check-agent-versions&interface=cli) in the IBM Container Registry

Install the IBM Cloud Kubernetes Service CLI plugin
```
$ ibmcloud plugin install cr  
```

Set the region to global 
```
$ ibmcloud cr region-set global
```
List versions of the agent available, pick the highest number as the most current.
```
$ ibmcloud cr images --restrict ibm/observe/logger-agent-plugin
```
These two commands will first set the region, then list all versions of the agent available. Pick the highest number as the most current.

The output will look something like we can clearly see that 1.2.3 is the most recent version.
```
Repository                               Tag     Digest         Namespace   Created        Size     Security status
icr.io/ibm/observe/logger-agent-plugin   1.1.1   80b538cf5a90   ibm         2 months ago   106 MB   -
icr.io/ibm/observe/logger-agent-plugin   1.2.0   886882f03ed0   ibm         1 month ago    91 MB    -
icr.io/ibm/observe/logger-agent-plugin   1.2.2   0e4a7fbbf01c   ibm         1 month ago    97 MB    -
icr.io/ibm/observe/logger-agent-plugin   1.2.3   92163c1328aa   ibm         2 weeks ago    97 MB    -
```

**Deployment command**

We can now deploy the agent using a single command. Review carefully, as it contains unique values we've gathered previously. Be sure to make the necessary substitutions for it to work as expected.

```
$ curl -sSL https://ibm.biz/logs-router-setup | bash -s -- \
-v 1.2.3  \
-m IAMAPIKey  \
-k <iam_api_key>  \
-t Kubernetes \
-r eu-de  \
--send-directly-to-icl  \
-h 3a622101-7521-4002-bf91-8c26e17eedcf.ingress.eu-de.logs.cloud.ibm.com
-p 443  \
-d <directory>\
```

| Parameter  |  Description |
| ------------ | ------------ |
|  curl -sSL https://ibm.biz/logs-router-setup | This is pulling down the logs-router-setup script.  You may want to examine this file to better understand the details of what is happening. At a high level, it is taking the set of parameters we are providing in the latter parts of this long command, and modifying the YAML file contents to be specific to our secret and URL.  |
|  **-v** 1.2.3 | Specifies the agent version.  |
| **-m** IAMAPIKey | Indicates that we intend to use an API key for authentication.  |
| **-k** Y12LmdUzByzsapbZGOEMUOerj1YlbGp0rod12xyDp2WM | Specifies the secret IAM API key.  |
| **-t** Kubernetes | Specifies the secret IAM API key.  |
| --send-directly-to-icl  | Indicates that we will bypass IBM Cloud Logs Routing and go directly to the IBM Cloud Logs instance.  |
| **-r** eu-de  | The region where the IBM Cloud Logs Routing Ingester endpoint is located.  |
| **-p**  443  | Sets the target port for log ingestion.  |
| **-h** 3a622101-7521-4002-bf91-8c26e17eedcf.ingress.eu-de.logs.cloud.ibm.com  | Cloud Logs ingress endpoint determined in prior steps.  |
| **-d** config\  |  The directory where the logger-agent-iks.yaml file is stored.  |

## Step 5 – Validate logs

To ensure your Kubernetes Service logs are successfully flowing to IBM Cloud Logs, follow these steps:

 - Access IBM Cloud Logs Web UI and navigate to the “Live Tail” view 

- Click the ‘Start’ button to begin watching logs as they arrive in real-time.

- You should see a continuous flow of log data from the “kube-system” application. These logs are coming from your cluster.

