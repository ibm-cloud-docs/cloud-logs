---

copyright:
  years:  2023, 2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Querying data by using Lucene
{: #query-data-lucene}

{{site.data.keyword.logs_full_notm}} log data can be searched using Lucene or DataPrime. For information on querying with DataPrime, see [Querying data by using DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).
{: shortdesc}

Searching can be used in conjunction with [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter) and [limiting by time](/docs/cloud-logs?topic=cloud-logs-query-data-time).
{: tip}


{{site.data.content.query-ui}}

## Using Lucene
{: #use-lucene}

1. Use the **< > Lucene**/**< > DataPrime** switch to change the search type to **Lucene**.

2. In the search field specify your search in [Lucene format.](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: external}

3. Click the arrow at the end of the field run your query.

## Lucene queries
{: #lucene-query}

A Lucene query is composed of *Terms* and *Operators*. Terms are extracted from the log data by the analyzer. There are two types of terms:

Single terms
:   This is a word in a text field.

Phrase
:   This is a group of words enclosed in double quotation marks (").

## Types of searches
{: #search-types}

{{site.data.keyword.logs_full_notm}} provides the following search types:

Free text search
:   A free text search is used to match terms in any field in your log data.

Field search
:   A field search restricts the search to the specific field that must match your search term.

Range search
:   A range search lets you query a range of matching numeric values.

Regex search
:   Regex searches let you use regular expressions to match patterns within your log data. [Lucene standard operators](https://www.elastic.co/guide/en/elasticsearch/reference/8.4/regexp-syntax.html#regexp-standard-operators){: external} are supported.

    Regex patterns to be matched need to be enclosed in forward slashes (`/`).

    Whenever possible use regex searches against keywords since keywords are not passed through the analyzer.
    {: tip}

## Example searches
{: #search-examples}

The following are examples of different types of searches and their results.

| Query | Results |
|-------|---------|
| `a very interesting log message` | Matches logs containing these terms. They can appear in any field and in any order. |
| `“a very interesting log message”` | Matches this exact phrase in any field. | 
{: caption="Example free text searches" caption-side="bottom"}

| Query | Results |
|-------|---------|
| `msg:interesting` | Matches logs containing this term in the msg field. |
| `msg:“a very interesting log message!”` |	Matches the exact phrase in the msg field. |
| `msg.keyword:”a very interesting message!”` | Matches logs that contain the phrase (including the !). |
{: caption="Example field searches" caption-side="bottom"}

| Query | Results |
|-------|---------|
| `status_code.numeric:[200 TO 299]` | Matches status codes between 200 and 299 (including 200 and 299). |
| `status_code.numeric:{199 TO 300}` | Matches status codes between 200 and 299 (excluding 199 and 300). |
| `status_code.numeric:[200 TO 300}` | Matches status codes between 200 and 299 (including 200 but excluding 300). |
| `status_code.numeric:{199 TO 299]` | Matches status codes between 200 and 299 (excluding 199 but including 299). |
{: caption="Example range searches" caption-side="bottom"}

| Query | Results |
|-------|---------|
| `msg.keyword:/.*what an interesting message!.*/` | Matches logs that contain the pattern “what an interesting message!” (including the !). |
| `version.keyword:/.*v.[1-5].[0-9]{2}.*/` | Matches logs that contain patterns like “v.1.24” or “v.5.69” in the version field. |
{: caption="Example regex searches" caption-side="bottom"}


## Types of operators
{: #lucene-operators}

You can use the operators `AND`, `OR`, and `NOT` to combine multiple filters. You can also use parenthesis to specify operator precedence when you have multiple operators in a query.

| Query | Results |
|-------|---------|
| `msg:”failed transaction” AND level: “ERROR” NOT env:”staging”` |	Matches ERROR level logs that contain the phrase “failed transaction” but not from the “staging environment”. |
| `(msg:”failed transaction” AND (cluster:”eu” OR cluster:”us”)) NOT env:”staging”` | Matches logs from the “eu” or “us” clusters that contain the phrase “failed transaction” but not from the “staging environment”. |
{: caption="Example queries using operators" caption-side="bottom"}


{{site.data.content.query-reset}}


{{site.data.content.save-view}}
