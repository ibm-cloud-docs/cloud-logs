---

copyright:
  years:  2024, 2026
lastupdated: "2026-06-01"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Enabling system metrics
{: #data-usage-enable-metrics}

In {{site.data.keyword.logs_full_notm}}, you can enable data usage metrics to collect predefined metrics that you can use to monitor your data usage. Then, you can use these metrics in custom dashboards, insights, and alerts.
{: shortdesc}


## Prereqs
{: #data-usage-enable-metrics-prereqs}

To configure this feature, you must attach a metrics bucket to your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Configuring the metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
{: attention}

## System metrics
{: #data-usage-enable-metrics-1}

The following metrics are generated when you enable Data Usage metrics:
- `cx_data_usage_bytes_total`: Reports GB Sent.
- `cx_alerts `: Reports data when an alert is triggered or resolved.




## Enabling Data Usage metrics
{: #data-usage-enable-metrics-data-usage}

Complete the following steps to enable collection of the Data Usage metric `cx_data_usage_bytes_total`:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Data Usage**.

    The *Data Usage* page opens.

    ![Data Usage](/images/data-usage.png "Data Usage"){: caption="Data Usage" caption-side="bottom"}

3. Select **Settings**. The Data usage settings page opens.

4. In the *Data Usage visibility > Enable metrics* section, switch on the toggle **Enable metrics**.

    ![Enable Data Usage](/images/data-usage-enable.png "Enable Data Usage"){: caption="Enable Data Usage" caption-side="bottom"}


After you enable data usage metrics, it can take up to two hours to see metrics.
{: note}


## Enabling the alerts metric
{: #data-usage-enable-metrics-alerts}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Person** icon ![Person icon](/icons/preferences.png "Person icon").

    ![Preferences](/images/preferences-1.png "Preferences"){: caption="Preferences" caption-side="bottom"}

3. Select **Preferences**.

4. In the *Alerts* section, enable the toggle to create a [gauge-type](/docs/cloud-logs?topic=cloud-logs-widget_gauge) metric called `cx_alerts`.

    ![cx_alerts metrics](/images/cx-alerts-enable.png "cx_alerts metrics"){: caption="cx_alerts metrics" caption-side="bottom"}



If enabled, the metric is generated whenever an alert is triggered or resolved.
{: note}

You can add this metric to [custom dashboards](/docs/cloud-logs?topic=cloud-logs-create_dashboards).
