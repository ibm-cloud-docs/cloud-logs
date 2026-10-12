---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


#  Writing optimized queries in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations}

In {{site.data.keyword.logs_full_notm}}, you can query log data by using Lucene queries, or DataPrime queries. You can query data in {{site.data.keyword.frequent-search}} or you can query directly data from an {{site.data.keyword.cos_full_notm}} (COS) bucket. In this topic, find out best practices to write optimized queries.
{: shortdesc}


## Replace DataPrime dynamic transformations with parsing rules in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-1}

Move complex formatting or parsing in a query into parsing rules during ingestion to reduce query-time processing.
{: tip}

DataPrime supports dynamic transformations, but these transformations impact the time that is required to process the data.

For example, if you have a query that uses the DataPrime [extract](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#extract) operator and subsequently filtering its results, consider creating a parsing rule and filtering on the parsed field instead. For more information, see [extract command](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#extract).

The following list outlines the DataPrime commands that generate new fields or modify existing ones and you **should replace with parsing rules**:

- `extract`: Transforms raw strings into structured data using regex or key-value logic.

    Sample: `extract $d.my_text into $d.my_data using regexp(e=/user (?<user>.*) has logged in/)`

- `explode`: Transforms an array of N elements into N separate fields. Each field contains one element of the array at the specified keypath.

- `create`: Defines a new field and assigns it a value from an expression.

    Sample: `create is_error from status_code >= 400`

- `replace`: Overwrites a field with a new value.

    Sample: `replace duration_ms with duration / 1_000_000`

- `remove`: Removes fields from the log record.

    Sample: `remove field1`

- `convert`: Makes type conversions explicit for readability.

    Sample: `convert datatypes status_code:number`

- `redact`: Masks sensitive data using a regex expression.

    Sample: `redact message matching /[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}/ to '[EMAIL]'`


## Reduce the working data set before running transformations and aggregations to improve performance optimization in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-2}

Use any of the following methods to reduce the working data set before running transformations:

### Add explicit filter clauses or grep conditions early in a DataPrime query
{: #query-recommendations-2a}

Add explicit filter clauses or grep conditions early in your DataPrime Query Assistance or search bar to reduce the working data set before running transformations.
{: tip}

For example, the following sample shows a filter condition before an aggregation expression:

```text
source logs
| filter $d.action == 'create'
| groupby $d.path aggregate count()
```
{: codeblock}

### Use the choose command to extract only the requested fields in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-2b}

Use the `choose` command to extract and reshape the data fields that you need from a log record.
{: tip}

The `choose` command extracts only the requested fields, flattens nested keypaths, adds a calculated value, and includes a constant metadata field for easy tracking or reporting.

For more information, see [choose command](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#choose).


### Use dynamic range variables in the DataPrime query in a widget in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-2c}

This recommendation only applies to DataPrime queries that you configure in the widget of a custom dashboard.
{: note}

If you are running a DataPrime query in a widget in a custom dashboard, you can use dynamic range variables (`$p`) to reduce the working data set before running transformations.
{: tip}

For more information, see [Using query parameters in your DataPrime queries in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-query-parameters).


## Narrow the timeframe of a query in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-3}

Querying large time ranges (weeks or months) increases the scan volume and slows down results.

Use relative time queries to narrow the timeframe of a query in {{site.data.keyword.logs_full_notm}}.
{: tip}

Relative time queries are handled via DataPrime time expressions. For example, use `now()` combined with standard time arithmetic and intervals (such as 1h, 15m, or 30s) to filter events dynamically or filter logs that are newer than one hour `($m.timestamp > now() - 1h)`. For more information, see [DataPrime date / time functions](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-date-time-func).

You can also use dynamic time range variables (`$p`) to automatically respect active dashboard time pickers. For example, you can reference `$p.timeRange.startTime` or `$p.timeRange.endTime` in your queries. For more information, see [Using query parameters in your DataPrime queries in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-query-parameters).

You can shift the evaluation window backward inside specific Dataprime commands to analyze historical baselines or compare current operational data against past performance. The `timeshifted` keyword modifies the timerange within the scope of the query. For example, when a custom dashboard has a global timerange of Today but your query only makes sense when looking at yesterday's data, you can use the keyword `timeshifted` followed by a time interval (`source logs timeshifted 1h`).

## Use exact matches when doing string searches in fields in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-4}

### Use direct key comparisons and exact matches in a query in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-4a}

Use direct key comparisons and exact matches such as `filter field == 'value'`.
{: tip}

Avoid fuzzy matching such as `filter field ~ 'value'` to let the engine take advantage of indexing for faster execution.

Make sure the number of characters for the value is more than 4. When the number of characters is less than 4, the field value pair is handled as a free text search and that impacts the time that is required to process the data.
{: note}


### Use regex searches against keywords since keywords are not passed through the analyzer in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-4b}

Regex searches let you use regular expressions to match patterns within your log data. [Lucene standard operators](https://www.elastic.co/guide/en/elasticsearch/reference/8.4/regexp-syntax.html#regexp-standard-operators){: external} are supported.

Regex patterns to be matched need to be enclosed in forward slashes (`/`).

Whenever possible use regex searches against keywords since keywords are not passed through the analyzer.
{: tip}


## Reduce the working data set after running transformations and aggregations and improve performance optimization in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-5}

Use any of the following methods to reduce the working data set after running transformations:

### Add the limit clause in a DataPrime search query that does not include aggregation commands in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-5a}

Use the `limit` clause in a search query to reduce the data resultset and improve performance optimization. For example, `source logs | ... | limit 500`.
{: tip}

The `limit` command restricts the number of logs that are returned by a query to the specified count.

This command is useful for performance optimization or for displaying only a subset of high-value results.

The `limit` command does not guarantee order unless it is used after an explicit orderby. If order matters, always pair it with `orderby` to ensure predictable results.


### Add the top or bottom command in a DataPrime search query that includes aggregation to improve performance optimization in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-5b}

You can use the `limit` clause in a search query that includes aggregation to reduce the data resultset and improve performance optimization. For example, `source logs | ... | groupby key aggregate avg(duration) as avg_duration | limit 500`.
{: tip}

- The `limit` command restricts the number of logs that are returned by a query to the specified count. It is typically used after sorting or aggregating operations to retrieve only the most relevant or top results from a larger dataset.

- The `limit` command is useful for performance optimization or for displaying only a subset of high-value results.

- The `limit` command does not guarantee order unless it is used after an explicit orderby. If order matters, always pair it with `orderby` to ensure predictable results.

When you run a query that combines the `orderby` aggregation command and the `limit` clause, use the `top` or `bottom` command instead, which combines ordering and limiting in one operation. For more information, see [top command](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#top) and [bottom command](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#bottom).
{: tip}

To sort the data by ascending/descending order of the expression value, use the orderby / sortby / order by / sort by commands.Ordering by multiple expressions is supported. For more information, see [orderby / sortby / order by / sort by](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#order_sort).

#### top command
{: #query-recommendations-5b-top}

The top command returns the first N results after sorting by one or more expressions in the by clause. It can be used with plain expressions or with aggregation functions.

- Without aggregation, the `top` command limits the full result set to N rows, ordered by a given expression.

- With aggregation, the `top` command groups results by the result expressions and returns the top N groups (not N rows per group), ranked by the ordering expression.

#### bottom command
{: #query-recommendations-5b-bottom}

The bottom command limits the rows returned from a query to the last N rows in a given set, ordered by a specified expression. It is useful for finding the lowest-ranking values or least frequent occurrences within a dataset.

When using this command, pay close attention to your ordering expression, as it determines which records are considered "bottom" in the result.


### Use the limit parameter through the CLI or when using the API
{: #query-recommendations-6}

When you run the query via API or CLI, you can limit the number of results setting the `limit` parameter in the `metadata` for the request.

## Avoid regular expressions or wildcards in filters
{: #query-recommendations-7}

Avoid regular expressions or wildcards in filters.
{: tip}



## Run free-text searches with moderation in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-3}

If you run a free-text search, consider the following scenarios:

- [Lucene] Avoid running free-text searches without the context of a specified keypath.

- [DataPrime] Use the `filter` command and the free-text search operator (`~`) for partial text searches within the context of a field in DataPrime queries.

- [DataPrime] Use the `find` command for quickly searching raw log fields across log messages or string fields where full parsing is unnecessary in DataPrime queries.

- [DataPrime] Avoid using the `contains` command in DataPrime queries.

- [DataPrime] Avoid using the `wildfind` or the `wildtext` commands.

    The `wildfind` command searches for a given string across all keypaths in every document in the working set. It is significantly slower than the `find` command, since it must inspect every field in every document. Use `find` when the keypath is known for better performance.


### Use the find command to perform a free-text search query in DataPrime query within a specified keypath (field) in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-3a}

The `find` command performs a free-text search within a specified keypath. Looks for specific strings without needing full field parsing. It acts as a shorthand for combining filter with a text match (~).

Use the `find` command for quickly searching raw log fields across log messages or string fields where full parsing is unnecessary.
{: tip}

For more information, see [Find command](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators-text-search#find_text).

### Use double quotes to run a free-text search query in Lucene within the context of a specified keypath (field) in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-3b}

To run a free-text search within the context of a specified keypath, include the string content within double quotes. For example, `field:"Error 403 - MSG001"`
{: tip}

### Use the free-text search operator for partial text searches within a specified keypath (field) in a DataPrime query in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-3c}

When you search for a partial string in a field value pair, switch from using the `contains` operator on strings to the free text search operator (`~`).
{: tip}

Use the expression:

```text
 filter field ~ 'value'
```
{: codeblock}

Use the `filter` command and the free-text search operator (`~`) for partial text searches within the context of a field in DataPrime queries.
{: tip}

### Use double quotes to run a free-text search query in Lucene without the context of a specified keypath (field) in {{site.data.keyword.logs_full_notm}}
{: #query-recommendations-3d}

Avoid running free-text searches without the context of a specified keypath. Why? When you run a free-text search, the query checks all the data available for search within the time range specified in the time picker and performance is degraded.
{: note}

If you must run a free-text search without the context of a specified keypath, include the string content within double quotes. For example, `"Error 403 - MSG001"` or `"Error 403" AND "P45- MSG001"`.
