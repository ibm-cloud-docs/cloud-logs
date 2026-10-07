---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-07"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Querying data by using Lucene in {{site.data.keyword.logs_full_notm}}
{: #query-data-lucene}

{{site.data.keyword.logs_full_notm}} log data can be searched using Lucene. Lucene is a text-based query language that you can use to search and filter data. It splits search strings into fields, terms, and operators. Use Lucene to query by using key value pairs or to run free-text searches.
{: shortdesc}

Searching can be used in conjunction with [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter) and [limiting by time](/docs/cloud-logs?topic=cloud-logs-query-data-time).
{: tip}


## Lucene queries
{: #query-data-lucene-query}

A Lucene query is composed of *Terms* and *Operators*. Terms are extracted from the log data by the analyzer. There are two types of terms:

Single terms
:   This is a word in a text field.

Phrase
:   This is a group of words enclosed in double quotation marks (").

## Running a Lucene query in the Logs page in {{site.data.keyword.logs_full_notm}}
{: #query-data-lucene-ui}

You can run a Lucene query in the **Explore Logs > Logs** page.

Complete the following steps to run a query in the *Logs* page in {{site.data.keyword.logs_full_notm}}:

1. [Launch the IBM Cloud Logs UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the *Explore logs icon* icon ![Explore logs icon](/icons/explore.svg). Then select **Logs**.

    By default, **Priority Insights** is selected.

    If you want to explore data from the COS bucket, click **All Logs**.

3. In the query section, select **</> Lucene** to specify your search to be a Lucene query.

    By default, the search query mode is set to **Lucene**.

4. Enter a Lucene query. Then, click the ![Play icon](/icons/play.png) to run your query.

    In the search field specify your search in [Lucene format](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: external}.

    For more information, see [Building a Lucene query in {{site.data.keyword.logs_full_notm}}](#query-data-lucene-query).

If you are searching in {{site.data.keyword.frequent-search}} and you are not seeing the data you expect, see [Why am I not seeing results from my Priority insights searches?](/docs/cloud-logs?topic=cloud-logs-ts-mapping-exceptions).
{: note}


## Running a Lucene query in a custom dashboard widget in {{site.data.keyword.logs_full_notm}}
{: #query-data-lucene-widget}

You can run a Lucene query in the **Dashboards > Custom Dashboards** page.

Complete the following steps to run a query in the *Custom Dashboards* page in {{site.data.keyword.logs_full_notm}}:

1. [Launch the IBM Cloud Logs UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the *Dashboards icon* icon ![Dashboards icon](/icons/dashboards.svg). Then select **Custom Dashboards**.

3. Create a new dashboard and add a widget. You can also add a widget to an existing dashboard.

4. In the widget's configuration panel, select **Lucene**.

    ![Lucene query in a custom dashboard](/images/query-dashboard-Lucene.png)
    {: #query-data-lucene-query}

5. Enter a Lucene query.

    In the search field specify your search in [Lucene format](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: external}.

    For more information, see [Building a Lucene query in {{site.data.keyword.logs_full_notm}}](#query-data-Lucene-query).

If you are searching in {{site.data.keyword.frequent-search}} and you are not seeing the data you expect, see [Why am I not seeing results from my Priority insights searches?](/docs/cloud-logs?topic=cloud-logs-ts-mapping-exceptions).
{: note}


## Types of searches
{: #query-data-lucene-search-types}

{{site.data.keyword.logs_full_notm}} provides the following search types:

Free text search
:   A free text search is used to match terms in any field in your log data. Enclose the text in double quotation marks (").

Field search
:   A field search restricts the search to the specific field that must match your search term. Enclose the text in double quotation marks (").

Range search
:   A range search lets you query a range of matching numeric values.

Regex search
:   Regex searches let you use regular expressions to match patterns within your log data. [Lucene standard operators](https://www.elastic.co/guide/en/elasticsearch/reference/8.4/regexp-syntax.html#regexp-standard-operators){: external} are supported.

    Regex patterns to be matched need to be enclosed in forward slashes (`/`).

    Whenever possible use regex searches against keywords since keywords are not passed through the analyzer.
    {: tip}

## Example searches
{: #query-data-lucene-query-examples}

The following are examples of different types of searches and their results.

| Query | Results |
|-------|---------|
| `a very interesting log message` | Matches logs containing these terms. They can appear in any field and in any order. |
| `"a very interesting log message"` | Matches this exact phrase in any field. |
{: caption="Example free text searches" caption-side="bottom"}

| Query | Results |
|-------|---------|
| `msg:interesting` | Matches logs containing this term in the msg field. |
| `msg:"a very interesting log message!"` |	Matches the exact phrase in the msg field. |
| `msg.keyword:"a very interesting message!"` | Matches logs that contain the phrase (including the !). |
| `msg.keyword:/.*/ AND NOT msg.keyword:/^$/` | Matches logs where the field has a value and is not an empty string ("") |
{: caption="Example field searches" caption-side="bottom"}

| Query | Results |
|-------|---------|
| `status_code.numeric:[200 TO 299]` | Matches status codes between 200 and 299 (including 200 and 299). |
| `status_code.numeric:{199 TO 300}` | Matches status codes between 200 and 299 (excluding 199 and 300). |
| `status_code.numeric:[200 TO 300}` | Matches status codes between 200 and 299 (including 200 but excluding 300). |
| `status_code.numeric:{199 TO 299]` | Matches status codes between 200 and 299 (excluding 199 but including 299). |
| `status_code.numeric:<300` | Matches status codes less than 300 (not including 300). |
| `status_code.numeric:>0.003` | Matches status codes greater than 0.003 (not including 0.003). |
{: caption="Example range searches" caption-side="bottom"}

| Query | Results |
|-------|---------|
| `msg.keyword:/.*what an interesting message!.*/` | Matches logs that contain the pattern "what an interesting message!" (including the !). |
| `version.keyword:/.*v.[1-5].[0-9]{2}.*/` | Matches logs that contain patterns like "v.1.24" or "v.5.69" in the version field. |
{: caption="Example regex searches" caption-side="bottom"}

| Query | Results |
|-------|---------|
| `FirewallMatchesActions:"abc" OR FirewallMatchesActions:"123"` | Matches logs containing the exact strings `abc` or `123`. |
| `FirewallMatchesActions.keyword:/(abc\|123)/` | Matches logs containing the exact strings `abc` or `123` by using regex. |
| `FirewallMatchesActions.keyword:/.*(abc\|123).*/` | Matches logs with strings containing the partial strings `abc` or `123` by using regex. |
{: caption="Example array searches" caption-side="bottom"}

## Types of operators
{: #lucene-operators}

You can use the operators `AND`, `OR`, and `NOT` to combine multiple filters. You can also use parenthesis to specify operator precedence when you have multiple operators in a query.

| Query | Results |
|-------|---------|
| `msg:"failed transaction" AND level: "ERROR" NOT env:"staging"` |	Matches ERROR level logs that contain the phrase "failed transaction" but not from the "staging environment". |
| `(msg:"failed transaction" AND (cluster:"eu" OR cluster:"us")) NOT env:"staging"` | Matches logs from the "eu" or "us" clusters that contain the phrase "failed transaction" but not from the "staging environment". |
{: caption="Example queries using operators" caption-side="bottom"}
