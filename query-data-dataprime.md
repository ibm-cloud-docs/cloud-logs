---

copyright:
  years:  2023, 2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Querying data by using DataPrime
{: #query-data-dataprime}

{{site.data.keyword.logs_full_notm}} log data can be searched using DataPrime or Lucene. For information on querying with Lucene, see [Querying data by using Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene).
{: shortdesc}

Searching can be used in conjunction with [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter) and [limiting by time](/docs/cloud-logs?topic=cloud-logs-query-data-time).
{: tip}

<!-- Acessing the Explore UI -->
{{site.data.content.query-ui}}

## Using DataPrime
{: #use-dataprime}

1. Use the **< > Lucene**/**< > DataPrime** switch to change the search type to **DataPrime**.

2. In the search field specify your search in DataPrime format.

   See the [DataPrime reference](/docs/cloud-logs?topic=cloud-logs-dataprime-ref) for operators and expressions that can be used when querying logs.

3. Click the arrow at the end of the field run your query.

<!-- Query reset -->
{{site.data.content.query-reset}}

<!-- Save view -->
{{site.data.content.save-view}}
