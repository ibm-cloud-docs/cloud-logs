---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-04"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# About Data Usage
{: #data-usage-r114}

In {{site.data.keyword.logs_full_notm}}, you can get detailed insights into your observability data usage through the *Data Usage* page.
{: shortdesc}

- You can view information related to ingested logs through the *User data sent*.
- You can view information related to metrics that are ingested and generated from log data that is ingested.

For example, you can use the information in the Data usage page to:
- Investigate spikes and anomalies in a period of time.
- Run accurate period-over-period comparisons for cost and planning.

The *Data Usage* page includes two sections:
- *User data sent* section: This section reports on the log data that is ingested and collected. For more information, see [Analyzing data usage](/docs/cloud-logs?topic=cloud-logs-data-usage-analyzer).
- *Metric usage* section: This section reports on the metrics that are ingested and generated from log data that is ingested. For more information, see [Analyzing metrics usage](/docs/cloud-logs?topic=cloud-logs-metrics-agent-usage-analyzer).



## Prerequisites
{: #data-usage-prereqs}

To configure this feature, you must attach a metrics bucket to your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Configuring the metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
{: attention}

## Launching the Data Usage page
{: #data-usage-launch}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Data Usage**.

    The *Data Usage* page opens.

    ![Data Usage](/images/data-usage.png "Data Usage"){: caption="Data Usage" caption-side="bottom"}

3. Configure the time selector. You can choose **Quick** to choose a preset or **Custom** to set a custom date and time range to view and compare usage across any timeframe.

    ![Data Usage time selector](/images/data-usage-timepicker.png "Data Usage time selector"){: caption="Data Usage time selector" caption-side="bottom"}


## Launching the Data Usage dashboard
{: #data-usage-dashboard-launch}

From the *Data Usage* page, you can launch the Data Usage dashboard. For more information, see [Data Usage dashboard](/docs-draft/cloud-logs?topic=cloud-logs-data-usage-dashboard&interface=ui).


## Generating reports
{: #data-usage-reports}

From the *Data Usage* page, you can generate and export data usage information. Choose any of the following options:

- [Generating detailed usage reports](/docs/cloud-logs?topic=cloud-logs-data-usage-detailed-reports)
- [Generating data usage overview reports](/docs/cloud-logs?topic=cloud-logs-data-usage-reports)
