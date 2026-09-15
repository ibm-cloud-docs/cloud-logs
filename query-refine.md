---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Refining query results in {{site.data.keyword.logs_full_notm}}
{: #query-refine}

In {{site.data.keyword.logs_full}}, you can refine a query by adding filters, narrowing timeframes, using dynamic variables, creating parsing rules, and using exact matches.
{: shortdesc}

Checklist for refining a query in {{site.data.keyword.logs_full_notm}}:

## Use the limit clause in your search query to reduce the data resultset
{: #query-refine-0}

Use the `limit` clause in your search query to reduce the data resultset and improve performance optimization. For example, `source logs | ... | limit 500`.

The limit command restricts the number of logs that are returned by a query to the specified count.

It is typically used after sorting or aggregating operations to retrieve only the most relevant or top results from a larger dataset.

This command is useful for performance optimization or for displaying only a subset of high-value results.

The `limit` command does not guarantee order unless it is used after an explicit orderby. If order matters, always pair it with `orderby` to ensure predictable results.



## Reduce the data resultset by adding filters to a query in {{site.data.keyword.logs_full_notm}}
{: #query-refine-1}

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

This recommendation only applies to Dataprime queries that you configure in the widget of a custom dashboard.
{: note}

If you are running a Dataprime query in a widget in a custom dashboard, you can use dynamic range variables (`$p`) to reduce the the working data set before running transformations.

For more information, see [Using query parameters in your DataPrime queries in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-query-parameters).


## Narrow the timeframe of a query in {{site.data.keyword.logs_full_notm}}
{: #query-refine-3}

Shorten the default time range in the *Explore Logs* page or inside the query code to minimize the volume of data that is scanned.

Querying large time ranges (weeks or months) increases the scan volume and slows down results.

To narrow the timeframe of a query in {{site.data.keyword.logs_full_notm}}:

- Use the time picker to select only what is necessary.

- Use relative time queries.

    Relative time queries are handled via DataPrime time expressions. For example, use `now()` combined with standard time arithmetic and intervals (such as 1h, 15m, or 30s) to filter events dynamically or filter logs that are newer than one hour `($m.timestamp > now() - 1h)`. For more information, see [DataPrime date / time functions](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-date-time-func).

    You can also use dynamic time range variables (`$p`) to automatically respect active dashboard time pickers. For example, you can reference `$p.timeRange.startTime` or `$p.timeRange.endTime` in your queries. For more information, see [Using query parameters in your DataPrime queries in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-query-parameters).

    You can shift the evaluation window backward inside specific Dataprime commands to analyze historical baselines or compare current operational data against past performance. The `timeshifted` keyword modifies the timerange within the scope of the query. For example, when a custom dashboard has a global timerange of Today but your query only makes sense when looking at yesterday's data, you can use the keyword `timeshifted` followed by a time interval (`source logs timeshifted 1h`).

## Change the querying mode to query data in the COS bucket to increase the amount of logs that are returned
{: #query-refine-4}

Change the querying mode to query data in the COS bucket to increase the amount of logs that are returned.

When you run a query in {{site.data.keyword.frequent-search}} that returns the message `Scan limit exceeded`, you have hit the cap for a query.
- You can switch to **All Logs** mode in the *Logs* page. This mode queries your full archive where scan limits are much higher.
- You can switch to ***Analyze and Alert** in a custom widget configuration panel. This mode queries data in the {{site.data.keyword.frequent-search}} and {{site.data.keyword.monitoring}} data pipelines where scan limits are much higher.
- You can also simplify the query by removing unnecessary transformations, filters, or nested expressions that force full scans.


## Commands reduce the dataset by applying filters or keeping only relevant fields


These commands reduce the dataset by applying filters or keeping only relevant fields.

    filter – Keep rows where a condition is true.

    filter status_code >= 500

    block – The opposite of filter. Remove rows that match a condition.

    block method == 'OPTIONS'

    choose / select – Keep only the specified fields.

    choose path, status_code

    distinct – Return one row per unique value.

    distinct user_id

    find / text – Free-text search within a field or across all data.

    find 'timeout' in message
    text '503'


## Commands that let you generate new fields or modify existing ones

Commands that let you generate new fields or modify existing ones.

    create / add / c – Define a new field based on an expression. This acts similarly to a variable.

    create is_error from status_code >= 500

    replace – Overwrite a field with a new value.

    replace duration_ms with duration / 1_000_000

    remove – Remove fields from the document.

    remove user_agent

    convert – Make type conversions explicit for readability.

    convert datatypes status_code:number

    redact – Mask sensitive data using regex.

    redact message matching /[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}/ to '[EMAIL]'
