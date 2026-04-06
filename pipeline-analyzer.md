---

copyright:
  years:  2024, 2026
lastupdated: "2026-04-06"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


#  Pipeline analyzer
{: #pipeline-analyzer}

In {{site.data.keyword.logs_full}}, you can use the pipeline analyzer to gain full visibility into how your logs are processed before being available for search. You can inspect logs as they move through your data pipelines and gain insights into any parsing rule that a log goes through before it is available for search.
{: shortdesc}

In complex environments, logs often flow from multiple services, applications, and infrastructure. To handle this scale, you might have customized processing pipelines—for security, compliance, observability, and more. These pipelines parse, enrich, and route logs based on TCO policies, enabling advanced monitoring and faster issue resolution. As the environment grows, pipelines multiply, and misconfigurations, conflicting rules, or visibility gaps can lead to incorrect parsing, broken dashboards, and monitoring failures. Using the Pipeline Analyzer helps you gain full visibility into how your logs are processed before being available for search.

With the Pipeline Analyzer, teams can trace log processing flows in order to:
- Visualize the full processing flow of logs on demand
- Compare raw and modified logs
- Troubleshoot pipeline behaviour with pinpoint accuracy


## Prerequisites
{: #pipeline-analyzer-prereqs}

- An {{site.data.keyword.cloud_notm}} account.
- An {{site.data.keyword.logs_full_notm}} instance.
- Permissions in {{site.data.keyword.logs_full_notm}} to configure the Pipeline Analyzer. You need the role **Manager** that includes the action **logs.pipeline-analyzer.read**. For more information, see [Getting started with IAM](/docs/cloud-logs?topic=cloud-logs-iam).

## Launching the Pipeline Analyzer
{: #pipeline-analyzer-start-using-pipeline-analyzer}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. In the dashboard, click **Data Pipeline** > **Pipeline Analyzer**.

The Pipeline Analyzer opens.


## Filtering logs
{: #pipeline-analyzer-capture-and-filter-logs-on-demand}

You can filter logs that are analyzed through the Pipeline Analyzer by using any of the following methods:
- Filtering logs on demand by choosing the option `Streaming`: You can define a query, and apply filters based on `application`, `subsystem` and `severity`. Only those logs meeting your filter criteria are analyzed.

- Inspecting real-time log processing by choosing the option `Raw Sample log`: You can paste a sample raw log for analysis.



## Limitations
{: #pipeline-analyzer-limitations}

Consider the following limitations when using the Pipeline Analyzer:
- Logs are not saved after you leave the page.
- Each session is limited to 2,000 logs or 10 minutes—whichever comes first.
- Currently supports parsing rules only.
