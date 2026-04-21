---

copyright:
  years:  2024, 2026
lastupdated: "2026-04-21"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Metrics explorer
{: #metrics-explorer}

In {{site.data.keyword.logs_full_notm}}, you can use the metrics explorer to investigate metric behavior, compare series across labels, and surface outliers across your entire label space from a single screen. You can query any Prometheus-compatible metric, visualize the results, and drill down by label dimensions without setting up a dashboard first.
{: shortdesc}

You can browse, search and filter metric time series by name and labels, generate PromQL queries of selected metric time series and create ad-hoc visualizations of selected metric time series and PromQL queries.


## Use cases
{: #metrics-explorer-1}

Use Metric Explorer to:

- Query without a dashboard — Build and run PromQL queries in a dedicated workspace, using a no-code builder or a code editor.
- Visualize and compare — See metric trends as time series charts, filter by labels, apply aggregations, and combine expressions to derive new signals.
- Find what's driving anomalies — Drill down by label dimensions to identify which label values are contributing to unusual behavior, without writing additional queries.

## Launching the Metrics Explorer
{: #metrics-explorer-launch}
{: step}


Complete the following steps to launch the Metrics Explorer:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select **Explore Logs** > **Visual Explorer**.

    ![Visual Explorer](/images/visual-explorer.png "Visual Explorer"){: caption="Visual Explorer" caption-side="bottom"}

3. Select **Query #1 > Open Metric Explorer**

    ![Metric Explorer](/images/metric-explorer.png "Metric Explorer"){: caption="Metric Explorer" caption-side="bottom"}

The Metric Explorer opens.


## Explore metric labels and values
{: #metrics-explorer-2}
{: step}

Before running a query, you can use the *Metric Explorer* section to find metrics that are available, their labels, and label values that you can use to generate a starting PromQL query without prior knowledge of the metric structure.

![Metric Explorer section](/images/metric-explorer-1.png "Metric Explorer section"){: caption="Metric Explorer section" caption-side="bottom"}

## Get insights on a metric
{: #metrics-explorer-3}
{: step}

In the *Metric Analysis* section, you can explore any metric listed in the *Metric Explorer* section.

You can get the following information:
- Trend: A trend line showing the shape of each series over the selected period.
- Label columns: The label dimensions that differentiate each series.
- Last value: The most recent recorded value for the series.

Choose a metric in the *Metric Explorer* section to display results in the Query over time chart and a table.

![Choose a metric](/images/metric-explorer-2.png "Choose a metric"){: caption="Choose a metric" caption-side="bottom"}

The chart shows each series as a color-coded line.
- Hover over the graph to see the exact values for each series at that moment.
- Use the legend to identify or toggle individual series.

![Hover over the graph](/images/metric-explorer-3.png "Hover over the graph"){: caption="Hover over the graph" caption-side="bottom"}

You can select a column header to sort the data in the column.

Use Search series to filter rows by label value.

You can interact with the table and chart by hovering or selecting a row in the table, which highlights the corresponding series in the chart.


## Next
{: #metrics-explorer-4}

After you analyze a metric, you can click **Apply query** and return to visual explorer to reuse the metric query in a dashboard.
