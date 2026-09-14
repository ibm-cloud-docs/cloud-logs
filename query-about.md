---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# About running queries in {{site.data.keyword.logs_full_notm}}
{: #query-about}

Consider the following information when you run a query in {{site.data.keyword.logs_full_notm}}:
{: shortdesc}

## About the data that is ingested and available for querying
{: #query-about-data}

Logs that are ingested and stored in {{site.data.keyword.logs_full_notm}} in the {{site.data.keyword.frequent-search}} backend or in your {{site.data.keyword.cos_full_notm}} (COS) bucket are referred as raw data.

When you build a query using Lucene or DataPrime or use widgets inside a custom dashboard, you get raw logs before you apply any transformations. For example, when you first drag a Dynamic Widget onto a dashboard, it opens in a table view displaying raw data in JSON format.

When you apply transformations that combine responses into a summary form such as percentages or totals, the data returned by the query is known as aggregated data.

In {{site.data.keyword.logs_full_notm}}, you aggregate data by using the Query Builder and the DataPrime query language to transform raw logs into aggregated data. For example, you can aggregate data by using any of the following aggregation methods:

- *Global Aggregation method*: Use this method to compute totals, averages, minimums, maximums, or counts as a single group using the aggregate command. For more information, see [DataPrime aggregation expressions](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-expressions-agg).

- *Grouping Data method*: Use this method to split data into distinct categories or shared values using the groupby command to calculate metrics per group. For more information, see [Group by](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#groupby).

- *Multi-Grouping method*: Use this method to combine multiple grouping statements or concatenate queries using multigroupby for efficient single-scan execution. For more information, see [multigroupby](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#multigroupby).



## Data stored in a COS bucket is normalized using a column-based schema
{: #query-about-0}

Logs that are ingested have different structures. As data is ingested, the {{site.data.keyword.logs_full_notm}} service automatically normalizes logs into a consistent column-based schema to improve querying.

- The normalization process prioritizes commonly used field names.

- Less frequent or rarely used fields might be excluded from the Parquet schema.

- Each Parquet file is limited to a maximum of 5,100 columns.

- A full original JSON document is also stored within a special column.

- If a query references a field that is not among the 5,100 Parquet columns, DataPrime will fall back to searching the raw JSON in the special column to retrieve the data.

## Maximum number of query requests
{: #query-about-1}

Direct query requests are capped at 30 per minute per instance.

Queries are limited to a maximum run time of 30 minutes for background queries.

## Maximum running time per query
{: #query-about-2}

Queries are limited to a maximum run time of 5 minutes in Explore.

Queries are limited to a maximum run time of 30 minutes for background queries.

## Maximum number of bytes scanned per query
{: #query-about-3}

The number of bytes that are scanned for queries that run on data in **{{site.data.keyword.frequent-search}}** is limited to 100MB. This limitation is placed on fetching 100 MB of high-tier data.

The number of bytes that are scanned for data available in the COS data bucket is limited to 30% of your daily ingest.



## Results returned by a query
{: #query-about-4}

The number of results that are returned by a DataPrime query depends on the type of the query and where it is being executed.

The following table shows the default limit and maximum limit on logs lines that are returned through the UI in any of the listed scenarios:

| UI Query Type                                                               | Default Limit     | Maximum Limit.    |
| ----------------------------------------------------------------------------|-------------------|-------------------|
| Explorer & dashboard widgets - Dataprime query including aggregation        | 2,000             | 5,000             |
| Explorer & dashboard widgets - Queries returning raw data                   | N/A               | 15,000            |
| Archive query                                                               | 2,000             | 30,000            |
{: caption="Log lines returned through the UI" caption-side="top"}

The following table shows the default limit and maximum limit on logs lines that are returned through the API in any of the listed scenarios:

| API Query Type            | Default Limit     | Maximum Limit.    |
| --------------------------|-------------------|-------------------|
| Archive query             | 2,000             | 50,000            |
| Background archive query  | N/A               | 1,000,000         |
{: caption="Log lines returned through the API" caption-side="top"}


The following table shows the default limit and maximum limit on logs lines that are returned through the CLI in any of the listed scenarios:

| CLI Query Type            | Default Limit     | Maximum Limit.    |
| --------------------------|-------------------|-------------------|
| Archive query             | 2,000             | 50,000            |
| Background archive query  | N/A               | 1,000,000         |
{: caption="Log lines returned through the CLI" caption-side="top"}


The number of logs lines that are returned by a query is the smaller of:
- The value set in the `limit` command in your DataPrime query. The limit command restricts the number of documents returned by a query to a specified count. It is typically used after sorting or aggregation operations to retrieve only the most relevant or top results from a larger dataset.
- For a query run via API or CLI, the value set in the `metadata.limit` field. The metadata.limit field sets the maximum number of results to be returned. The default value is 2000 results. The maximum value that can be specified for the TIER_FREQUENT_SEARCH (data in {{site.data.keyword.frequent-search}}) is 12000. The maximum value that can be specified for the TIER_ARCHIVE (data stored in the data bucket) is 50000.
- The tier's hard limit.

    If the query does not set a limit, by default you get the soft limit of 2,000 log lines regardless of the tier.

    The TIER_FREQUENT_SEARCH ({{site.data.keyword.frequent-search}}) hard limit is 12000 log lines.

    The TIER_ARCHIVE hard limit is 50,000 log lines for archive queries and 1,000,000 log lines for backgroubd archive queries.


To control the number of results that are returned by a query, you can refine the query by applying filters and reducing the timerange. For more information, see [Refining query results](/docs/cloud-logs?topic=cloud-logs-query-refine).



## Partial data when Shuffle limit is reached
{: #query-about-5}

Partial data is returned when the shuffle limit is reached as a result of a query that does joins or aggregations.
{: note}

A shuffle limit refers to a constraint on the amount of data that can be processed during operations that require data shuffling, such as joins or aggregations.

When a DataPrime query involves significant data movement, especially in joins with large datasets of logs that exceed this limit, you can get a warning such as  `shuffleFileSizeLimitReachedWarning`. The result set may be incomplete or incorrect when aggregation functions are used because not all data is processed.

This warning may appear in any of the following situations:
- When using joins in a DataPrime query.
- When the data that is being shuffled does not fit into memory.

This warning can also happen under various conditions depending on the query design.



| Location           | Max shuffle size |
| ------------------ | ---------------- |
| Explore            | 1GB              |
| API                | 1GB              |
| Background queries | 10GB             |


What can you do when you reach the shuffle limit on a query?

1. Apply filters to reduce the dataset size.
2. Decrease the number of joins in the query.
3. Check for cardinality explosions, for example, many-to-many relationships.

## Partial data when Block limit is reached
{: #query-about-6}

Partial data is returned when the Block limit is reached running a query that searches data in the data bucket.
{: note}

In a data bucket, data ingested is divided into logical units called blocks. A block is a group of log data bundled together, typically by time intervals. When you run a query on data that is available in the data bucket, the {{site.data.keyword.logs_full_notm}} service must load and scan one or more of these blocks to extract the requested log lines.

You might encounter a `BLOCK_LIMIT` error when a query attempts to process too many blocks in a single execution due to a large time range or filters not applied, for example.

To avoid hitting the Block Limit, consider refining your query to reduce the set of data to query.
{: tip}



## Quering an empty array
{: #query-about-7}

When you run a DataPrime query on {{site.data.keyword.frequent-search}} data, the query is translated into a Lucene query by the DataPrime engine.

In Lucene, an empty array is treated the same as a key with a value.
In DataPrime, an empty array is treated as a `null` value.

Depending on how you write your query, you might encounter inconsistencies running the query.

To work with empty arrays and avoid inconsistencies running the same query in *Priority Insights* or *All Logs*, use the following syntax to explicitly check the array length instead of relying on `null`:

```text
filter arrayLength($d.my_array) == 0
```
{: codeblock}


Do not use the following syntax:

```text
filter $d.my_array == null
```
{: codeblock}


## Using large numeric values
{: #query-about-8}

DataPrime supports numeric values up to a maximum of `2^53` (9,007,199,254,740,992). Using larger numbers may result in precision loss or unexpected behavior in queries.
{: note}

Limitations in binary precision as defined by the IEEE 754 standard may cause certain decimal values to be **stored or displayed imprecisely**, even if they appear simple.
