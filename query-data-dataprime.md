---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Querying data by using DataPrime
{: #query-data-dataprime}

In {{site.data.keyword.logs_full_notm}}, you can search log data by using DataPrime.
{: shortdesc}

Dataprime is an advanced query language that filters, transforms, and aggregates data by using commands that are combined by using the pipe (`|`) operator and applied sequentially.

Use Dataprime queries to filter, transform, and aggregate data by using commands that help you manipulate log records with a language that offers full expression support similar to programming languages.

Searching can be used in conjunction with [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter) and [limiting by time](/docs/cloud-logs?topic=cloud-logs-query-data-time).
{: tip}


{{site.data.content.query-ui}}

## Using DataPrime
{: #use-dataprime}

1. Use the **< > Lucene**/**< > DataPrime** switch to change the search type to **DataPrime**.

2. In the search field specify your search in DataPrime format.

   See the [DataPrime reference](/docs/cloud-logs?topic=cloud-logs-dataprime-ref) for operators and expressions that can be used when querying logs.

3. Click the arrow at the end of the field run your query.

If you are searching in {{site.data.keyword.frequent-search}} and you are not seeing the data you expect, see [Why am I not seeing results from my Priority insights searches?](/docs/cloud-logs?topic=cloud-logs-ts-mapping-exceptions).
{: tip}


{{site.data.content.query-reset}}


{{site.data.content.save-view}}
