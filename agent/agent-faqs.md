---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-12"

keywords:

subcollection: cloud-logs

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for the {{site.data.keyword.agent}}
{: #agent_faq}

Frequently asked questions about the {{site.data.keyword.agent}}.
{: shortdesc}

## Is there a recommended setting for the Workers configuration for the {{site.data.keyword.agent}}?
{: #agent_faq_agent_workers}
{: faq}

A worker, in the context of the {{site.data.keyword.agent}}, represents a CPU thread that is available to the {{site.data.keyword.agent}} for handling logs.
You can configure the number of available workers that are available in the output plugin configuration.

The `Workers` configuration setting for the output plug-in depends on the log volume being processed.  See the [agent workers configuration considerations](/docs/cloud-logs?topic=cloud-logs-agent-plugin-parameters#agent-worker-configuration-considerations) which describes the logs that you can look for to help determine the appropriate setting for your environment.

For example, the {{site.data.keyword.agent}} is deployed as a Daemonset in a Kubernetes or OpenShift cluster. 1 {{site.data.keyword.agent}} pod is deployed in each worker (node) in the cluster.  The Helm charts for Openshift and Kubernetes deployments are configured with 4 workers by default. Each {{site.data.keyword.agent}} pod is configured by default to use 4 fluent-bit workers (or threads) to handle the processing of logs in each pod. You can use the guidance in [agent workers configuration considerations](/docs/cloud-logs?topic=cloud-logs-agent-plugin-parameters#agent-worker-configuration-considerations) to configure the number of workers based on your log volumes.



## What do the `[input] pausing tail` messages in my agent log mean?
{: #agent_faq_agent_input_pausing_tail}
{: faq}

The message `[input] pausing tail` is an indication that the buffers managed by the {{site.data.keyword.agent}} are full and that the {{site.data.keyword.agent}} is unable to process any more content from the file so it's pausing the input processing.  This can happen for a number of reasons and the frequency and persistence of the warning message will determine your action.

- If the logging volume increase is temporary and the message only occurs a few times over an hour and is followed almost immediately by a `[input] resume tail` message, then this is likely a temporary situation and you can safely ignore the message.  Some logs might be delayed by less than a minute, but generally speaking you will likely not notice a difference when you review your logs in {{site.data.keyword.logs_full_notm}}.

- If the `[input] resume tail` message does not appear within a few seconds then this might be an indication of a problem sending to {{site.data.keyword.logs_full_notm}}.  You should check the network connectivity between the {{site.data.keyword.agent}} and {{site.data.keyword.logs_full_notm}}.  Not observing the `[input] resume tail` message may also be an indication of an {{site.data.keyword.logs_full_notm}} service disruption.

- If the `[input] resume tail` and `[input] pausing tail` messages occur more than 30 times within 5 minutes, this is typically an indication that the agent is not configured appropriately to handle the log volume that the agent is processing.  This can usually be corrected by increasing the `Workers` configuration in the output plug-in, increasing the CPU limit assigned to the agent process or both actions.  See the [agent workers configuration considerations](/docs/cloud-logs?topic=cloud-logs-agent-plugin-parameters#agent-worker-configuration-considerations) for more details.

- Consider reviewing the logs that are being collected and determine whether all of the logs are required.  See the [Filtering logs](/docs/cloud-logs?topic=cloud-logs-configure-include-exclude) topic for ways that you can reduce the volume of logs sent from the {{site.data.keyword.agent}} to {{site.data.keyword.logs_full_notm}}.

## How can I send my kube audit logs to {{site.data.keyword.logs_full_notm}}?
{: #faq_kube_audit}
{: faq}


{{../_include-segments/kube-config.md}}


For more information about the `input-kubernetes.conf` file, see [Configuring whether logs are included or excluded](/docs/cloud-logs?topic=cloud-logs-configure-include-exclude).
