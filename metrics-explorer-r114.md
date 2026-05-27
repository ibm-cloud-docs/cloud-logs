---

Copyright:
  years:  2024, 2026
lastupdated: "2026-05-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Working with the Metrics explorer
{: #metrics-explorer-r114}

In {{site.data.keyword.logs_full_notm}}, you can use the **Metrics explorer** to gain insights into metrics, volumes, cardinality and dimensions. For example, you can use the Metrics explorer page to identify which label values contribute most to a metric's cardinality. While other views show the total number of time series or label combinations, this tab allows you to drill down further and see how individual label values affect the number of generated series.

For example, by understanding which values generate the most series, you can decide whether to adjust label usage, remove unnecessary dimensions, or change metric design.

In the Metrics Explorer, you can only analyze one day at a time, not a range of days.
{: note}


## Prerequisites
{: #metrics-explorer-r114-prereqs}

To configure this feature, you must attach a metrics bucket to your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Configuring the metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
{: attention}


## Launching the Metrics Explorer
{: #metrics-explorer-r114-launch}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Usage icon](/icons/usage.svg "Usage") > **Metrics Usage**.

    The *Metrics Usage* page opens.

    ![Metrics Usage explorer](/images/metrics-usage-explorer.png "Metrics Usage explorer"){: caption="Metrics Usage explorer" caption-side="bottom"}

3.  Use the sub-tabs to explore metrics, labels, queries, and blicked metrics.

    Select **Metrics** to visualize ingested metrics including usage, cardinality, and samples.

    Select **Labels** to see all labels that are attached to metrics.

    Select **Queries** to show query patterns and usage across metrics.

    Select **Blocked** to see metrics that are blocked from ingestion.



## Exploring the Usage analysis tab
{: #metrics-explorer-r114-1}

### Metrics view
{: #metrics-explorer-r114-1-metrics}

Use this view to detect metrics that are heavily influenced by the chosen label or that have excessive label variations.
{: note}

At the top-level, you can find charts that summarize metrics ingestion and trends for the selected time range. Use these charts to understand how your metric volume and cardinality change over time:

- The *Total samples chart* shows how many metric data points are ingested.

    Use this chart to spot ingestion spikes or drops that might indicate deployment issues, misconfigured scrapers, or unexpected increases in data volume.

- The *Total cardinality chart* shows how many unique time series are generated.

    Use this chart to detect sudden growth in time-series count, often caused by new labels, unexpected label values, or high-cardinality dimensions such as pod_name or operation.

These charts help you correlate ingestion patterns, identify high-impact changes quickly, and prioritize where to reduce cardinality or remove unnecessary variations.


The Metrics view shows how the selected label is used across different metrics.

For each metric, you can view the following information:
* In the **Usage** column,  you can see the data volume attributed to the label.
* In the **% Usage** column, you can see the relative share of total usage.
* In the **Samples** column, you can see the number of data points collected.
* In the **Dimensions** column, you can see the unique label keys.
* In the **Variations** column, you can see the unique combinations of label keys.
* In the **Cardinality** column, you can see the unique time series per metric.
* In the **% Cardinality** column, you can see the share of total series cardinality.
* In the **Last Ingested** column, you can see the timestamp of the latest ingestion for that metric.
* In the **Status** column, you can see whether the metric is active or disabled.
* In the **Action** column, you can see whether the metric is blocked.


### Labels view
{: #metrics-explorer-r114-1-labels}

Use this view to understand which metrics and label values drive data volume and cardinality.
{: note}

The Labels tab analyzes label-level impact on storage and cardinality. Use it to analyze how a specific label contributes to metric usage, variation, and value diversity.

* Lists all labels attached to the metric
* Shows each label's usage, cardinality, and unique value count
* Highlights labels driving high series counts

Watch for labels with many unique values such as pod_name or operation; they often inflate cost.
{: note}

- You can select a label to display the available values for that label.

    Select a label associated with the metric. The label selector lists all labels detected for the metric. Once selected, the interface displays the available values for that label.

- You can select 1 or more label values to compare how different values contribute to the total number of time series.

    Select one or more label values to analyze.

    The values panel displays the values associated with the selected label.

    You can select up to 40 values at a time.

- You can review the cardinality table to compare values and identify which ones generate the most time series. This helps determine whether specific label values are responsible for cardinality growth and where to focus optimization efforts.

    The table displays the results for each selected value, showing:

    * Value: The label value
    * Series: The number of unique time series that are generated
    * Samples: The number of samples associated with those time series


### Query analyzer
{: #metrics-explorer-r114-1-query}

Use the Query Analyzer to gain insight into how metrics are used across your observability environment and explore query patterns, and track usage frequency.
{: note}

For example, you can use the Query Analyzer to:
- Identify high-value metrics versus rarely used or unused ones.
- Detect redundant queries that increase cost or cardinality.
- Understand which dashboards, alerts, or APIs use a given metric.
- Correlate high-usage queries with ingestion data for cost analysis.
- Before removing a metric, verify that no critical dashboards or alerts depend on it.

Use Query Usage Analyzer periodically to identify query patterns across different sources in one place, along with their usage and success rates, to help clean up unused metrics.


Consider the following information:
* Supports PromQL queries only.
* Client context (for example, Dashboard, API, Alert) might not appear in all cases.
* Can only analyze one day at a time, not a range of days.


![Metrics Usage explorer](/images/metrics-usage-query.png "Metrics Usage explorer"){: caption="Metrics Usage explorer" caption-side="bottom"}


## Exploring the Fair usage limits tab
{: #metrics-explorer-r114-2}

Use the Fair Usage Limits view to provide transparency, predictability, and control over platform usage. By defining clear thresholds, offering real-time monitoring, and providing actionable insights, this feature ensures a balanced allocation of resources while maintaining system performance and reliability.

When usage approaches or exceeds defined limits, the platform offers guidance on adjustments, helping users refine workflows and improve data efficiency. This ensures a seamless experience while maintaining fair access to resources for all users.

Use Fair Usage Limits to:

- Achieve greater transparency, ensuring your team has clear visibility into system thresholds
- Understand when limits have been reached and take action to prevent recurrence
- Improve reliability and predictability across your platform performance
