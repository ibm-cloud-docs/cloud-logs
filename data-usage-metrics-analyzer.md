---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Working with the Metrics Usage Analyzer
{: #data-usage-metrics-analyzer}

In {{site.data.keyword.logs_full_notm}}, you can gain insights into metrics usage through the **Data usage > Metrics Usage** tab.
{: shortdesc}

In the *Metrics Usage* tab, you can monitor metrics to:
- Identify high-volume metrics
- Identify high-cardinality metrics
- Understand data ingestion patterns
- Identify inefficient time series



## Launching the Metrics Usage tab
{: #data-usage-metrics-analyzer-launch}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Usage icon](/icons/usage.svg "Usage") > **Data Usage**.

    The *Data Usage* page opens.

    ![Data Usage](/images/data-usage.png "Data Usage"){: caption="Data Usage" caption-side="bottom"}

3. Configure the time selector. You can choose **Quick** to choose a preset or **Custom** to set a custom date and time range to view and compare usage across any timeframe.

    ![Data Usage time selector](/images/data-usage-timepicker.png "Data Usage time selector"){: caption="Data Usage time selector" caption-side="bottom"}

4. Select the **Metric usage** tab.


## Filtering options
{: #data-usage-metrics-analyzer-filter}

You can filter data by **Source** in *Filtered by*.

Valid source values are: `user`, `system`, and `event2metrics`.


## Aggregation options
{: #data-usage-metrics-analyzer-agg}

You can aggregate data by choosing one or more options in **Group data by**:
- Priority: Defines the TCO data pipeline associated with the metrics. Valid values are: `Medium` and `Blocked`.
- Source: Defines the type of source. Valid values are: `user`, `system`, and `event2metrics`.


## Viewing data
{: #data-usage-metrics-analyzer-data}

You can view information about metric volumes in the following widgets:
- Total : Total usage in the selected period. Shows how many metric data points are ingested in the selected period.

    Use this chart to spot ingestion spikes or drops that might indicate deployment issues, misconfigured scrapers, or unexpected increases in data volume.

- *Max daily usage*: Highest daily ingested volume
- *Min daily usage*: Lowest daily ingetsed volume
- *Avg daily usage*: Average daily ingested volume

In the *Metrics breakdown* section, you can monitor volumes of metrics based on the filtering and group by options selected.

![Metrics breakdown](/images/metrics-breakdown.png "Metrics breakdown"){: caption="Metrics breakdown" caption-side="bottom"}
