---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Querying data through the Explorer Logs UI in {{site.data.keyword.logs_full_notm}}
{: #query-data-ui-explorer}

In {{site.data.keyword.logs_full_notm}}, you can query data through the *Explorer Logs* page.
{: shortdesc}

In the *Explore logs* page, you can:

* [Search log data by using Lucene queries](/docs/cloud-logs?topic=cloud-logs-query-data-lucene)
* [Search log data by using DataPrime queries](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)

You can also apply [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter) in conjunction with searching using Lucene or DataPrime.

After you define a query, you can save it for later reuse by creating a view. For more information, see [Launching views](/docs/cloud-logs?topic=cloud-logs-custom_views#custom_views_launch) and [Creating custom views](/docs/cloud-logs?topic=cloud-logs-custom_views&interface=ui#create_view).


## Limitations querying data from the data bucket through Explorer
{: #query-data-ui-archive-limitations-1}

Read the following limitations that apply when you query data located in the data bucket through a view in **Explore Logs > Logs** that queries **All Logs**:

| Limitations per query     | Description  |
|--------------------------|--------------|
| Characters that can be included in a query | A search query can include a maximum of 3000 characters. |
| Query using the keyword data type | You can not create a keyword type when a field that is longer than 256 characters. |
| Bytes processed          | Up to 30% of daily ingested bytes |
| Parquet files scanned    | Up to 500.000 files |
| Ordering of logs         | Ordering is guaranteed only for up to 10,000 results. |
| Time out running a query | Up to 5 minutes of query execution |
| Number of logs that are returned from a query  | The maximum number of results that are returned from {{site.data.keyword.cos_full_notm}} (from a query using *All Logs*) is 50.000 log lines when you run a Lucene query. <\n>Up to 30,000 log lines setting the `limit <value>` in a DataPrime query. The default limit is set to 2000 log lines. <\n>Up to 5,000 log lines when you run an analytical query that includes aggregation in a DataPrime query. <\n>Up to 15,000 log lines for a query where there is no aggregation in a DataPrime query.|
{: caption="Limitations running a query on data from a COS bucket" caption-side="bottom"}

Once a limit is reached, a warning message is displayed. Refine your query results to avoid reaching a limit.
{: important}

## Limitations querying data in {{site.data.keyword.frequent-search}} through Explorer
{: #query-data-ui-archive-limitations-2}

Read the following limitations that apply when you query data located in {{site.data.keyword.frequent-search}} through a view in **Explore Logs > Logs** that queries **Priority Insights**:

| Limitations per query     | Description  |
|--------------------------|--------------|
| Characters that can be included in a query | A search query can include a maximum of 3000 characters. |
| Query using the keyword data type | You can not create a keyword type when a field that is longer than 256 characters. |
| Bytes processed          | A maximum of 100 MB is scanned for {{site.data.keyword.frequent-search}} data.|
| Parquet files scanned    | Up to 500.000 files |
| Ordering of logs         | Ordering is guaranteed only for up to 10,000 results. |
| Time out running a query | Up to 5 minutes of query execution |
| Number of logs that are returned from a query  | The maximum number of results that are returned from {{site.data.keyword.frequent-search}} is 12.000 log lines. |
{: caption="Limitations running a query on data in Priority Insights" caption-side="bottom"}

Once a limit is reached, a warning message is displayed. Refine your query results to avoid reaching a limit.
{: important}



## Keyword data type in search queries
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
