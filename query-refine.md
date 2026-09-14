---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Refining query results in {{site.data.keyword.logs_full_notm}}
{: #query-refine}

In {{site.data.keyword.logs_full}}, you can refine a query by adding filters, narrowing timeframes, and using exact matches.
{: shortdesc}

Checklist for refining a query in {{site.data.keyword.logs_full_notm}}:

## Reduce the data resultset by adding filters to a query in {{site.data.keyword.logs_full_notm}}
{: #query-refine-1}
{: step}

Add explicit filter clauses or grep conditions early in your DataPrime Query Assistance or search bar to reduce the working data set before running transformations.

For example, the following sample shows a filter condition before an aggregation expression:

```text
source logs
| filter $d.action == 'create'
| groupby $d.path aggregate count()
```
{: codeblock}

## Reduce the data resultset by using dynamic range variables in widget queries in {{site.data.keyword.logs_full_notm}}
{: #query-refine-2}
{: step}

If you are running a Dataprime query in a widget in a custom dashboard, you can use dynamic range variables (`$p`) to reduce the the working data set before running transformations. For more information, see [Using query parameters in your DataPrime queries in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-query-parameters).


## Narrow the timeframe of a query in {{site.data.keyword.logs_full_notm}}
{: #query-refine-3}
{: step}

Shorten the default time range in the *Explore Logs* page or inside the query code to minimize the volume of data that is scanned.

Querying large time ranges (weeks or months) increases the scan volume and slows down results.

To narrow the timeframe of a query in {{site.data.keyword.logs_full_notm}}:

- Use the time picker to select only what is necessary.

- Use relative time queries.

    Relative time queries are handled via DataPrime time expressions. For example, use `now()` combined with standard time arithmetic and intervals (such as 1h, 15m, or 30s) to filter events dynamically or filter logs that are newer than one hour `($m.timestamp > now() - 1h)`. For more information, see [DataPrime date / time functions](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-date-time-func).

    You can also use dynamic time range variables (`$p`) to automatically respect active dashboard time pickers. For example, you can reference `$p.timeRange.startTime` or `$p.timeRange.endTime` in your queries. For more information, see [Using query parameters in your DataPrime queries in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-query-parameters).

    You can shift the evaluation window backward inside specific Dataprime commands to analyze historical baselines or compare current operational data against past performance. The `timeshifted` keyword modifies the timerange within the scope of the query. For example, when a custom dashboard has a global timerange of Today but your query only makes sense when looking at yesterday's data, you can use the keyword `timeshifted` followed by a time interval (`source logs timeshifted 1h`).


## Use direct key comparisons and exact matches in a query in {{site.data.keyword.logs_full_notm}}
{: #query-refine-4}
{: step}

Use direct key comparisons and exact matches such as `filter my.key == 'hello'` and avoid fuzzy matching such as `filter my.key ~ 'hello'` to let the engine take advantage of indexing for faster execution.


## Replace Dataprime dynamic transformations with parsing rules in {{site.data.keyword.logs_full_notm}}
{: #query-refine-5}
{: step}

Move complex formatting or parsing into parsing rules during ingestion to reduce query-time processing.

DataPrime supports dynamic transformations, but these transformations impact the time that is required to process the data.


## Change the querying mode to query data in the COS bucket to increase the amount of logs that are returned
{: #query-refine-6}
{: step}

Change the querying mode to query data in the COS bucket to increase the amount of logs that are returned.

When you run a query in {{site.data.keyword.frequent-search}} that returns the message `Scan limit exceeded`, you have hit the cap for a query.
- You can switch to **All Logs** mode in the *Logs* page. This mode queries your full archive where scan limits are much higher.
- You can switch to ***Analyze and Alert** in a custom widget configuration panel. This mode queries data in the {{site.data.keyword.frequent-search}} and {{site.data.keyword.monitoring}} data pipelines where scan limits are much higher.
- You can also simplify the query by removing unnecessary transformations, filters, or nested expressions that force full scans.
