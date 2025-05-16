---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-16"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Query Builder
{: #widget_query_bulder}

Using the Query Builder, you can build queries for your custom {{site.data.keyword.logs_full}} dashboards widgets without needing to know the DataPrime, Lucene, or PromQL syntax.
{: shortdesc}

When you define your widget, you can select if you want to use **Builder** or **Query** mode.

## Metrics-based queries
{: #qb_metrics}

When you build a widget that uses metrics, select **Builder** mode and then **Metrics** as your source.

### Query type
{: #qb_metrics_type}

For the query type, select either an *instant* or *range* query. The query is run over a specific time frame that is defined by the dashboard time picker or the widget time frame.

* *Instant query mode* displays the metric's value at a single point in time, specifically at the end timestamp of the selected time frame. *Instant query mode* is ideal for real-time monitoring, providing a snapshot of data at the moment of visualization. It is also more performant, retrieving only the most recent data point without fetching the entire dataset.

* *Range query mode* retrieves and aggregates metric data over a specified time frame. It returns all data points between the start and end timestamps that match your query. As the time frame changes, the system automatically adjusts the interval to optimize the number of data points displayed in the graph. *Range query mode* is best used for identifying trends or evaluating performance over a defined period.

### Metric name
{: #qb_metrics_name}

Choose your preferred metric from the drop-down menu that is dynamically filled with available metrics. You can use the autocomplete capability to explore the metric name, labels, and values.

### Filters
{: #qb_metrics_filters}

To add a filter, click the **+**. Choose a metric label and an associated value to filter your metric.

Select the `=` or `!=` operator from the drop-down menu to include or exclude one or more values. By using the `=~` or `!~` operators, you can input a RegEx expression.

To add more label-value pairs, click the **+** to add a line.

### Functions
{: #qb_metrics_functions}

By selecting metrics and labels create a valid Prometheus query, but you can also create more complex queries by using functions.

To add a function, click **+**. Select between `aggregation`, `count`, and `rollup` functions.

*Aggregation* functions calculate a set of values and return a single value. These functions include `SUM()`, `AVG()`, `MIN()`, `MAX()`, `COUNT()`, and others. After you choose the function, select the label to aggregate in the drop-down menu or enter a label value.

| Aggregation | Description |
|-------------|-------------|
| `average` |	The average value of all data points within the selected time range. |
| `count` |	The total number of data points within the selected time range. |
| `min` |	The smallest value among the data points within the selected time range. |
| `max` |	The largest value among the data points within the selected time range. |
| `sum` |	The sum of all data points within the selected time range. |
| `quantile` |	The `quantile(phi, q) by (group_labels)` function is an aggregate that computes the `phi-quantile` for each group of labels within the time series that is returned by `q`. The value of `phi` must fall within the range `[0...1]`. The quantile is calculated separately for each set of points with the same timestamp. |
| `histogram_quantile` | The `histogram_quantile` function is a transformation function that computes the `phi-percentile` based on the provided histogram buckets. The value of `phi` must be between `[0...1]`. For example, `histogram_quantile(0.5, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))` returns the median request duration for all requests in the last 5 minutes.|
{: caption="Aggregation functions" caption-side="bottom"}


*Count* functions run calculations on a set of values and return a single value. These functions include `Count()`, `Absent()`, `Absent over time()`, `Present over time()`, `Changes()`, `Resets()`, and others.

| Count |	Description |
|-------|-------------|
| `count` |	The total number of data points within the selected time range. |
| `absent` | Returns 1 if time series has no points. Otherwise, it returns an empty result. |
| `absent over time` | Returns 1 if the provided time range does not contain raw samples. |
| `present over time` |	Returns 1 if there is at least a single raw sample in the provided time range. |
| `changes` |	The number of times that the time series value changed within the provided time range. |
| `resets` | The number of counter resets within the provided time range. |
{: caption="Count functions" caption-side="bottom"}

A *rollup* function refers to functions that aggregate time series data over a specified time range. These functions compute metrics such as `average (avg_over_time)`, `sum (sum_over_time)`, `minimum (min_over_time)`, `maximum (max_over_time)`, `count (count_over_time)`, and `quantiles (quantile_over_time)` over a window of time. They are used to summarize and analyze metric data.

| Rollup | Description |
|--------|-------------|
| `average over time` |	Computes the average of time series values over a time range. |
| `max over time` |	Finds the maximum value of time series data over a time range. |
| `min over time` |	Determines the minimum value of time series data over a time range. |
| `sum over time` |	Calculates the sum of time series values over a time range. |
| `count over time` |	Counts the number of non-`NaN` elements in the time series over a time range. |
| `quantile over time` | Computes the specified quantile of time series data over a time range. |
{: caption="Rollup functions" caption-side="bottom"}

After you choose the function, select the range to be queried as a number or `${__range}`. `${__range}` represents the duration of the dashboard time range. It is rendered as an interval string supported by PromQL. For example, if you select a time range from `13.00` to `14.30`, the `${__range}` variable is rendered as `90m`.

With *rank* functions you can sort, rank, and filter data within your queries. You can use them to refine your results based on specific metrics and values.

To add a rank function, click **+** and choose from `TOPK`, `SORT`, or `SORT Descending`. After you select a rank function, configure it by specifying the metric and parameters (for example, populate the number of `K` results you would like the query to retrieve for `TOPK`).

| Rank | Description |
|------|-------------|
| `TOPK` | Retrieves the highest `K` results from a dataset based on a specified metric. Use `TOPK` to show the highest-ranking data points. |
| `SORT` | Orders the data in ascending order based on the selected metric. Use `SORT` to organize data from the smallest to the largest value. |
| `SORT Descending` | Orders data in descending order based on the selected metric. Use `SORT Descending` to prioritize the largest values at the beginning of the result set. |
{: caption="Rank functions" caption-side="bottom"}


## Log-based queries
{: #qb_logs}

With the log-based Query Builder, you can create complex queries by crafting Lucene-based queries and then adding filters and functions.

When you build a widget that uses logs, select **Builder** mode and then **Logs** as your source.

You also need to choose if you are querying logs in the {{site.data.keyword.frequent-search}} or {{site.data.keyword.monitoring}} data pipeline.


### Filters
{: #qb_logs_filters}

To add a filter, click **+**. Choose a label and an associated value.

Select the `=` or `!=` operator from the drop-down menu to include or exclude one or more values. By using the `=~` or `!~` operators, you can input a RegEx expression.

To add more label-value pairs, click the **+**.

### Functions
{: #qb_logs_functions}

To add a function, click **+**. Select an aggregated value by using a function.

| Function | Description |
|----------|--------------|
| `Count` |	The total number of data points within the selected time range. |
| `Count Distinct` | The number of unique data points within the selected time range. |
| `Sum` |	The sum of all data points within the selected time range. |
| `Min` |	The smallest value among the data points within the selected time range. |
| `Max` |	The largest value among the data points within the selected time range. |
| `Average` |	The average value of all data points within the selected time range. |
| `Percentile XX`	| Represents the value where less than `XX`% of the data points fall. For example, `Percentile 95` is the value where less than `95%` of data points fall.|
{: caption="Logs functions" caption-side="bottom"}

With *Group by*, you can group query results by one or more fields.


## DataPrime queries
{: #qb_dp}

You can create a DataPrime query as the basis for your widget.

You need to choose if you are querying logs in the {{site.data.keyword.frequent-search}} or {{site.data.keyword.monitoring}} data pipeline.



When you create a query based on log data, you have the option of converting the query to the DataPrime syntax language by clicking **Convert to DataPrime** in the Query Builder.

When converted, the transformed query appears under the **DataPrime** tab in the Query Builder.

After you change data sources, or convert your query to DataPrime, your original query parameters in the Query Builder will be lost. Saving your widget preserves the most recent state of the widget.
{: important}

## Widget time
{: #qb_time}

The dashboard's time picker sets the default time frame for your query. To customize the time frame for the widget you are configuring, click **Widget time** and switch the toggle to off to unlink it from the dashboard’s time frame. You can then choose a standard or custom time frame specifically for the widget you are configuring.
