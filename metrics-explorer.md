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

## Explore metric labels and values
{: #metrics-explorer-2}

Before running a query, you can use Browse Metric Labels and Values to browse available metrics, labels, and label values—and generate a starting PromQL query without prior knowledge of the metric structure.

## Visualize results
{: #metrics-explorer-3}

After running a query, Metric Explorer displays results in the Query over time chart and a table.

The chart shows each series as a color-coded line. Hover over any timestamp to see the exact values for each series at that moment. Use the legend to identify or toggle individual series.

The table lists each series with:

- Trend — a trend line showing the shape of each series over the selected period.
- Label columns — the label dimensions that differentiate each series.
- Last value — the most recent recorded value for the series.

Select a column header to sort the table.

Use Search series to filter rows by label value.

You can interact with the table and chart by hovering or selecting a row in the table, which highlights the corresponding series in the chart.

## Drill down by label dimensions
{: #metrics-explorer-4}

Select any row in the table to open the *Drill-down by label dimensions* panel. Use it to understand how the selected series distributes across all available label dimensions—without writing additional queries.

The panel applies the selected series value as a filter to the query and shows a grid of subseries charts—a chart per available label. Each chart displays all values for that label as separate series, so you can compare behavior across dimensions.

To control which labels appear in the grid, use Labels to explore in the panel. You can add or remove labels, with up to 30 labels visible at a time.

Select **Update main screen** to apply the current drilldown selections back to the main query view.
