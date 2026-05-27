---

Copyright:
  years:  2024, 2026
lastupdated: "2026-05-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Working with the Metrics Data explorer
{: #metrics-explorer-r114}

In {{site.data.keyword.logs_full_notm}}, you can use the **Metrics Data explorer** to identify high-volume or high-cardinality metrics, understand ingestion patterns, detect inefficient time series, and optimize the data pipeline. You can drill down further and see how individual label values affect the number of generated series.
{: shortdesc}

For example, by understanding which values generate the most series, you can decide whether to adjust label usage, remove unnecessary dimensions, or change metric design.

The Metrics Data explorer works with pre-aggregated statistics that are updated from the ingestion pipeline. Variations, labels, and trends reflect real-time ingestion data.

In the Metrics Data explorer, you can only analyze one day at a time, not a range of days.
{: note}


## Prerequisites
{: #metrics-explorer-r114-prereqs}

To configure this feature, you must attach a metrics bucket to your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Configuring the metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
{: attention}


## Launching the Metrics Data Usage explorer
{: #metrics-explorer-r114-launch}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Usage icon](/icons/usage.svg "Usage") > **Metrics Data**.

    The *Metrics Data* page opens.

    ![Metrics Data Usage analysis](/images/metrics-usage-explorer.png "Metrics Data Usage analysis"){: caption="Metrics Data Usage analysis" caption-side="bottom"}

3.  In the *Usage Analysis* tab, use the sub-tabs to explore metrics, labels, queries, and blocked metrics.

    Select **Metrics** to visualize ingested metrics including usage, cardinality, and samples.

    Select **Labels** to see all labels that are attached to metrics.

    Select **Queries** to show query patterns and usage across metrics.

    Select **Blocked** to see metrics that are blocked from ingestion.

## Launching the Metrics Data Fair Usage limits
{: #metrics-explorer-r114-launch-fairusage}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Usage icon](/icons/usage.svg "Usage") > **Metrics Data**.

    The *Metrics Data > Fair usage limits* page opens.

3.  In the *Fair Usage Limits* tab, check information about the metrics limits, the ingestion limits, and the query limits.


## Exploring the Usage Analysis tab
{: #metrics-explorer-r114-1}

### Metrics view
{: #metrics-explorer-r114-1-metrics}

Select the **Metrics** tab in the *Usage Analysis* page.

Use this view to detect metrics that are heavily influenced by the chosen label or that have excessive label variations.
{: note}

At the top-level, you can find charts that summarize metrics ingestion and trends for the selected time range. Use these charts to understand how your metric volume and cardinality change over time:

- The *Total samples* chart that shows the metric data points that are ingested in the selected time range.

    Use this chart to spot ingestion spikes or drops that might indicate deployment issues, misconfigured scrapers, or unexpected increases in data volume.

- The *Total Cardinality* chart shows unique time series in the selected time range.

    Use this chart to detect sudden growth in time-series count, often caused by new labels, unexpected label values, or high-cardinality dimensions such as pod_name or operation.

These charts help you correlate ingestion patterns, identify high-impact changes quickly, and prioritize where to reduce cardinality or remove unnecessary variations.

The Metrics view shows how the selected label is used across different metrics. For each metric, you can view the following information:
* In the **Volume** column, you can see the volume of metrics.
* In the **% Volume** column, you can see the fraction of total metrics volume.
* In the **Samples** column, you can see the number of data points collected.
* In the **% Samples** column, you can see the fraction of data points collected.
* In the **Dimensions** column, you can see the count of unique label names.
* In the **Variations** column, you can see the count of unique variations. A variation represents the unique label combinations for a metric.
* In the **Cardinality** column, you can see the count of unique time series.
* In the **% Cardinality** column, you can see the fraction of total series cardinality.
* In the **Last Ingested** column, you can see the timestamp of the latest ingestion for that metric.
* In the **Status** column, you can see whether the metric is active or disabled.
* In the **Action** column, you can see whether the metric is blocked.

When you click on a metric, a page opens with detailed information about the metric.

![Metrics view](/images/metrics-view.png "Metrics view"){: caption="Metrics view" caption-side="bottom"}



### Labels view
{: #metrics-explorer-r114-1-labels}

Select the **Labels** tab in the *Usage Analysis* page.

Use this view to analyze how a specific label contributes to metric usage, variation, and value diversity.
{: note}

You can use the Labels tab to analyze label-level impact on storage and cardinality, for example:
* List all labels attached to the metric
* Show each label's usage, cardinality, and unique value count
* Highlight labels driving high series counts

Watch for labels with many unique values such as pod_name or operation. They often inflate cost.
{: note}

- You can select a label to display detailed information such as the metrics that have that label.

- If you select **Live values**, you can see the list of values identified for the chosen label in the selected time range.

- You can review the table to compare values and identify which ones generate the most variations. This helps determine whether specific label values are responsible for cardinality growth and where to focus optimization efforts.


### Query analyzer
{: #metrics-explorer-r114-1-query}

Select the **Queries** tab in the *Usage Analysis* page.

Use the Query Analyzer to gain insight into how metrics are used across your environment, explore query patterns, and track usage frequency. Use it periodically to identify query patterns across different sources in one place, along with their usage and success rates, to help clean up unused metrics.
{: note}

For example, you can use the Query Analyzer to:
- Identify high-value metrics versus rarely used or unused ones.
- Detect redundant queries that increase cost or cardinality.
- Understand which dashboards, alerts, or APIs use a given metric.
- Correlate high-usage queries with ingestion data for cost analysis.
- Before removing a metric, verify that no critical dashboards or alerts depend on it.


Consider the following information:
* Supports PromQL queries only.
* Location shows where a mmetric is being used and queries.
* Can only analyze one day at a time, not a range of days.


![Metrics Usage explorer](/images/metrics-usage-query.png "Metrics Usage explorer"){: caption="Metrics Usage explorer" caption-side="bottom"}

In this tab, you can view the following information:

- `Query pattern`: Normalizes queries by replacing variable values with $var to group similar queries and reduce label noise.
- `# Times used`: Displays the number of times each query pattern has run on the selected date.
- `Status`: Shows success and failure percentages for query executions, helping identify errors or invalid queries.
- `Location`: Lists the source of the query, such as a Dashboard, alerts.
- `Date selection`: View query activity for a specific date using the date selector.

You can filter query patterns by keyword or location.

Consider the following information when you interpret the data:
- When the value of `# Times used` is high, the metric is actively queried and likely important. Keep the metrics and monitor its performance.
- When the `# Times used` is low or zero, the metric is rarely or never used. Review dashboards and alerts to confirm whether you can drop the metric.
- When the `# Times used` for a Frequent location such as Alerts is high, the metric is operationally critical.	Prioritize retention and optimization.
- WWhen the `# Times used` for a Frequent location such as Alerts is low, you might be able to drop this metrics. Investigate label usage and aggregation strategies.

## Exploring the Fair usage limits tab
{: #metrics-explorer-r114-2}

Select the **Metrics** tab in the *Usage Analysis* page.

Use the Fair Usage Limits view to provide transparency, predictability, and control over platform usage. By defining clear thresholds, offering real-time monitoring, and providing actionable insights, this feature ensures a balanced allocation of resources while maintaining system performance and reliability.

When usage approaches or exceeds defined limits, the platform offers guidance on adjustments, helping users refine workflows and improve data efficiency. This ensures a seamless experience while maintaining fair access to resources for all users.

Use Fair Usage Limits to:

- Achieve greater transparency, ensuring your team has clear visibility into system thresholds
- Understand when limits have been reached and take action to prevent recurrence
- Improve reliability and predictability across your platform performance
