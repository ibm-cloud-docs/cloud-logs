---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-04"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Using the Metrics Usage Analyzer
{: #metrics-usage-analyzer}

In {{site.data.keyword.logs_full_notm}}, you can use the *Metrics Usage Analyzer* to gain insights into systems health, performance trends, and capacity planning.
{: shortdesc}

In the *Metrics Usage Analyzer*, you can monitor metrics:
- Identify high-volume metrics
- Identify high-cardinality metrics
- Understand data ingestion patterns
- Identify inefficient time series
in the *Metric usage* tab.


## Launching the Metrics Usage Analyzer
{: #metrics-usage-analyzer-launch}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Usage icon](/icons/usage.svg "Usage") > **Data Usage**.

    The *Data Usage* page opens.

    ![Data Usage](/images/data-usage.png "Data Usage"){: caption="Data Usage" caption-side="bottom"}

3. Configure the time selector. You can choose **Quick** to choose a preset or **Custom** to set a custom date and time range to view and compare usage across any timeframe.

    ![Data Usage time selector](/images/data-usage-timepicker.png "Data Usage time selector"){: caption="Data Usage time selector" caption-side="bottom"}

4. Select the **Metric usage** tab.


## Filtering options
{: #metrics-usage-analyzer-filter}

You can filter data by choosing one or more options in **Filtered by**:

- Priority: Defines the TCO data pipeline associated with the logs. Valid values are: `Medium` and `Blocked`.
- cx_source: Defines the type of source. Valid values are: `user`, `system`, `event2metrics`, and `recordingrules`.


## Aggregation options
{: #metrics-usage-analyzer-agg}

You can aggregate data by choosing one or more options in **Group data by**:
- Priority: Defines the TCO data pipeline associated with the metrics. Valid values are: `Medium` and `Blocked`.
- cx_source: Defines the type of source. Valid values are: `user`, `system`, `event2metrics`, and `recordingrules`.


## Viewing data
{: #metrics-usage-analyzer-data}

You can view information about metric volumes in the following widgets:
- Total : Shows how many metric data points were ingested. Use this chart to spot ingestion spikes or drops that might indicate deployment issues, misconfigured scrapers, or unexpected increases in data volume.
- Max daily usage
- Min daily usage
- Avg daily usage

In the *Metrics breakdown* section, you can monitor volumes of metrics based on the filtering and group by options selected.

![Metrics breakdown](/images/metrics-breakdown.png "Metrics breakdown"){: caption="Metrics breakdown" caption-side="bottom"}
