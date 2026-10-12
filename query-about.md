---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# About running queries in {{site.data.keyword.logs_full_notm}}
{: #query-about}

Consider the following information when you run a query in {{site.data.keyword.logs_full_notm}}:
{: shortdesc}

## About the data in {{site.data.keyword.logs_full_notm}}
{: #query-about-data}

Logs that are ingested and stored in {{site.data.keyword.logs_full_notm}} in the {{site.data.keyword.frequent-search}} backend or in your {{site.data.keyword.cos_full_notm}} (COS) bucket are referred as raw data.

When you build a query using Lucene or DataPrime or use widgets inside a custom dashboard, you get raw logs before you apply any transformations. For example, when you first drag a Dynamic Widget onto a dashboard, it opens in a table view displaying raw data in JSON format.

When you apply transformations that combine responses into a summary form such as percentages or totals, the data returned by the query is known as aggregated data.

In {{site.data.keyword.logs_full_notm}}, you aggregate data by using the DataPrime query language to transform raw logs into aggregated data. For example, you can aggregate data by using any of the following aggregation methods:

- *Global Aggregation method*: Use this method to compute totals, averages, minimums, maximums, or counts as a single group using the aggregate command. For more information, see [DataPrime aggregation expressions](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-expressions-agg).

- *Grouping Data method*: Use this method to split data into distinct categories or shared values using the groupby command. For more information, see [Group by](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#groupby).

- *Multi-Grouping method*: Use this method to combine multiple grouping statements or concatenate queries using multigroupby for efficient single-scan execution. For more information, see [multigroupby](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#multigroupby).



### Using large numeric values in {{site.data.keyword.logs_full_notm}}
{: #query-about-8}

DataPrime supports numeric values up to a maximum of `2^53` (9,007,199,254,740,992). Using larger numbers may result in precision loss or unexpected behavior in queries.
{: note}

Limitations in binary precision as defined by the IEEE 754 standard may cause certain decimal values to be **stored or displayed imprecisely**, even if they appear simple.


### Keyword data type in search queries in {{site.data.keyword.logs_full_notm}}
{: #query-data-ui-explorer-keyword}

Keywords represent text that does not pass through the analyzer before indexing.

The keyword data type is suitable for regular expressions, aggregation, and sorting. For more information, see [Using RegEX to query data](/docs/cloud-logs?topic=cloud-logs-query-regex).

The syntax to use the keyword data type in your query is:

```text
<fieldName>.keyword
```
{: codeblock}

{{site.data.keyword.logs_full_notm}} can not create a keyword type when a field is longer than 256 characters.
{: important}


### Quering an empty array in {{site.data.keyword.logs_full_notm}}
{: #query-about-7}

When you run a DataPrime query on {{site.data.keyword.frequent-search}} data, the query is translated into a Lucene query by the DataPrime engine.

In Lucene, an empty array is treated the same as a key with a value. In DataPrime, an empty array is treated as a `null` value. Depending on how you write your query, you might encounter inconsistencies running the query.

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



##  Considerations when querying {{site.data.keyword.frequent-search}} data
{: #query-about-frequent-search}

There are considerations when querying log data in the {{site.data.keyword.logs_full_notm}} {{site.data.keyword.frequent-search}} pipeline:

- You can query logs that are ingested and processed through the [{{site.data.keyword.frequent-search}} data pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) by using a Lucene query or a DataPrime query.
- Filtering can be used in conjunction with searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).
- Logs in the [{{site.data.keyword.frequent-search}} pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) are indexed. If your instance reaches its maximum amount of indexed fields, additional fields are unavailable to query. For more information on indexing and data mapping, see [Understanding indexing and field mapping](/docs/cloud-logs?topic=cloud-logs-indexing_mapping).
- You can get a mapping exception when data that is ingested through the {{site.data.keyword.frequent-search}} data pipeline detects the same field sent by different log records with different types. Mapping exceptions make fields unavailable to query. For more information, see [Mapping exceptions](/docs/cloud-logs?topic=cloud-logs-query-mapping-exceptions).


## Refining query results (recommendations building queries)
{: #query-about-refine-query}

In {{site.data.keyword.logs_full}}, you can refine a query by adding filters, narrowing timeframes, using dynamic variables, creating parsing rules, and using exact matches.

For more information, see [Refining query results in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-query-refine).


## Querying data through the UI in {{site.data.keyword.logs_full_notm}}
{: #query-about-ui-ov}
{: ui}

In {{site.data.keyword.logs_full_notm}}, you can query data in the UI through the *Explorer Logs* page, a custom dashboard, or by running an archive query. You can query log data by using Lucene queries, DataPrime queries, or by querying directly data from an {{site.data.keyword.cos_full_notm}} (COS) bucket.

You can also apply [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter) in conjunction with searching using Lucene or DataPrime.

After you define a query, you can save it for later reuse by creating a view. For more information, see [Launching views](/docs/cloud-logs?topic=cloud-logs-custom_views#custom_views_launch) and [Creating custom views](/docs/cloud-logs?topic=cloud-logs-custom_views&interface=ui#create_view).

### Querying data synchronously through the Logs Explorer UI in {{site.data.keyword.logs_full_notm}}
{: #query-about-ui-explorer}
{: ui}

In {{site.data.keyword.logs_full_notm}}, you can query data through the *Logs Explorer* page by using any of the following options:

- You can monitor {{site.data.keyword.frequent-search}} data through the *Priority Insights* option.

- You can monitor data through the *All Logs* option that is available in the COS data bucket and ingested through any data pipeline.

- You can [search log data by using Lucene queries](/docs/cloud-logs?topic=cloud-logs-query-data-lucene)

- You can [search log data by using DataPrime queries](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)

### Querying data asynchronously through the UI in {{site.data.keyword.logs_full_notm}}
{: #query-about-ui-archive}
{: ui}

In {{site.data.keyword.logs_full_notm}}, you can query data asynchronously that is stored in the {{site.data.keyword.cos_full_notm}} data bucket through the **Logs Explorer > Archive** page.



## Querying data by using CLI commands in {{site.data.keyword.logs_full_notm}}
{: #query-about-cli-ov}
{: cli}

In {{site.data.keyword.logs_full_notm}}, you can query log data synchronously by using the `ibmcloud logs query` CLI commands or asynchronously by using the `ibmcloud logs background-query` commands.


### Querying data asynchronously by using CLI commands in {{site.data.keyword.logs_full_notm}}
{: #query-about-cli-ov-1}
{: cli}

In {{site.data.keyword.logs_full_notm}}, you can query log data asynchronously by using the `ibmcloud logs background-query` commands.

The background query lets you run a query and fetch the results at a later point in time. The query results are prepared and, once ready, you can download the results as a file using the CLI or the API.

With the background query up to 1M records can be returned.

For more information, see [Managing background queries through the CLI](/docs/cloud-logs?topic=cloud-logs-query-background&interface=cli#query-background-cli).


### Querying data synchronously by using CLI commands in {{site.data.keyword.logs_full_notm}}
{: #query-about-cli-ov-2}
{: cli}

In {{site.data.keyword.logs_full_notm}}, you can query log data synchronously by using the `ibmcloud logs query` CLI commands.

The `query` command is limited to returning 50K records.

For more information, see [Running synchronous queries through the CLI in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-query-synch#query-sync-ov-cli).

## Querying data by using the API in {{site.data.keyword.logs_full_notm}}
{: #query-about-api-ov}
{: api}

In {{site.data.keyword.logs_full_notm}}, you can query log data synchronously by using the method `POST /v1/query` or asynchronously by using the method `POST /v1/background_query`.


### Querying data asynchronously by using the API in {{site.data.keyword.logs_full_notm}}
{: #query-about-api-ov-1}
{: api}

In {{site.data.keyword.logs_full_notm}}, you can query log data asynchronously by using the method `POST /v1/background_query`.

The background query lets you run a query and fetch the results at a later point in time. The query results are prepared and, once ready, you can download the results as a file using the CLI or the API.

With the background query up to 1M records can be returned.

For more information, see [Managing background queries through the API](/docs/cloud-logs?topic=cloud-logs-query-background&interface=cli#query-background-api).

### Querying data synchronously by using the API in {{site.data.keyword.logs_full_notm}}
{: #query-about-api-ov-2}
{: api}

In {{site.data.keyword.logs_full_notm}}, you can query log data synchronously by using the method `POST /v1/query`.

The `query` command is limited to returning 50K records.

For more information, see [Running synchronous queries through the API in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-query-synch#query-sync-ov-api).
