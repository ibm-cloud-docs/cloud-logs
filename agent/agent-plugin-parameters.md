---

copyright:
  years:  2024
lastupdated: "2024-11-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Output plug-in parameters to send data to an {{site.data.keyword.logs_full_notm}} instance
{: #agent-plugin-parameters}


List of parameters that you can use to configure the output plugin to send data to an {{site.data.keyword.logs_full_notm}} instance in the {{site.data.keyword.agent}}.
{: shortdesc}

## FluentBit parameters
{: #agent-plugin-parameters-fluentbit}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
| `Name`   |  Name of the plug-in. Must be set to `logger-icl-output-plugin` | n/a  |  `logger-icl-output-plugin` | true  |
| `Id`     |  Unique ID for the plug-in. |  n/a |  any string  | true  |
| `Match`  |  Use to specify how to match events. |  n/a |  any string  | true  |
| `Retry_Limit` |  Retry processing if the plug-in fails to send data to Cloud Logs.  \n Set `False` if you want to retry forever, otherwise set to an Integer value.  \n For more information about how to configure retries, see [here](https://docs.fluentbit.io/manual/administration/scheduling-and-retries#configuring-retries){: external} |  1 |  `False` or N >= 1  | true  |
| `Workers` | The number of concurrent worker threads sending to {{site.data.keyword.logs_full_notm}}.  \n In order to increase the throughput of logs sent to {{site.data.keyword.logs_full_notm}}, you can increase the number of concurrent threads sending from each agent.  \n See [here](#agent-worker-configuration-considerations)  | 1 | 1 or more | false |
{: caption="Fluentbit parameters" caption-side="bottom"}


## Connection parameters
{: #agent-plugin-parameters-connection-parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Target_Host` |  Ingest hostname to be used for connection |  n/a |  any url endpoint  | true  |
|  `Target_Port` |  Ingest Port to be used for connection |  `443` |  any port number  | false  |
|  `Target_Path` |  URL path to be used for connection |  `/logs/v1/singles` |  any string  | false  |
{: caption="Connection parameters" caption-side="bottom"}

## Logging parameters
{: #agent-plugin-parameters-logging-parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Logging_Level` |  Specify the log level to be used in the plug-in |  `info` |  `debug`  \n `info`  \n `error`  | false  |
|  `Package_Size` | Specify the package size in KB or MB | `2` | any number followed by a unit, for example, `2MB`, `10KB`. Must be less than `2MB` | false |
{: caption="Logging parameters" caption-side="bottom"}


## Authentication parameters
{: #agent-plugin-parameters-authentication-parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Authentication_Mode` |  Specify the authentication mode |  `TrustedProfile` | `TrustedProfile`  \n `IAMAPIKey`  | false  |
|  `IAM_Environment` |  Specify the IAM environment for authentication |  `Production` |  `Production` specifies the public endpoint `iam.cloud.ibm.com`  \n `PrivateProduction` specifies the private endpoint `private.iam.cloud.ibm.com` | false  |
|  `CR_Token_Mount_Path` |  Path where the CRToken is present |  `/var/run/secrets/tokens/vault-token` | any string  | false - Only used when Authentication_Mode is set to TrustedProfile  |
|  `Trusted_Profile_ID` |  ID of the Trusted Profile to be used |  n/a |  any string	  | true - Only used when Authentication_Mode is set to TrustedProfile |
{: caption="Authentication parameters" caption-side="bottom"}

When `Authentication_Mode` is set to `IAMAPIKey`, consider the following information:

- The API key must be specified in an environment variable called `IAM_API_KEY`.
- If no value is provided in the `IAM_API_KEY` variable, the plug-in initialization will fail.



## Fluentbit Agent Workers configuration considerations
{: #agent-workers-configuration-considerations}

A `worker`, in the context of the {{site.data.keyword.agent}}, represents a CPU thread that is available to the {{site.data.keyword.agent}} for handling logs.

You can configure the number of available workers that are available in the output plugin configuration.

- In the fluent-bit default configuration, `Workers=1` is the default configuration and this will work for workloads generating log volumes less than 1MB/sec.
- In an environment with greater logging volumes, more than 1 MB/sec, it might be necessary to increase the `Workers` configuration in order for the output plug-in to be able to process the logs being consumed.
- The Helm chart for [Openshift](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy) and [Kubernetes](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy) deployments are configured with 4 workers since this is generally a good setting for most Kubernetes workloads.

Use the `outputWorkers` Helm variable to manage the Workers setting for the output plugin if you are using the Helm chart.
{: tip}

The Helm chart for [Openshift](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy) and [Kubernetes](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy) deployments are configured with 4 workers since this is generally a good setting for most Kubernetes workloads.

Here are some considerations when setting the `Workers` value in your environment:

- Reducing the number of workers from 4 to 2 might reduce the CPU requirements for the {{site.data.keyword.agent}}.

- Increasing the number of workers to greater than 4 without also increasing the CPU limit in a Kubernetes environment will usually not result in more logs processed by the {{site.data.keyword.agent}}. There is a point when the CPU will limit the throughput and must be increased as well.

- If you see messages in the {{site.data.keyword.agent}} logs reporting `[input] pausing tail` followed closely by `[input] resume tail` this is an indication that the output plugin that is sending the logs is unable to keep up with the volume of logs generated.  If the CPU usage has not reached the CPU limit defined, then increasing the number of workers will usually increase the throughput.  If the CPU usage is close to the limit, then you can need to increase the CPU limit in addition to increasing the number of workers.  It is OK if the `[input] pausing tail` message is issued a few times an hour.  If this message occurs many times a minute you should consider a configuration change.

- If you see the message `[ warn] [input:tail:tail.0] purged rotated file while data ingestion is paused, consider increasing rotate_wait`, this is usually an indication that the volume of input is significantly faster than the agent is able to process.  Failing to increase the number of workers or CPU (or both) will lead to missing logs since the rotated files are no longer being processed due to the file rotation and the ingestion is paused.  You need to increase the workers or CPU limits (or both) if you are encountering this error.
