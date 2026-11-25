---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-25"

keywords: views, extensions, saved views, manifest, directory layout

subcollection: cloud-logs

content-type: tutorial
completion-time: 15m

---

{{site.data.keyword.attribute-definition-list}}


# Data usage v2 extension for {{site.data.keyword.logs_full_notm}}
{: #extensions-data-usage-v2}

The Data Usage v2 extension provides essential visibility into log and metric ingestion across an {{site.data.keyword.logs_full_notm}} instance, enabling you to monitor consumption patterns, control costs, and optimize your TCO configuration.
{: shortdesc}

The key capabilities include:

1. Accurate ingestion tracking for active and blocked logs and metrics.

2. Cost optimization by identifying blocked data and forecasting daily log ingestion volumes.

3. Proactive alerting on unexpected ingestion spikes before budget overruns occur.


## Before you begin
{: #extensions-data-usage-v2-prereq}

This extension does not require parsing rules. It uses the internal system metric `cx_data_usage_bytes_total` to report ingestion data.

Before you deploy this extension, make sure that the following requirements are met:

- A {{site.data.keyword.cos_full_notm}} data bucket and metrics bucket are attached to your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Configuring the metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
- System metrics are enabled on your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Enabling data usage metrics](/docs/cloud-logs?topic=cloud-logs-data-usage-metrics).


## Included alerts
{: #extensions-data-usage-v2-included-alerts}

The following table lists the {{site.data.keyword.logs_full_notm}} alerts with severity: 


| Alert name                   | Severity   |   Condition and Threshold  | PromQL Query | 
|------------------------------------ |---------| ------------------| ----------------|
| Data usage - Spike detected on increase of logs by priority  | P1 | Alert triggers when log ingestion for an application, subsystem, and severity combination exceeds 30 MB within a 10-minute window |  `topk(5, sum(cx_data_usage_bytes_total{application_name =~ ".+",subsystem_name =~ ".+", pillar = "logs"}) by (application_name,subsystem_name,severity))` | 
| Data Usage - Unexpected spike on metrics data |  P2  | `Alert triggers when total metrics ingestion exceeds 54 MB in 10 minutes   | `sum(cx_data_usage_bytes_total{pillar="metrics"})`     |
| Data Usage - Unexpected spike of logs ingested today |   P2  | Alert triggers when the total account log ingestion exceeds 75 MB in 10 minutes     | `sum(cx_data_usage_bytes_total{pillar="logs"})` |
| Data usage - Spike on logs ingested by application and subsystem | P5   | Alert triggers when the application and subsystem combination exceeds ~30.15 MB in 10 minutes   |   `topk(5, sum(cx_data_usage_bytes_total{subsystem_name =~ ".+", pillar = "logs"}) by (application_name,subsystem_name))`  | 
| Data Usage - Reached daily estimated logs ingestion volume | P3 | Alert triggers when projected daily log volume reaches or exceeds 70.26 MB    |   `sum(cx_data_usage_bytes_total{pillar = "logs"}) + max(increase(cx_data_usage_bytes_total{pillar = "logs"}[1h])) * ((24 - ceil((time() % 86400) / 3600)) % 24)`   | 
{: caption="Alerts with severity" caption-side="bottom"}


## Included dashboards
{: #extensions-data-usage-v2-included-dashboards}

You can deploy any of the following predefined dashboards:

- `High Level Data Usage Overview`: Use this dashboard to monitor real-time gauges that compare active versus blocked logs and metrics, view daily usage projections, review pillar breakdowns, and identify the top 10 applications by ingestion increase over the last 24 hours.
- `Compare Last 24 Hours with Last Week`: Use this dashboard to compare the ingestion rate for the last 24 hours against the same day of the previous week to identify abnormal trends.





