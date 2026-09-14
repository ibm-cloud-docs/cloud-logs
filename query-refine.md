---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Refining query results in {{site.data.keyword.logs_full_notm}}
{: #query-refine}

In {{site.data.keyword.logs_full}}, you can refine a query by adding filters, narrowing timeframes, and using exact matches.
{: shortdesc}

Checklist for refining a query in {{site.data.keyword.logs_full_notm}}:
1. Add filters first to a Dataprime query in {{site.data.keyword.logs_full_notm}} to reduce the amount of data that is processed as part of the query and before you add aggregation expressions or transformation functions.
2. Shorten the default time range in the *Explore Logs* page or inside the query code to minimize scan volume and speed up troubleshooting.

## Reduce the data resultset by adding filters to a query in {{site.data.keyword.logs_full_notm}}
{: #query-refine-1}
{: step}

Add explicit filter clauses or grep conditions early in your DataPrime Query Assistance or search bar to reduce the working data set before running transformations.

For example, the following sample shows a filter condition before an aggregation expression:

```text
source logs
| filter $d.action == 'create'
| groupby $d.path aggregate count()
```
{: codeblock}


## Narrow the timeframe of a query in {{site.data.keyword.logs_full_notm}}
{: #query-refine-2}
{: step}

Shorten the default time range in the *Explore Logs* page or inside the query code to minimize scan volume and speed up troubleshooting.

Querying large time ranges (weeks or months) increases scan volume and slows results. Reduce your time window when troubleshooting:

    Use the time picker to select only what’s necessary.
    Use relative time queries where applicable.


## Use exact matches in a query in {{site.data.keyword.logs_full_notm}}
{: #query-refine-3}

Use exact matches: Swap fuzzy matching out for direct key comparisons (e.g., filter my.key == 'hello') to let the engine take advantage of indexing for faster execution. [1] (https://coralogix.com/docs/dataprime/user-guide/foundations/troubleshooting/)


## Replace Dataprime dynamic transformations with parsing rules in {{site.data.keyword.logs_full_notm}}
{: #query-refine-4}

Avoid expensive transformations during querying

DataPrime supports dynamic transformations, but these come at a performance cost. Move complex formatting or parsing into Parsing Rules during ingestion to reduce query-time processing.

##

“Scan limit exceeded”

You’ve hit the scan cap for your query. This is a guardrail to prevent excessive resource usage.
Fixes:

    Switch to “All Logs Mode” or “All Traces Mode”: These modes query your full archive (e.g., S3) where scan limits are much higher.
    Simplify your query: Remove unnecessary transformations, filters, or nested expressions that force full scans.
