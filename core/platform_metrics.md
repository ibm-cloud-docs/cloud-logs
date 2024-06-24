---

copyright:
  years:  2024
lastupdated: "2024-04-01"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Platform metrics for {{site.data.keyword.logs_full_notm}}
{: #platform_metrics}

You can use the {{site.data.keyword.mon_full}} service to monitor platform metrics that are exposed by {{site.data.keyword.logs_full_notm}}. For example, you can use it to monitor how {{site.data.keyword.logs_full_notm}} is routing events in each region where you are collection auditing events.
{: shortdesc}

{{site.data.keyword.mon_full_notm}} is a cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. You can use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.

## Enabling platform metrics
{: #monitoring_metrics_enable}

Platform metrics are metrics that are exposed by enabled-monitoring services and the platform in IBM Cloud. You can use them to find and take action on configuration problems and possible outages.
- To monitor platform metrics, you must provision a {{site.data.keyword.mon_short}} instance in the same region where the metrics are exposed.

    For example, you can use the {{site.data.keyword.mon_full_notm}} service to monitor that events are forwarded to the configured destination.

- You can configure 1 instance only of the {{site.data.keyword.mon_full_notm}} service per region to collect platform metrics in that location.

    In a region, before you configure a {{site.data.keyword.mon_short}} instance to collect platform metrics, check with the account or service administrator if another {{site.data.keyword.mon_short}} instance has already been configured. You may not have permissions to see all {{site.data.keyword.mon_short}} instances in the region.
    {: note}

- If you have configured {{site.data.keyword.logs_full_notm}} in more than one region, you must enable platform metrics for each region.

For more information on how to enable platform metrics, select 1 of the following options:

[![Option 1. UI](../images/platform_metrics_option_1.svg)](/docs/monitoring?topic=monitoring-platform_metrics_enabling#platform_metrics_enabling_ui) [![Option 2. CLI](../images/platform_metrics_option_2.svg)](/docs/monitoring?topic=monitoring-platform_metrics_enabling#platform_metrics_enabling_cli)

## Viewing metrics for {{site.data.keyword.logs_full_notm}}
{: #monitoring_metrics_view_v2}

You monitor metrics in the {{site.data.keyword.mon_short}} web UI.

To monitor {{site.data.keyword.logs_full_notm}} metrics, you must launch the {{site.data.keyword.mon_short}} UI for the instance that is enabled for platform metrics in the region where your target is defined. For example, if you have a target defined in US-South, you must launch the {{site.data.keyword.mon_short}} instance in US-South that has the flag platform metrics. For more information, see [Launching the {{site.data.keyword.mon_short}} UI from the Observability page](/docs/monitoring?topic=monitoring-launch#launch_step2).

You can use the *IBM {{site.data.keyword.logs_full_notm}} Overview* predefined dashboard template to monitor {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}}.

To open the predefined {{site.data.keyword.logs_full_notm}} template, complete the following steps from the {{site.data.keyword.mon_short}} UI:

1. In the {{site.data.keyword.mon_short}} UI, go to **Dashboards** &gt; **Dashboard templates** &gt; **IBM**.
2. Select **IBM {{site.data.keyword.logs_full_notm}} Overview**.

You cannot modify a dashboard template. However, you can copy the template and create a custom dashboard that you can then configure.
{: note}

Next, choose any of the following tasks to learn more about how to manage and work with platform metrics:

[![Working with platform metrics](../images/platform_metrics_task_1.svg)](/docs/monitoring?topic=monitoring-platform_metrics_working) [![Controlling what data is visible](../images/platform_metrics_task_2.svg)](/docs/monitoring?topic=monitoring-platform_metrics_working#controlling-what-data-is-visible) [![Monitoring metrics through dashboards](../images/platform_metrics_task_3.svg)](/docs/monitoring?topic=monitoring-platform_metrics_working#platform_metrics_working_dash) [![Configuring an alert on a platform metric](../images/platform_metrics_task_4.svg)](/docs/monitoring?topic=monitoring-platform_metrics_working#platform_metrics_working_alert) [![Controlling access by using teams](../images/platform_metrics_task_5.svg)](/docs/monitoring?topic=monitoring-platform_metrics_working#platform_metrics_working_team)

## Metrics
{: #monitoring_metrics_details}

{{site.data.keyword.logs_full_notm}} exposes the following metrics:

- [Total number of events successfully sent to the storage target](/docs/atracker?topic=atracker-monitoring_metrics#ibm_atracker_successful_events_by_target)
- [Total number of events that failed to send to the storage target](/docs/atracker?topic=atracker-monitoring_metrics#ibm_atracker_failed_events_by_target)
- [Total number of events that are discarded](/docs/atracker?topic=atracker-monitoring_metrics#ibm_atracker_discarded_events)


### Total number of events successfully sent to the storage target
{: #ibm_atracker_successful_events_by_target}

Total number of events that are successfully sent to the storage target.

| Metadata         | Description |
|------------------|-------------|
| `Metric Name`    | `ibm_atracker_successful_events_by_target` |
| `Metric Type`    | `counter` |
| `Value Type`     | `none` |
| `Segment By`     | `target type` |
{: caption="Table 1. Total number of events successfully sent to the storage target" caption-side="top"}


### Total number of events that failed to send to the storage target
{: #ibm_atracker_failed_events_by_target}

Total number of events that failed to send to the storage target.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_atracker_bad_config_discarded_events`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By`  | `target type, reason` |
{: caption="Table 2. Total number of events that failed to send to the storage target" caption-side="top"}

### Total number of events that are discarded
{: #ibm_atracker_discarded_events}

Total number of events that are discarded.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_atracker_failed_events_by_target`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By`  | `target type, reason` |
{: caption="Table 3. Total number of events that are discarded" caption-side="top"}

### Global Attributes
{: #global-attributes}

The following attributes are available for all metrics.

| Attribute        | Attribute Name            | Attribute Description |
|------------------|---------------------------|-----------------------|
| `Cloud Type`     | `ibm_ctype`               | The cloud type is `public`, `dedicated`, or `local`. |
| `Location`       | `ibm_location`            | The location of the monitored resource, which can be a region, data center, or global. |
| `Resource`       | `ibm_resource`            | The resource that is measured by the service, which is typically an identifying name or GUID. |
| `Resource Type`  | `ibm_resource_type`       | The type of the resource that is measured by the service. |
| `Scope`          | `ibm_scope`               | The scope is the account, organization, or space GUID associated with the metric. |
| `Service name`   | `ibm_service_name`        | The name of the service that is generating this metric. |
{: caption="Table 4. Global atributes" caption-side="top"}

### More attributes
{: #additional-attributes}

The following attributes are available for one or more attributes described in the previous tables. See the individual metrics for options.

| Attribute     | Attribute Name             | Attribute Description |
|---------------|----------------------------|-----------------------|
| `target type` | `ibm_atracker_target_type` | The target type destination of the event. Valid values are: `cloud_object_storage`, `logdna`, or `event_streams`. |
| `reason`      | `ibm_atracker_reason_code` | The reason for the failure of an event delivery to its destination. |
{: caption="Table 5. Other atributes" caption-side="top"}
