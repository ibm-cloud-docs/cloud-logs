---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Visual Explorer
{: #visual-explorer}

The {{site.data.keyword.logs_full}} Visual Explorer is a powerful tool that integrates a multifunctional display with customizable dashboard widgets. Visual Explorer provides a fast way to add query-based graphs without needing to set up custom dashboards. You can run multiple queries from different data sources so they are be displayed side by side on the same page, making it easier to correlate data and providing a more comprehensive view of your system.
{: shortdesc}

Instead of manually sifting through raw logs or metrics data, you can quickly pinpoint the source of issues that use log patterns and visual indicators. The ad hoc visualizations can be created by using a simplified query builder or by using query languages such as DataPrime, Lucene, or PromQL.



## Building queries
{: #ve-build}

By using the Visual Explorer, you can build queries for your widgets without having to know the exact DataPrime, Lucene, or PromQL syntax for the query.

Query building functions include:

* The ability to select logs or metrics as data sources.

* Easily creating DataPrime queries by using the *Convert to DataPrime* function.

* Adding filters to your queries to narrow down results based on specific attributes or categories, making it easier to find relevant data.

* Add functions to enhance your queries. For example,

    * Grouping query results by a label for a more granular view.

    * Aggregating sets of values to return a single value. Functions include `SUM()`, `AVG()`, `MIN()`, `MAX()`, `COUNT()`, and more.

Up to 4 queries with dedicated attributes can be created on a single Visual Explorer page. You can then add new graphs, or duplicate an existing graph with all its settings and configurations.

## Using the Visual Explorer
{: #ve-use}

Access the Visual Explorer by doing the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the Logs icon ![Logs icon](/icons/explore.svg "Explore logs") > **Visual Explorer**.

4. In **Query**, configure your query.

    * In **Query Name**, give your query a meaningful name.

    * Choose a **data source** (`Logs`, `Metrics`, or `DataPrime`) for the query.

        If you create a Logs query, you can convert it to the DataPrime syntax language by clicking **Convert to DataPrime**.
        {: tip}

5. When you create a Metrics query, choose the metric to be queried from the menu of available metrics.

You can create up to 4 query charts on a single Visual Explorer page. To create another query, click **+**. To duplicate an existing query, click the **Duplicate query** icon.

A query chart can be deleted from the Visual Explorer page. The action is permanent and cannot be undone.

### Switching visualizations
{: #ve-switch}

You can easily switch chart visualizations without re-creating the widgets. By switching chart types you can explore data in different ways with the same query.

Use the menu to toggle between the different available views.

### Saving as a dashboard
{: #ve-save}

While Visual Explorer charts are temporary, you can save them as [custom dashboards](/docs/cloud-logs?topic=cloud-logs-create_dashboards) for future reference to share with your team.

To save the chart as a dashboard:

1. Click **Save As Dashboard**.

2. Give the dashboard a meaningful name.

3. Click **Save**.

## Logs queries
{: #ve-logs}

### Logs data pipeline
{: #ve-logs-dp}

For log queries you can select {{site.data.keyword.frequent-search}} or All Logs for the data pipeline.

### Logs filters
{: #ve-logs-filters}

You can add a filter by selecting a label and an associated value.

The `=` and `!=` operators include or exclude one or more values.

Add more filters by clicking **+**.

### Logs functions
{: #ve-logs-functions}

The following functions are available to aggregate log data:

| Function | Description |
|----------|-------------|
| `Count` |	The total number of data points within the selected time range.|
| `Count Distinct` | The number of unique data points within the selected time range. |
| `Sum` |	The sum of all data points within the selected time range. |
| `Min` |	The smallest value among the data points within the selected time range. |
| `Max` |	The largest value among the data points within the selected time range. |
| `Average` |	The average value of all data points within the selected time range. |
| `Percentile XX` |	`Percentile xx` represents the value under which XX% of the data points fall. For example, `Percentile 95` is the value under which 95% of data points fall. |
{: caption="Log functions" caption-side="bottom"}

You can also use `Group by` to group query results by one or more fields.

### DataPrime queries
{: #ve-dp}

You can also create a DataPrime query for your widget. The default view includes a log-based line chart widget with a DataPrime query (`source logs | groupby $m.timestamp / 1m as timestamp agg count() as count`). This query retrieves logs, groups them into 1-minute intervals based on their timestamp, and then counts how many log entries appear in each of those 1-minute intervals.

## Metrics queries
{: #ve-metrics}

When you use metrics as your data source, you can use one of two modes: **Builder** and **Query**. In **Query** mode, specify a PromQL query. In **Builder** mode, you build a query by selecting options without having to understand the PromQL syntax.

### Metrics filters
{: #ve-metrics-filters}

You can add a filter by selecting a label and an associated value.

The `=` and `!=` operators include or exclude one or more values.

Add more filters by clicking **+**.

### Metrics functions
{: #ve-metrics-functions}

Selecting metrics and labels builds a valid PromQL query, but you can create more complex queries by using functions.

#### Aggregation
{: #ve-metrics-aggregation}

Aggregation functions calculate a set of values and return a single value. After you choose the function, select the label to aggregate in the menu or enter the label.

| Function | Description |
|-------------|-------------|
| `average` |	The average value of all data points within the selected time range. |
| `count` |	The total number of data points within the selected time range. |
| `min` |	The smallest value among the data points within the selected time range. |
| `max` |	The largest value among the data points within the selected time range. |
| `sum`	 | The sum of all data points within the selected time range. |
| `quantile`	| The `quantile(phi, q) by (group_labels)` function is an aggregate that computes the phi-quantile for each group of labels within the time series that is returned by `q`. The value of `phi` must fall within the range `[0...1]`. The quantile is calculated separately for each set of points with the same timestamp. This function is supported by PromQL. |
| `histogram_quantile` |	The `histogram_quantile` function is a transformation function that computes the phi-percentile based on the provided histogram buckets. The value of phi must be between `[0...1]`. For example, `histogram_quantile(0.5, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))` returns the median request duration for all requests in the last 5 minutes. |
{: caption="Aggregation functions" caption-side="bottom"}


#### Count
{: #ve-metrics-count}

Count functions run calculations on a set of values and return a single value.

| Function |	Description |
|-------|-------------|
| `count` |	The total number of data points within the selected time range. |
| `absent` |	Returns `1` if the time series has no points. Otherwise, `absent` returns an empty result. |
| `absent over time` |	Returns `1` if the provided time range does not contain raw samples. |
| `present over time` |	Returns `1` if there is at least a single raw sample in the provided time range. |
| `changes` |	The number of times that the time series value changed within the provided time range. |
| `resets` |	The number of counter resets within the provided time range. |
{: caption="Count functions" caption-side="bottom"}

#### Rollup
{: #ve-metrics-rollup}

A rollup function refers to functions that aggregate time series data over a specified time range. They are used to summarize and analyze metric data.

| Function | Description |
|--------|-------------|
| `average over time` |	Computes the average of time series values over a time range. |
| `max over time` |	Finds the maximum value of time series data over a time range. |
| `min over time` |	Determines the minimum value of time series data over a time range. |
| `sum over time` |	Calculates the sum of time series values over a time range. |
| `count over time` |	Counts the number of non-NaN elements in the time series over a time range. |
| `quantile over time` |	Computes the specified quantile of time series data over a time range. |
{: caption="Rollup functions" caption-side="bottom"}

After you choose the function, select the range to be queried as a number or `${__range}`. The variable represents the duration of the dashboard time range. It is an interval string that is supported by PromQL. For example, if you select a time range from `13.00` to `14.30`, the `${__range}` variable is rendered as`90m`. For more information, see [PromQL query variables](/docs/cloud-logs?topic=cloud-logs-variables#variables-promql).

#### Rank
{: #ve-metrics-rank}

Rank functions sort, rank, and filter data within your queries. You can use rank functions to refine your results based on specific metrics and values.

After you select a rank function, configure it by specifying the metric and parameters (for example, populate the number of `K` results you would want the query to retrieve for `TOPK`).

| Function | Description |
|------|-------------|
| `TOPK`	| Retrieves the highest `K` results from a dataset based on a specified metric. Use `TOPK` to show the highest-ranking data points. |
| `SORT`	| Orders data in ascending order based on the selected metric. Use `SORT` to organize data from the smallest to the largest value. |
| `SORT Descending` |	Orders data in descending order based on the selected metric. Use `SORT Descending` to prioritize the largest values at the beginning of the result set. |
{: caption="Rank functions" caption-side="bottom"}

## Example use case
{: #ve-example}

This example combines two graphs to correlate logs with `Error` and `Critical` severity levels with the memory usage of the host that is running the services.

First, add the logs query:

1. Select `Logs` as the data source.

2. Add the `Group` by `product_id` function.

3. Add a filter for `Severity=Error, Critical`.

Then, add the metrics query:

1. Click **+** to add a query.

2. Select `Metrics` as the data source.

3. Select the `mem_used` metrics.

4. Add the `sum` by `host` function.


