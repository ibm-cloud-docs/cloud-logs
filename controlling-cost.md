---

copyright:
  years:  2024, 2025
lastupdated: "2025-08-20"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Controlling cost
{: #controlling-cost}

After you start using {{site.data.keyword.logs_full}}, you might find that you need to adjust how data is processed by {{site.data.keyword.logs_full_notm}} to control costs.
{: shortdesc}

You can configure {{site.data.keyword.logs_full_notm}} or adjust the data that is ingested by {{site.data.keyword.logs_full_notm}} to control your usage cost.

## Selecting the best service plan
{: #cc-sp}

Review the available [service plans and pricing](/docs/cloud-logs?topic=cloud-logs-service_plans). The cost for the [data pipeline](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines) where you plan to store data affects your total cost.

Also, consider how long you need to keep your data for fast search in {{site.data.keyword.frequent-search}}. You can configure your {{site.data.keyword.logs_full_notm}} instance to save your data in {{site.data.keyword.frequent-search}} for a shorter time period.

Data is metered by the service per gigabytes ingested. You can configure [data usage metrics](/docs/cloud-logs?topic=cloud-logs-data-usage-metrics) to monitor your data usage. Data usage metrics requires that you have a [metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket) configured.
{: tip}

## Configuring the TCO optimizer
{: #cc-tco}

By default, when an {{site.data.keyword.logs_full_notm}} instance is created, all data flows to the {{site.data.keyword.frequent-search}} data pipeline. While this pipeline gives you the fastest search, it is the highest cost pipeline.

To control costs, you want to optimize the pipeline where data is sent.

By defining the data pipeline based on the importance of the data to your business, the TCO Optimizer can help you improve real-time analysis and alerting and helps you manage costs.

For information on configuring the TCO optimizer, see [Configuring the TCO Optimizer](/docs/cloud-logs?topic=cloud-logs-tco-optimizer).

### Using TCO policies
{: #cc-tcop}

How logs are associated to pipelines is determined by [policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer#tco-optimizer-create-policy). Policies are applied on combinations of applications, subsystems, and log severity as logs are ingested. Logs are assigned to the appropriate TCO pipeline based on the policy content.

You must have a [{{site.data.keyword.cos_full_notm}} data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket) configured before creating a policy.
{: attention}



## Understanding data ingestion
{: #cc-ingest}

To understand how to contol your cost when using {{site.data.keyword.logs_full_notm}}, you need to understand how data is ingested by the service.

{{site.data.keyword.logs_full_notm}} ingests data from multiple sources and that data is processed in a specific order:

1. Logs are sent by the source. 

   * Operational logs are sent using an agent or API REST call. 
   * Platform logs and activity tracking events are sent by IBM Cloud.

2. {{site.data.keyword.logs_full_notm}} ingests (receives) the data.

3. {{site.data.keyword.logs_full_notm}} parsing rules are applied to the ingested data.

4. TCO [policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer#tco-optimizer-create-policy) are applied and the data is assigned to the appropriate [data pipeline](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines), or dropped, depending on the policy.

A log is considered to be ingested for the purposes of billing once the parsing rules and TCO policies have been applied.  Logs that are blocked before being sent to the data pipelines do not incur charges and these logs are not retained.
{: important}

## Controlling ingested data
{: #cc-ingest-control}

In addition to controlling the data pipelines where your data is kept within {{site.data.keyword.logs_full_notm}}, you can control the data that is ingested by {{site.data.keyword.logs_full_notm}}.

### Using parsing rules 
{: #cc-parse}

You can use the *block* parsing rule to filter out incoming logs based on a RegEx expression. For more information on configuring a *block* parsing rule, see [Blocking log data](/docs/cloud-logs?topic=cloud-logs-parse-block-rule&interface=ui).

You aren't limited to blocking full log lines. Fields in log lines that you don't need can be removed using parsing rules. For information on removing fields, see [Removing fields from logs by using the *Remove fields* rule](/docs/cloud-logs?topic=cloud-logs-parse-remove-rule&interface=ui).

### Filtering and restructuring data sent through the {{site.data.keyword.agent}}
{: #cc-agent}

If you are sending operational logs to {{site.data.keyword.logs_full_notm}} by using the {{site.data.keyword.agent}}, you can parse and restructure the log data for consistency and to remove data that you might not require in {{site.data.keyword.logs_full_notm}}.

* You can use the Fluent Bit [grep filter with the exclude option](https://docs.fluentbit.io/manual/pipeline/filters/grep){: external}.

* You can use the Fluent Bit [modify filter](https://docs.fluentbit.io/manual/3.2/pipeline/filters/modify){: external} to drop fields that you don't need.

* When installing the {{site.data.keyword.agent}}, make use of the [`excludeLogSourcePaths`](/docs/cloud-logs?topic=cloud-logs-agent-helm-template-clusters#agent-helm-template-clusters-chart-options-log-source-paths) option when installing with the helm chart or the [`Exclude_Path`](/docs/cloud-logs?topic=cloud-logs-agent-helm-template-clusters#agent-helm-template-clusters-chart-options-log-source-paths) option on the `tail` plug-in (Linux and Windows installations) to not send logs from specific locations.

* You can use [Lua scripts](https://docs.fluentbit.io/manual/pipeline/filters/lua){: external} to filter and modify data that is being sent to {{site.data.keyword.logs_full_notm}} prior to ingestion.

#### Making sure logging data is well structured
{: #cc-structure}

When you modify log data, you need to make sure that the data sent to {{site.data.keyword.logs_full_notm}} is well-formatted so {{site.data.keyword.logs_full_notm}} can process the data correctly.

* Logs should be sent in either JSON format or a filter is used with the {{site.data.keyword.agent}} to convert the content into JSON format.

* Since TCO policies use severity information within the log data to assign logs to the appropriate data pipeline, for consistent assignment it is best to make sure that the log data contain an appropriate `level`, `loglevel`, or `severity` value rather than having the {{site.data.keyword.agent}} or [{{site.data.keyword.logs_full_notm}} imply the severity](/docs/cloud-logs?topic=cloud-logs-severities).

* For logs originating from non-Kubernetes sources, log lines need to have [`application` and `subsystemName` fields](/docs/cloud-logs?topic=cloud-logs-metadata) included. These fields are also used by TCO processing.

* Logs should also include timestamps in UTC format. Alternately the {{site.data.keyword.agent}} can be configure to offset the timestamp before sending the logs. See the information on `Time_Offset` and `Time_System_Timezone` in the [Fluent Bit documentation](https://docs.fluentbit.io/manual/pipeline/parsers/configuring-parser){: external}.

* Fields that will be frequently used in searches (for example, `http_error_code`) should be [extracted into separate keys](/docs/cloud-logs?topic=cloud-logs-parse-extract-rule&interface=ui), rather than being included in the log line.
