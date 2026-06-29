---

copyright:
  years:  2024, 2026
lastupdated: "2026-06-29"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring metrics for {{site.data.keyword.logs_full_notm}}
{: #monitoring}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.logs_full_notm}}, generate platform metrics that you can use to gain operational visibility into the performance and health of the service in your account.
{: shortdesc}

You can use {{site.data.keyword.metrics_router_full_notm}}, a platform service, to route platform metrics in your account to a destination of your choice by configuring targets and routes that define where platform metrics are sent. For more information, see [About {{site.data.keyword.metrics_router_full_notm}} in {{site.data.keyword.cloud_notm}}](/docs/metrics-router?topic=metrics-router-about).

{{site.data.keyword.mon_full_notm}} is a third-party cloud-native, and container-intelligence management system that can be included as part of your {{site.data.keyword.cloud_notm}} architecture. It offers administrators, DevOps teams, and developers full-stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. For more information, see [Monitoring in IBM Cloud](/docs/monitoring?topic=monitoring-about-monitor).

You can use {{site.data.keyword.mon_full}} to visualize and alert on metrics that are generated in your account and routed by {{site.data.keyword.metrics_router_full_notm}} to an {{site.data.keyword.mon_full_notm}} instance.

## Locations where metrics are generated
{: #mon-locations}

{{site.data.keyword.logs_full_notm}} sends metrics in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Montreal (`ca-mon`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where metrics are sent in Americas locations" caption-side="top"}
{: #mon-table-1}
{: tab-title="Americas"}
{: tab-group="mon"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where metrics are sent in Asia Pacific locations" caption-side="top"}
{: #mon-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="mon"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [No]{: tag-red} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where metrics are sent in Europe locations" caption-side="top"}
{: #mon-table-3}
{: tab-title="Europe"}
{: tab-group="mon"}
{: class="simple-tab-table"}
{: row-headers}


## Enabling platform metrics for {{site.data.keyword.logs_full_notm}}
{: #monitoring-enable}

Platform metrics for {{site.data.keyword.logs_full_notm}} are enabled automatically when you provision an {{site.data.keyword.logs_full_notm}} instance. No additional configuration is required to start receiving metrics.


## Viewing metrics
{: #monitoring-view}

To monitor {{site.data.keyword.logs_full_notm}} metrics, you must launch the {{site.data.keyword.mon_full_notm}} web UI for the instance that is enabled for platform metrics in the region where your {{site.data.keyword.logs_full_notm}} instance is provisioned.

If you manage routing of platform metrics in the account through {{site.data.keyword.metrics_router_full_notm}}, you must launch the {{site.data.keyword.mon_full_notm}} web UI for the instance that is configured to collect {{site.data.keyword.logs_full_notm}} metrics.

### Launching {{site.data.keyword.mon_full}} from the {{site.data.keyword.logs_full_notm}} dashboard
{: #monitoring-view-ui}

You can launch the {{site.data.keyword.mon_full_notm}} UI directly from the {{site.data.keyword.logs_full_notm}} service instance page:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](/icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Logging**. By default **Instances** are displayed.

4. Click the **Cloud Logs** tab.

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

   If the instances are not displayed, click **Instances** > **Cloud Logs** to display the list of logging instances.

4. Click **Open dashboard** for your selected instance.

5. In the *Overview* page, click **Actions > Monitoring**.

    If you need to set up monitoring, select **Add monitoring** to configure the account. Once you configure it, you get the option **Monitoring**. For more information, see [Provision an instance of {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-provision) and [Configuring monitoring in the account](/docs/metrics-router?topic=metrics-router-getting-started).

    The {{site.data.keyword.mon_full_notm}} UI opens and automatically loads the **Cloud Logs Overview** dashboard, pre-filtered to your service instance and region.

### Launching {{site.data.keyword.mon_full}} from the Observability page
{: #monitoring-view-ob}

For more information about launching the {{site.data.keyword.mon_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.mon_full_notm}} documentation.](/docs/monitoring?topic=monitoring-launch)

## Monitoring {{site.data.keyword.logs_full_notm}}
{: #monitoring-monitor}

Use platform metrics to understand the ingestion health of your {{site.data.keyword.logs_full_notm}} instance. Key areas to monitor include:
- Log ingestion volumes
- Log rejection rate
- Data usage

### Log ingestion volume
{: #monitoring-monitor-1}

Track the total number of log entries accepted by your {{site.data.keyword.logs_full_notm}} instance. A sustained drop in accepted log entries may indicate a connectivity issue between your log sources and the {{site.data.keyword.logs_full_notm}} instance, or a configuration problem with your log agents.

Monitor the **Number of Log Entries Accepted** panel in the Cloud Logs Overview dashboard and set alerts if values drop below expected thresholds for your workload.

### Log rejection rate
{: #monitoring-monitor-2}

Track the number of log entries rejected by {{site.data.keyword.logs_full_notm}}. Rejections can occur due to quota limits, malformed payloads, or TCO policy configurations. Use the `ibm_logs_rejection_reason` label to identify the root cause and take corrective action.

Monitor the **Number of Log Entries Rejected** panel and the **Rate of Rejected Log Entries** chart in the Cloud Logs Overview dashboard.

### Data usage
{: #monitoring-monitor-3}

Track the volume of data (in bytes) processed per service instance, segmented by application name, subsystem name, TCO priority, and log severity. This helps you understand cost drivers and identify applications generating unexpectedly high data volumes.

Monitor the **Data Usage Section** panels in the {{site.data.keyword.logs_full_notm}} Overview dashboard.

## Cloud Logs predefined dashboards
{: #monitoring-dashboards}

{{site.data.keyword.logs_full_notm}} provides a predefined dashboard template, **Cloud Logs Overview** (`ibm_logs_overview`), that is automatically available in the **Dashboard Library > IBM** section of all {{site.data.keyword.mon_full_notm}} instances that receive {{site.data.keyword.logs_full_notm}} platform metrics.

The dashboard includes the following panels:

| Section | Panel | Description |
|---------|-------|-------------|
| Logs: Accepted | Number of Log Entries Accepted | Total count of accepted log entries |
| Logs: Accepted | Average Rate of Accepted Log Entries | Average ingestion rate |
| Logs: Accepted | Rate of Accepted Log Entries | Time-series chart of accepted log entry rate |
| Logs: Rejected | Number of Log Entries Rejected | Total count of rejected log entries |
| Logs: Rejected | Average Rate of Rejected Log Entries | Average rejection rate |
| Logs: Rejected | Rate of Rejected Log Entries | Time-series chart of rejected log entry rate |
| Data Usage Section | Data Usage Total | Total data usage in bytes |
| Data Usage Section | Average Data Usage | Average data usage |
| Data Usage Section | Daily Data Usage | Daily data usage trend |
{: caption="{{site.data.keyword.logs_full_notm}} Overview dashboard panels" caption-side="bottom"}

The dashboard is automatically scoped to your `ibm_location` and `ibm_service_instance` when launched from the {{site.data.keyword.logs_full_notm}} service instance page.

## Metrics available by service plan
{: #monitoring-metrics-by-plan}

Platform metrics for {{site.data.keyword.logs_full_notm}} are available for all service plans.

## Predefined alerts
{: #monitoring-alerts}

{{site.data.keyword.logs_full_notm}} does not include predefined alerts at this time.

You can create custom alerts in {{site.data.keyword.mon_full_notm}} based on the platform metrics.

## Metrics available by Service Plan
{: metrics-by-plan}

| Metric Name |
|-----------|
| [{{site.data.keyword.logs_full_notm}} accepted log metrics](#ibm_logs_accepted_log_entries_total) |
| [{{site.data.keyword.logs_full_notm}} data usage bytes per service instance](#ibm_logs_data_usage_bytes_total) |
| [{{site.data.keyword.logs_full_notm}} rejected log metrics](#ibm_logs_rejected_log_entries_total) |
{: caption="Table 1: Metrics Available by Plan Names" caption-side="top"}

### {{site.data.keyword.logs_full_notm}} accepted log metrics
{: #ibm_logs_accepted_log_entries_total}

Total number of accepted logs

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_logs_accepted_log_entries_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance` |
{: caption="Table 2: {{site.data.keyword.logs_full_notm}} accepted log metrics metric metadata" caption-side="top"}

### {{site.data.keyword.logs_full_notm}} data usage bytes per service instance
{: #ibm_logs_data_usage_bytes_total}

Total data usage in bytes per applicationName, subsystemName, priority and severity

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_logs_data_usage_bytes_total`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Application that generated the traffic, Subsystem that generated the traffic, TCO priority (high, medium, low), Log severity (critical, error, warn, info, debug, trace)` |
{: caption="Table 3: {{site.data.keyword.logs_full_notm}} data usage bytes per service instance metric metadata" caption-side="top"}

### {{site.data.keyword.logs_full_notm}} rejected log metrics
{: #ibm_logs_rejected_log_entries_total}

Total number of rejected logs

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_logs_rejected_log_entries_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `{{site.data.keyword.logs_full_notm}} rejected reason, Service instance` |
{: caption="Table 4: {{site.data.keyword.logs_full_notm}} rejected log metrics metric metadata" caption-side="top"}


## Attributes for segmentation
{: #monitoring-attributes}

### Global attributes
{: #monitoring-attributes-global}

The following attributes are available for all {{site.data.keyword.logs_full_notm}} platform metrics.

| Attribute | Description |
|-----------|-------------|
| `ibm_ctype` | The cloud type. Value is `public`. |
| `ibm_location` | The region where the {{site.data.keyword.logs_full_notm}} instance is provisioned (for example, `eu-gb`). |
| `ibm_scope` | The account scope in the format `a/{account_id}`. |
| `ibm_service_name` | The service name. Value is `logs`. |
| `ibm_service_instance` | The GUID of the {{site.data.keyword.logs_full_notm}} service instance. |
{: caption="Global segmentation attributes" caption-side="bottom"}

### Additional attributes
{: #monitoring-attributes-add}

The following attributes are available to segment specific metrics.

| Attribute | Applicable metric(s) | Description |
|-----------|----------------------|-------------|
| `ibm_logs_rejection_reason` | `ibm_logs_rejected_log_entries` | The reason the log entry was rejected. |
| `ibm_logs_application_name` | `ibm_logs_data_usage_bytes_total` | The application that generated the log traffic. |
| `ibm_logs_subsystem_name` | `ibm_logs_data_usage_bytes_total` | The subsystem that generated the log traffic. |
| `ibm_logs_priority` | `ibm_logs_data_usage_bytes_total` | The TCO priority of the logs: `high`, `medium`, or `low`. |
| `ibm_logs_severity` | `ibm_logs_data_usage_bytes_total` | The severity of the logs: `critical`, `error`, `warn`, `info`, `debug`, or `trace`. |
{: caption="Additional segmentation attributes" caption-side="bottom"}
