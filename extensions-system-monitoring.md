---

copyright:
  years:  2024, 2025
lastupdated: "2025-11-13"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# System Monitoring extension
{: #extensions-system-monitoring}

Use the System Monitoring extension to gain insights into your system's performance and usage within an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

## What this extension deploys
{: #extensions-system-monitoring-deploys}

This extension includes one or more items.

| Includes | Number |
|----------|--------|
| [Alerts](/docs/cloud-logs?topic=cloud-logs-alerts) | 0 |
| [Dashboards](/docs/cloud-logs?topic=cloud-logs-about_dashboards) | 3 |
| [Enrichments](/docs/cloud-logs?topic=cloud-logs-enriching-data) | 0 |
| [Events to metrics](/docs/cloud-logs?topic=cloud-logs-configure-event2metrics) | 0 |
| [Rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) | 0 |
| [Views](/docs/cloud-logs?topic=cloud-logs-custom_views) | 0  |
{: caption="Items included when extension is deployed" caption-side="bottom"}

Before deploying this extension, make sure that deploying the extension will not cause you to exceed [limits for your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-limits). If deploying the extension results in limits being exceeded, the deployment will fail.
{: tip}

## Deploying the extension
{: #extensions-nginx-deploy}

You can deploy this extension in any {{site.data.keyword.logs_full_notm}} instance. This extension helps you maintain control over system resources, quickly identify issues, and ensure optimal performance within your instance.

For more information about deploying the extension, see [Deploying, managing, and removing {{site.data.keyword.logs_full_notm}} extensions](/docs/cloud-logs?topic=cloud-logs-extensions-mgmt).


{{/_include-segments/extensions-validate.md}}

## Dashboards
{: #extensions-system-monitoring-dashboards}

You can deploy any of the following predefined dashboards:
- `Logs Overview`: Use this dashboard to gain insights into the volume, types, and patterns of logs ingested by your system.
- `Mapping Exceptions`: Use this dashboard to track and troubleshoot issues related to data mapping errors in your Priority Insights logs.
- `Data Usage`: Use this dashboard to monitor data consumption and optimize TCO policies based on usage trends.
