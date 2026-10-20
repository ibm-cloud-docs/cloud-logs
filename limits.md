---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-20"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_full_notm}} limits
{: #limits}

{{site.data.keyword.logs_full}} has limits that need to be considered when using the service.
{: shortdesc}

## Character support
{: #unicode}

{{site.data.keyword.logs_full_notm}} does not provide full Unicode support for multibyte characters.

## Naming requirements when provisioning an {{site.data.keyword.logs_full_notm}} instance
{: #limits-instance-name}

When provisioning an {{site.data.keyword.logs_full_notm}} instance, the service instance name is limited to 1-256 characters in length and can only include the following characters:

* Letters (`A`-`Z`, `a`-`z`)
* Numbers (`0`-`9`)
* Period (`.`)
* Underscore (`_`)
* Hypen (`-`)
* Colon (`:`)
* Space (` `)


## Limits per instance
{: #limits-per-instance}

{{site.data.keyword.logs_full_notm}} has limits for each provisioned instance.

| Item | Limit |
|------|-------|
| Alerts | 500 |
| Parsing rules | 70 |
| Enrichments | 10 |
| Events to Metrics labels | 8 |
| Ingestion log size | 32 K |
| Largest log size processed by the pipeline | 33 K |
| Branches | 1500 |
| Query time range | 8 days |
| Maximum number of fields | 3000 |
| Number of logs that can be exported through the user interface (UI) | 5000 |
{: caption="Limits per instance" caption-side="bottom"}

## Dynamic alerts limits
{: #limit-dynamic alert}

A dynamic alert is an alert with a **More than usual** or **Less than usual** condition. Each dynamic alert is allocated 500 permutations with a maximum of 10,000 permutations allowed for any {{site.data.keyword.logs_full_notm}} instance.

The permutation limit means that a maximum of 20 dynamic alerts can be configured for an {{site.data.keyword.logs_full_notm}} instance.

You can still create other non-dynamic alerts when you have reached the 20 dynamic alerts limit.

## Log ingestion limits
{: #limit-ingestion}

When you send data to an {{site.data.keyword.logs_full_notm}} instance:
- Logs cannot be older than 24 hours.
- Logs cannot be more than 4 hours into the future.



For a single ingestion request {{site.data.keyword.logs_full_notm}}, these limitations exist:

* `request_timeout`: 30 seconds
* `request_body_limit_bytes`: 10 MiB

## Query limits
{: #limit-query}

### Characters within a query
{: #limit_query_characters}

There are limits to the number of characters that can be included in a query.

* A maximum of 3000 characters can be included in a query in the **Logs** view.

* A maximum of 65,535 characters can be included in an alert query definition. Alert query definitions are also limited to a maximum of 50 `AND` and `OR` statements.


### Keyword types
{: #limit_keyword}

Keywords represent text that does not pass through the analyzer before indexing. This data type is suitable for regular expressions, aggregation, and sorting.

The syntax to use the keyword data type in your query is: `<fieldName>.keyword`.

{{site.data.keyword.logs_full_notm}} can not create a keyword type when a field is longer than 256 characters.


### Results returned
{: #limit_returned_results}

The maximum number of rows that are returned from a query depends if you are querying from {{site.data.keyword.frequent-search}} or data that is stored in {{site.data.keyword.cos_full_notm}}.

* The maximum number of results that are returned from {{site.data.keyword.frequent-search}} is 12 K.
* The maximum number of results that are returned from {{site.data.keyword.cos_full_notm}} (from a query using *All Logs*) is 50 K.


### Bytes scanned
{: #limit_bytes_scanned}

A maximum of 100 MB is scanned for {{site.data.keyword.frequent-search}} data.



### Rate limiting
{: #limit_rate_limit}

A maximum of 10 queries per minute can be submitted via API or through the archive query feature. When the rate limit is exceeded, an HTTP 429 is returned.

## Livetail limits
{: #limit-livetail}

A Livetail view can run continuously for 10 minutes. After 10 minutes the Livetail will stop and you will need to access the Livetail again to restart the view.
