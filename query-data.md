---

copyright:
  years:  2023, 2024
lastupdated: "2024-06-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


#  Querying data
{: #query-data}

In {{site.data.keyword.logs_full_notm}}, you can query your log data by using Lucene queries, DataPrime queries, or by querying directly data from an {{site.data.keyword.cos_full_notm}} (COS) bucket. You can also apply filters to your queries.
{: shortdesc}


## Query data from the UI
{: #query-data-ui}

In the Explore **Logs** page, you can:

* [Filter log data](/docs/cloud-logs?topic=cloud-logs-query-data-filter)
* [Search log data using Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene)
* [Search log data using DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)

Filtering can be used in conjunction with searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).

After you define a query, you can save it for later reuse by creating a view. For more information, see [Creating custom views](/docs/cloud-logs?topic=cloud-logs-custom_views&interface=ui#create_view).



##  Considerations when querying {{site.data.keyword.frequent-search}} data
{: #query-data-frequent-search}

There are considerations when querying log data in the {{site.data.keyword.logs_full_notm}} {{site.data.keyword.frequent-search}} pipeline:

- Filtering can be used in conjunction with searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).
- Logs in the [{{site.data.keyword.frequent-search}} pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) are indexed. If your instance reaches its maximum amount of indexed fields, additional fields are unavailable to query. For more information on indexing and data mapping, see [Understanding indexing and field mapping](/docs/cloud-logs?topic=cloud-logs-index-field-map).
- You can get a mapping exception when data that is ingested through the {{site.data.keyword.frequent-search}} data pipeline detects the same field sent by different log records with different types. Mapping exceptions make fields unavailable to query. For more information, see [Mapping exceptions](/docs/cloud-logs?topic=cloud-logs-query-mapping-exceptions).
- Logs ingested through the {{site.data.keyword.monitoring}} and {{site.data.keyword.monitoring}} data pipelines can only be [directly queried from the archive.](/docs/cloud-logs?topic=cloud-logs-query-archive-data-bucket&interface=ui).
- You can query logs that are ingested and processed through the [{{site.data.keyword.frequent-search}} data pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) by using a Lucene query or a DataPrime query.

    For example, when you define a Lucene query, you can run queries such as free-text searches, regular RegEX expressions, or using field searches.

    If you are not seeing expected data:

    * Consider broadening your query or removing filters.

    * Note that some of your logs might not yet be indexed and will not be found by the filter or query.



##  Considerations when querying data from a bucket
{: #query-data-all-logs}

You can query data from the Explorer logs page or by running an archive query.

There are considerations when querying log data from the data bucket:

- Data stored in the data bucket include data ingested through the {{site.data.keyword.frequent-search}}, {{site.data.keyword.monitoring}}, and {{site.data.keyword.compliance}} data pipelines.
- You maintain the data in the bucket. You can keep the data for as long as you need and query it via the **Logs** page, selecting the **All logs** option.
- Filtering can be used in conjunction with searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).
- You can query data with unlimited time frames. There are no restrictions on how far back in time your data can go. You maintain the data and you ahve access to the data for as long as you keep it.
- You can query logs regardless of log priority and daily quota. Only blocked logs are not sent to the archive.
- Archive Query lets you to directly query your logs from your archive using any text or a wide range of syntax queries. You can query logs regardless of log priority, daily quota, or the time frame of your data. For more information, see [Querying archived data](/docs/cloud-logs?topic=cloud-logs-query-archive-data-bucket&interface=ui).


## Limitations querying data through the Explorer
{: #query-data-limitations}

Limits exist when querying data in {{site.data.keyword.logs_full}}.

<!-- Query limits -->
{{_include-segments/query-limits.md}}


## Archive query limitations
{: #query_archive_limits}

The following are the limitations placed on queries.

| Limitation | 	Description |
|---------|----------|
| Bytes processed |	Up to 30% of daily ingested bytes |
| Parquet files | Scanned	up to 500K files |
| Clone results |	Up to 1M results while running Archive Query |
| Time out |	Up to 5 minutes of query execution |
 {: caption="Table 1. Archive query limitations" caption-side="bottom"}

You also need to be aware of the following when querying archived data:

* You can use the same query syntax ([Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)) on the **Archive Queries** page.

* You might see slight delays when querying archived data when compared with other **Explore** queries.

* Once a limit is reached, a warning message is displayed. Refine your query results to avoid reaching a limit.


## Refining archive query results
{: #refine-archive-query}

You can refine your query results using the following methods:

* Apply more selective filters to your queries (for example, application or subsystem).

* If using the DataPrime [extract](/docs/cloud-logs?topic=cloud-logs-dataprime-ref#extract) operator and subsequently filtering its results, create a parsing rule and filter on the parsed field instead.

* Avoid regular expressions or wildcards in filters.

* In [DataPrime](/docs/cloud-logs?topic=cloud-logs-dataprime-ref), switch from using the contains operator on strings to the free text search operator (`~`).
