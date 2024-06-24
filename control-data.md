---

copyright:
  years:  2024
lastupdated: "2024-06-11"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Controlling data ingested for search in {{site.data.keyword.logs_full_notm}}
{: #control-data}

You can control the data that is ingested, and is available to be searched in {{site.data.keyword.logs_full_notm}}. Data can be dropped during ingestion or by using parsing rules.
{: shortdesc}

![Flow of logs through {{site.data.keyword.logs_full_notm}}](images/Cloud-Logs-data-pipeline-02.svg "Flow of logs through {{site.data.keyword.logs_full_notm}}"){: caption="Flow of logs through {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}

## TCO policy to drop logs
{: #cd-tco}

Logs can be dropped before processed by any of the three [TCO pipelines](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines) by [creating a TCO policy.](/docs/cloud-logs?topic=cloud-logs-tco-optimizer#tco-optimizer-create-policy)

TCO policies can drop logs from being processed by any of the {{site.data.keyword.logs_full_notm}} TCO pipelines based on three metadata fields that are contained in the log data:

- [Application name](/docs/cloud-logs?topic=cloud-logs-metadata#md-app-name)
- [Subsystem name](/docs/cloud-logs?topic=cloud-logs-metadata#md-sys-name)
- Severity - `critical`, `error`, `warn`, `info`, `debug`, and `trace`.

TCO policies can also determine which of the three TCO pipelines are used to process the logs.

- [{{site.data.keyword.frequent-search}}](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines#tco-optimizer-high)

- [{{site.data.keyword.monitoring}}](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines#tco-optimizer-medium)

- [{{site.data.keyword.compliance}}](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines#tco-optimizer-low)

The TCO policy is applied when data is received by the ingestion endpoint and before any other {{site.data.keyword.logs_full_notm}} processing.

## Using parsing rules
{: #cd-parsing}

After TCO policies are applied, you can drop or remove data within ingested logs by using [parsing rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules).

### Block parsing rule
{: #cd-block}

You can drop ingested logs that weren't dropped by TCO policies by using the `block` parsing rule. The `block` rule drops logs based on a [RegEx expression](/docs/cloud-logs?topic=cloud-logs-parse-rules-regex).

If you configure a rule group, any application name, subsystem name, and severity filtering are applied before the `block` rule is applied.

Only 15% of low-priority log volume is counted against the {{site.data.keyword.frequent-search}} [data usage quota](/docs/cloud-logs?topic=cloud-logs-data-usage&interface=ui). However, when your `block` rule is, if you select **View blocked logs in LiveTail and archive to IBM Cloud Object Storage**, your dropped logs are saved in the {{site.data.keyword.compliance}} pipeline. You can search the logs from archived data. In this way, ingested log data is not lost.

Using the `block` rule is a way to move logs to low priority in a more refined way than using TCO policies. For performance reasons, specify `block` rules in a rules group before any other parsing rules.
{: tip}

### Remove parsing rule
{: #cd-remove}

You can drop parts of ingested logs that you don't need by using the `remove` parsing rule.

10% of the data volume that is removed is counted against the {{site.data.keyword.frequent-search}} [data usage quota](/docs/cloud-logs?topic=cloud-logs-data-usage&interface=ui), similar to data blocked by a `block` rule.
{: note}

By removing log data that you do not need, you can control {{site.data.keyword.logs_full_notm}} costs. However, removed data is still archived to {{site.data.keyword.cos_full_notm}} by the {{site.data.keyword.compliance}} pipeline and is available for search.

