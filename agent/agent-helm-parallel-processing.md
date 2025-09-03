---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configure the output plugin to enable parallel processing of log data
{: #agent-helm-parallel-processing}

When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to define the number of worker threads used by the output plug-in to enable parallel processing of log data.
{: shortdesc}

The `outputWorkers` setting defines the number of worker threads used by the output plug-in to enable parallel processing of log data.

The default is  `4`.

In most environments, increasing the number of threads beyond 4 does not significantly impact performance. If your log volume is high and you’ve allocated more than 1 CPU, increasing this value to 8 can help improve output throughput.

For low-volume enviroments, reducing this value to 1 or 2 will limit the maximum log volume that can be sent to {{site.data.keyword.logs_full_notm}}, which may be suitable for smaller workloads.

```yaml
outputWorkers: 2
```
{: codeblock}

After you modify the `logs-values.yaml`, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
