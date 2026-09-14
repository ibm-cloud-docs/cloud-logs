---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Filtering log data
{: #query-data-filter}

In {{site.data.keyword.logs_full_notm}}, filter data by configuring filters through the UI when you run a Lucene or a Dataprime query. You can also add filters by adding the `filter` command in Dataprime queries.
{: shortdesc}

Filtering can be used in conjunction with searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).
{: tip}


## Specifying filters through the UI
{: #query-data-filter-ui}

You can apply filters to a Lucene or Dataprime query in a view by choosing 1 or more filters that reduce the data that is processed by the query. You can also apply filters to a query that is configured for a widget in a custom dashboard.

By default, in the *Logs* page, filters for metadata information are displayed: `Application`, `Subsystem`, and `Severity`. For widgets, you must add and configure filters including the ones to filter metadata.

You can add additional filters by clicking **Add Filter**.
- The list of values for a field that you choose as a filter can be displayed by expanding or collapsing the filter.
- You can select the filter values to be included in the view. You can select individual values, **SELECT ALL**, or **UNSELECT ALL**.


## Specifying filters by using the filter command
{: #query-data-filter-1}

Add explicit filter clauses or grep conditions early in your DataPrime Query Assistance or search bar to reduce the working data set before running transformations.

For example, the following sample shows a filter condition before an aggregation expression:

```text
source logs
| filter $d.action == 'create'
| groupby $d.path aggregate count()
```
{: codeblock}

For more information, see [filter command](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#filter).
