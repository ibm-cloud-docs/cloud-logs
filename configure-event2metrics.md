---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-22"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring collection of metrics from logs
{: #configure-event2metrics}

In {{site.data.keyword.logs_full}}, you can generate metrics from {{site.data.keyword.frequent-search}} logs and {{site.data.keyword.monitoring}} logs.
{: shortdesc}

When you define metrics from logs, consider the following information:
- Metrics are collected from the point in time in which they were defined.
- You can create up to 30 metric rules.
- You can set the retention period to any length. You manage the metrics bucket and you can retain the data for as long as you need.
- You have a quota of 10M total metric permutations per day.
- Your maximum query time range for your Events2Metrics indices is 90 days.


## Prerequisites
{: #event2metrics-prereq}

Before you can define metrics from logs, check the following requirements:

- You must have a [metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket) configured for your {{site.data.keyword.logs_full_notm}} instance. 

   If you do not have a metrics bucket configured, the following message will be issued and Events to Metrics data is only available for a few hours.

   ```text
   WARNING - Metric Bucket is Missing
   To extend the retention period of your metric data beyond a few hours, it is essential to
   configure a metric bucket. Without this configuration, your data may be automatically purged
   after a short time frame, resulting in potential data loss.
   ```
   {: screen}

- You can only define metrics for {{site.data.keyword.frequent-search}} logs and {{site.data.keyword.monitoring}} logs.


## Configuring Events to Metrics
{: #configure-event2metrics-steps}

Do the following to configure Events to Metrics in your environment.


{{site.data.content.launch-ui}}

2. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Events to Metrics**.

3. Click **New Events2Metrics**.

4. Define the details for your metrics.

   For **Name**, specify the name for the metric that will be used in the long-term index.

   For **Description**, describe your metric.

4. Select your **Event Source**. Only **Logs** is supported.

5. In the *Query* section, you can use a text or Lucene query. Enter the [query](#event2metrics-query) to select the logs for your metric.

6. For **Scope**, you can filter logs by applications, subsystems, or severity.

7. (Optional) Define the metrics field to extract data based on `max`, `min`, `count`, `average`, or aggregation (`histogram` or `samples`).

   * Define up to 10 fields for which the metrics will be collected.

   * For each metric, you can define an aggregation function that aggregates the stream of data.

   * A `histogram` bucket is a range of values within a histogram. When you create a histogram you specify the value ranges that will be used to group the data. Each bucket in the histogram represents the number of observations that fall within the range of values for the bucket.  Granular buckets provide more accurate percentiles during querying, but increase the number of time series and storage.

   * When selecting `histogram` aggregation, you need to provide the buckets that represent the distribution of the data. For example, a CPU metric histogram could be `0, 10, 30, 45, 50, 60, 70, 85, 90, 100`. Values are specified as a comma-separated list.

   * You can use the `sample` aggregation to collect 4 samples a minute with each sample representing a quarter of a minute. When data is received within the same quarter, the minimum or maximum of the data is kept. You must define whether to collect the minimum or the maximum value per sample collected.

8. Define the labels to use for the visualization.  You can create up to 6 labels.

9. Select the maximum number of metrics permutations that are allowed for a metric. Note the following:

   * Each environment is limited to 10M metric permutation a day.
   * Each metric rule has a permutation quota.
   * Metric rules are blocked when a specific or organization quota is met.
   * A graph is displayed estimating the results for high priority logs based on the prior 7-days of logging. You can use this information to determine the maximum number of permutations that you want to configure. You want to choose a number of permutations that are high enough for average daily data, but not so high as to affect your daily quota.


## Default metric
{: #configure-event2metrics-default}

A default metric is created for each metric defined in Events to Metrics. This metric counts the total number of logs matching the query and the configured scope.  The metric name is `<Metric Name>_cx_docs_total` and can be queried the same as any other metric. The default metric can be grouped with labels as well.

## Configuring Events to Metrics queries
{: #event2metrics-query}

The query used to configure Events to Metrics can be simple or complex. 

### Free text queries
{: #e2m-query-freetext}

Enter a text string to define a search on free text.

For example, to find all `response_code 200` strings in GET requests, enter `GET 200`. This query will find logs containing the strings `200` and `GET`.

### Phrase queries
{: #e2m-query-phrase}

Enter the phrase in double quotation marks to define a search matching a specific phrase.

For example, `"GET 200"` will only match lines containing that exact string.

### Field queries
{: #e2m-query-field}

Prefix the field name before the value to define a search for a value in a specific field.

For example, `environment:production` will search for the value `production` in the `environment` field.

### Numeric range queries
{: #e2m-query-range}

Specify the range of numeric values in bracket(`[START_VALUE TO END_VALUE]`) to search for a range of values.

For example, to search for all lines with a 4xx status code in the `status` field, specify `status.numeric:[400 TO 499]`.

### Complex queries
{: #e2m-query-complex}

You can use regular expressions in your searches. Regex must be wrapped in `/` characters. 

For example, to search for all EU regions you can specify `region:keyword:/eu-(fr|es)/`

You can also use the boolean operators `AND`, `OR`, and `NOT`. 

For example, to define a search for lines with a 4xx status code and and extension of `php`, specify `status.numeric[400 TO 499] AND extension.php`.

Another example is to search for all lines from the production environment with status codes of 4xx not originating in the EU regions.

```text
environment:production AND status.numeric:[400 TO 499] NOT region:/region:/eu-(fr|es)/
```
{: codeblock}

### Using keywords in JSON structured logs
{: #e2m-query-keyword}

You can add the `.keyword` suffix to a field name to query data without indexing so that `key.keyword:/first-name*/` will return the log `"Key":"first-name: John"` and also `"Key":"first-name: Bob"`, but won't return the log `"Key":"The first participant's name is John"` since it looks to match the exact phrase `first-name`.

You need to use forward slash (`/`) before and after your regex string.
{: important}

Keywords are not created for fields longer than 256 characters.
{: restriction}
