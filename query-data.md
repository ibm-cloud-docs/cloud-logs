---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


#  Querying data
{: #query-data}

In {{site.data.keyword.logs_full_notm}}, you can query log data by using Lucene queries, DataPrime queries, or by querying directly data from an {{site.data.keyword.cos_full_notm}} (COS) bucket. You can also apply filters to your queries.
{: shortdesc}

- You can query logs through the UI in the *Explorer Logs* page, through custom dashboards or by running an archive query.

- You can query logs in the CLI by running an archive query synchronously or a background archive query asynchronously.

- You can query logs by using the API to run an archive query synchronously or a background archive query asynchronously.

- You can access telemetry data directly from your {{site.data.keyword.cos_full_notm}} data bucket without reindexing or doing data rehydration.

- You can query historical data anytime without retention constraints.

- You can apply filtering in conjunction with search queries that use [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime). For example, you can use advanced features like aggregations, redactions, and dynamic filtering in a DataPrime query to refine analysis and handle compliance audit and performance checks more easily.

- You can query data across all the TCO data pipelines running queries against data that is stored in the data bucket. Data stored in the data bucket includes data ingested through the {{site.data.keyword.frequent-search}}, {{site.data.keyword.monitoring}}, and {{site.data.keyword.compliance}} data pipelines. It also includes logs that are matched through a Block parsing rule that has the *View blocked logs in Live tail and archive to IBM Cloud Object Storage* option enabled.

- You can query data through visual dashboards to surface correlations and patterns for faster root-cause analysis.

The following table lists the different methods that you can use to query data by TCO data pipeline in an {{site.data.keyword.logs_full_notm}} instance through the UI:

| Options to query data            | Priority Insights  | Analyze & Alert    | Store and Search   |
|----------------------------------|--------------------|--------------------|--------------------|
| Explore Logs (Priority Insights) | [Yes]{: tag-green} |                    |                    |
| Explore Logs (All Logs)          | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
| Custom dashboard                 | [Yes]{: tag-green} | [Yes]{: tag-green} |                    |
| Archive query                    | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Archive query options through the UI" caption-side="bottom"}

The following table lists the different methods that you can use to query data by TCO data pipeline in an {{site.data.keyword.logs_full_notm}} instance through the CLI or by using the API:

| Options to query data           | Priority Insights  | Analyze & Alert    | Store and Search   |
|---------------------------------|--------------------|--------------------|--------------------|
| Archive query (synchronous)     | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
| Background query (asynchronous) `[*]` | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Archive query options through CLI or API" caption-side="bottom"}

`[*]` This feature queries data in the COS data bucket.

Consider the following information when querying {{site.data.keyword.frequent-search}} data:

- You can query logs that are ingested and processed through the [{{site.data.keyword.frequent-search}} data pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) by using a Lucene query or a DataPrime query.

- You can apply filtering in conjunction with searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).

- Logs in the [{{site.data.keyword.frequent-search}} pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) are indexed. If your instance reaches its maximum amount of indexed fields, additional fields are unavailable to query. For more information on indexing and data mapping, see [Understanding indexing and field mapping](/docs/cloud-logs?topic=cloud-logs-indexing_mapping).

- You can get a mapping exception when data that is ingested through the {{site.data.keyword.frequent-search}} data pipeline detects the same field sent by different log records with different types. Mapping exceptions make fields unavailable to query. For more information, see [Mapping exceptions](/docs/cloud-logs?topic=cloud-logs-query-mapping-exceptions).

Consider the following information when querying data from the COS data bucket:

- Data stored in the data bucket includes data ingested through the {{site.data.keyword.frequent-search}}, {{site.data.keyword.monitoring}}, and {{site.data.keyword.compliance}} data pipelines. It also includes logs that are matched through a Block parsing rule that has the *View blocked logs in Live tail and archive to IBM Cloud Object Storage* option enabled.

- You can query historical data that is available in the bucket without retention constraints and using the same queries that you use for newly ingested data.

- You can apply filtering in conjunction with searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).

- You can use the same query syntax ([Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)) when you run a query on old data.

* You might see slight delays when querying archived data, that is data stored in the data bucket, when compared with other **Explore** queries that query data in Priority Insights.


##  Querying data from the UI
{: #query-data-ui}
{: ui}

In {{site.data.keyword.logs_full_notm}}, you can query data in the UI through the *Explorer Logs* page, a custom dashboard, or by running an archive query. You can query log data by using Lucene queries, DataPrime queries, or by querying directly data from an {{site.data.keyword.cos_full_notm}} (COS) bucket. You can also apply filters to your queries.


### Querying data through the Explorer Logs page
{: #query-data-ui-explorer}

In the *Explore logs* page,

- You can monitor {{site.data.keyword.frequent-search}} data through the *Priority Insights* option.

- You can monitor data through the *All Logs* option that is available in the COS data bucket and ingested through any data pipeline.

- You can [search log data by using Lucene queries](/docs/cloud-logs?topic=cloud-logs-query-data-lucene)

- You can [search log data by using DataPrime queries](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)

You can also apply [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter) in conjunction with searching using Lucene or DataPrime.

After you define a query, you can save it for later reuse by creating a view. For more information, see [Launching views](/docs/cloud-logs?topic=cloud-logs-custom_views#custom_views_launch) and [Creating custom views](/docs/cloud-logs?topic=cloud-logs-custom_views&interface=ui#create_view).



### Querying data by running an archive query
{: #query-data-ui-archive}

By using the *Archive Query* feature, you can query data stored in the {{site.data.keyword.cos_full_notm}} data bucket. This query runs asynchronously.

For more information, see [Running an archive query]().


## Query data using the CLI
{: #query-data-cli}
{: cli}

There are two ways to query log data using the CLI:

* Running a synchronous query using the `ibmcloud cloud-logs query` command.
* Running an asynchronous query using the `ibmcloud cloud-logs background-query-create` command.

The Query CLI supports only `logs-raw`, `logs-prettify`, and `json` as output. The default is `logs-raw`.
{: note}

### Querying data by running a synchronous query
{: #query-data-cli-sync}

The `query` command is limited to returning 50K log lines.

### Querying data by running an asynchronous query
{: #query-data-cli-async}

You can run the `ibmcloud cloud-logs background-query-create` command to query logs in the {{site.data.keyword.cos_full_notm}} data bucket asynchronously.

The background query lets you run a query and fetch the results at a later point in time. The query results are prepared and, once ready, you can download the results as a file using the CLI or the API.

With the background query, up to 1M records can be returned.

## Query data using the API
{: #query-data-api}
{: api}

### Querying data by running a synchronous query
{: #query-data-api-sync}

The `query` command is limited to returning 50K log lines.

### Querying data by running an asynchronous query
{: #query-data-api-async}


## Refining query results (recommendations building queries)
{: #query-data-refine-query}

You can refine your query results using the following methods:

- Reduce the time range of the query.

- Apply more filters to your queries, in addition to application, subsystem or severity.

- In [DataPrime](/docs/cloud-logs?group=dataprime),

    Switch from using the contains operator on strings to the free text search operator (`~`).

    If using the DataPrime [extract](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#extract) operator and subsequently filtering its results, create a parsing rule and filter on the parsed field instead.

    Decrease the number of joins in a query.

    Use the `limit` clause in your search query. For example, `source logs | limit 500`.

    When you run the query via API or CLI, you can also limit the number of results setting the `limit` parameter in `metadata` for the request.

- Avoid regular expressions or wildcards in filters.
