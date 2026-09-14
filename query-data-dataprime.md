---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Querying data by using DataPrime in {{site.data.keyword.logs_full_notm}}
{: #query-data-dataprime}

In {{site.data.keyword.logs_full_notm}}, you can search log data by using DataPrime.
{: shortdesc}

Dataprime is an advanced query language that filters, transforms, and aggregates data by using commands that are combined by using the pipe (`|`) operator and applied sequentially.

Use Dataprime queries to filter, transform, and aggregate data by using commands that help you manipulate log records with a language that offers full expression support similar to programming languages.

Searching can be used in conjunction with [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter) and [limiting by time](/docs/cloud-logs?topic=cloud-logs-query-data-time).
{: tip}

## Building a Dataprime query in {{site.data.keyword.logs_full_notm}}
{: #query-data-dataprime-query}

You can define a Dataprime query using the following format:

```text
source logs | operator1 ... | operator2 ... | operator3 | ...
```
{: codeblock}

Any whitespace between operators is ignored.

A pipe character (`|`) is used to chain sequential operations, passing transformed or filtered data from one step to the next in a pipeline.

You can also define Dataprime queries across multiple lines:

```text
source logs |
operator1 .... |
operator2 .... |
operator3 ....
```
{: codeblock}

Operators are commands that transform unstructured streams of JSON data to create a new stream for a specified time period. Examples include: `filter`, `extract`, `sortby`, `groupby`, `orderby`, `find`, and `choose`.

For more information about DataPrime operators, see the [DataPrime operators](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators).

## Running a Dataprime query in the Logs page in {{site.data.keyword.logs_full_notm}}
{: #query-data-dataprime-ui}

You can run a Dataprime query in the **Explore Logs > Logs** page.

Complete the following steps to run a query in the *Logs* page in {{site.data.keyword.logs_full_notm}}:

1. [Launch the IBM Cloud Logs UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the *Explore logs icon* icon ![Explore logs icon](/icons/explore.svg). Then select **Logs**.

    By default, **Priority Insights** is selected.

    If you want to explore data from the COS bucket, click **Archive**.

3. In the query section, select **</> DataPrime** to specify your search to be a DataPrime query.

    By default, the search query mode is set to **Lucene**.

4. Enter a Dataprime query. Then, click the ![Play icon](/icons/play.png) to run your query.

    For more information, see [Building a Dataprime query in {{site.data.keyword.logs_full_notm}}](#query-data-dataprime-query).

If you are searching in {{site.data.keyword.frequent-search}} and you are not seeing the data you expect, see [Why am I not seeing results from my Priority insights searches?](/docs/cloud-logs?topic=cloud-logs-ts-mapping-exceptions).
{: note}


## Running a Dataprime query in a custom dashboard widget in {{site.data.keyword.logs_full_notm}}
{: #query-data-dataprime-widget}

You can run a Dataprime query in the **Dashboards > Custom Dashboards** page.

Complete the following steps to run a query in the *Custom Dashboards* page in {{site.data.keyword.logs_full_notm}}:

1. [Launch the IBM Cloud Logs UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the *Dashboards icon* icon ![Dashboards icon](/icons/dashboards.svg). Then select **Custom Dashboards**.

3. Create a new dashboard and add a widget. You can also add a widget to an existing dashboard.

4. In the widget's configuration panel, select **Dataprime**.

    ![Dataprime query in a custom dashboard](/images/query-dashboard-dataprime.png)

5. Enter a Dataprime query.

    For more information, see [Building a Dataprime query in {{site.data.keyword.logs_full_notm}}](#query-data-dataprime-query).

If you are searching in {{site.data.keyword.frequent-search}} and you are not seeing the data you expect, see [Why am I not seeing results from my Priority insights searches?](/docs/cloud-logs?topic=cloud-logs-ts-mapping-exceptions).
{: note}
