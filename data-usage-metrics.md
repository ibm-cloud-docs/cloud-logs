---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Enabling data usage metrics
{: #data-usage-metrics}

In {{site.data.keyword.logs_full_notm}}, you can enable data usage metrics to collect predefined metrics that you can use to monitor your data usage. Then, you can use these metrics in custom dashboards, insights, and alerts
{: shortdesc}


## Prereqs
{: #data-usage-metrics-prereqs}


To be able to enable data usage metrics, you must [configure a metrics bucket.](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
{: note}


## Enabling metrics
{: #data-usage-metrics-1}

Complete the following steps:
1. In the navigation bar, click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Data Usage**.

2. Enable data usage metrics.


After you enable data usage metrics, it can take up to two hours to see metrics.
{: note}


## Predefined metrics
{: #data-usage-metrics-2}

The following pre-defined metric is available when you enable data usage metrics:
- `cx_data_usage_bytes_total`: Reports GB Sent.


In the Data Usage page in the UI, you can see the following information per day for the range of time that you select:
- Maximum bytes sent per day
- Total number of bytes sent

You can select data for the current month, the past 30 days, or the past 90 days.

## Labels available for metrics
{: #data-usage-metrics-3}

The information collected on these metrics includes the following labels:

- `tier`: Storage for logs. Valid values are: `high`, and `low`.
- `pillar`: Type of traffic. Valid values are: `logs`, and `metrics`.
- `severity`:	Log severity. Valid values are: `critical`, `error`, `warn`, `info`, `debug`, and `trace`.
- `priority`:	TCO priority. Valid values are: `high`, `medium`, `low`, and `blocked`.
- `subsystem_name`:	Host from where logs are generated.
- `application_name`: Application that generates logs.
- `blocking_reason_type`: The reason why traffic is blocked. Valid values are: `tco_policy` or `parsing_rule`.
- `blocking_reason_name`: The name of the TCO policy or parsing rule which is blocking traffic.


## Next steps
{: #data-usage-metrics-next}

Check how you can generate data usage reports. For more information, see:
- [Generating detailed usage reports](/docs/cloud-logs?topic=cloud-logs-data-usage-detailed-reports)
- [Generating data usage overview reports](/docs/cloud-logs?topic=cloud-logs-data-usage-reports)
