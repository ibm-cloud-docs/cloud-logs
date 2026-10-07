---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-07"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


#  Querying data by using the API
{: #query-data-api}

In {{site.data.keyword.logs_full_notm}}, you can query your log data by using Lucene queries, DataPrime queries, or by querying directly data from an {{site.data.keyword.cos_full_notm}} (COS) bucket. You can also apply filters to your queries.
{: shortdesc}


Run DataPrime or Lucene queries directly from your code


Filtering can be used in conjunction with searching using Lucene or DataPrime.

After you define a query, you can save it for later reuse by creating a view. For more information, see [Creating custom views](/docs/cloud-logs?topic=cloud-logs-custom_views&interface=ui#create_view).

## Submit a background query to be processed asynchronously.
{: #query-data-api-background-query}

[Submit a background query to be processed asynchronously](/docs/apis/logs-service-api#submit-background-query)

Submits a query that runs in the background, allowing the client to continue without waiting for the results immediately.

POST /v1/background_query

curl -X POST --location --header "Authorization: Bearer ${iam_token}"   --header "Accept: application/json"   --header "Content-Type: application/json"   --data '{ "query": "source logs | filter $d.apiVersion == 42", "syntax": "dataprime_utf8_base64" }'   "${base_url}/v1/background_query"


## Run a query to search the logs
{: #query-data-api-search-logs}

Run a query to search the logs. Note that this is a SSE (Server Sent Events) API and the content type of the response is text/event-stream

curl -X POST --location --header "Authorization: Bearer ${iam_token}"   --header "Accept: text/event-stream"   --header "Content-Type: application/json"   --data   '{
    "metadata": {
      "end_date": "2024-05-02T22:47:12.940Z",
      "limit": 100,
      "start_date": "2024-05-01T20:47:12.940Z",
      "strict_fields_validation": false,
      "syntax": "dataprime",
      "tier": "frequent_search"
    },
    "query": "source logs | limit 10"
  }'   "${base_url}/v1/query"
  
https://cloud.ibm.com/apidocs/logs-service-api#query    synchronous
The maximum number of results that are returned from Priority insights is 12 K.
The maximum number of results that are returned from IBM Cloud Object Storage (from a query using All Logs) is 50 K.
10 queries per minute limitationhttps://cloud.ibm.com/apidocs/logs-service-api#submit-background-query   --> asynchronous
up to 1 million records


# API and background query limitations
{: #query-data-api-query-limitations}

## Direct query limitations[​](#direct-query-limitations "Direct link to Direct query limitations")
{: #query-data-api-direct-query-limitations}

Coralogix places certain limitations on direct query responses. Warnings are returned when a limit is breached.

### Results returned[​](#results-returned "Direct link to Results returned")
{: #query-data-api-results-returned}

You can control the number of results returned in two ways:

* The `limit` clause in your query — for example, `source logs | limit 5000`.
* The `limit` field in the request `metadata`.

The total rows returned is the **smaller of**: any `| limit N` in your query, the `metadata.limit` field, and the tier's hard limit. If you provide no limit at all, you get the **soft limit** of 2,000 rows regardless of tier.

| Tier                              | Soft limit (no `limit` set) | Hard limit (with `limit` set) |
| --------------------------------- | --------------------------- | ----------------------------- |
| High (default when tier is unset) | 2,000 rows                  | 15,000 rows                   |
| Archive                           | 2,000 rows                  | 50,000 rows                   |


For Archive-tier queries against object storage, see [S3 Archive](https://coralogix.com/docs/docs/user-guides/data-flow/s3-archive/connect-s3-archive/.md).

### Bytes scanned limit[​](#bytes-scanned-limit "Direct link to Bytes scanned limit")
{: #query-data-api-scanned-limit}

The number of **bytes scanned** is limited as follows:

* **High tier:** 100 MB for [OpenSearch](https://coralogix.com/docs/docs/user-guides/visualizations/hosted-opensearch-view/opensearch-api/.md) queries. This applies to **fetching** 100 MB of high-tier data — it does **not** limit the scanning within the database storage.
* **Archive tier:** archive scan limit is derived from your team's quota.

### Rate limit[​](#rate-limit "Direct link to Rate limit")
{: #query-data-api-rate-limit}

Direct query requests are capped at **30 per minute**.

## Background query limitations[​](#background-query-limitations "Direct link to Background query limitations")
{: #query-data-api-background-query-limitations}

When performing background queries—whether via the Coralogix platform or by using the API—you may encounter a number of system-enforced limits or errors. These are typically related to data volume, storage access, or execution time. The table below outlines the most common error codes and messages you might receive, along with explanations and guidance to help you understand and resolve them effectively.

| Error                                                                                                                       | Explanation                                                             | Description                                                                                                                                                                            |
| --------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "[MAX\_RESULTS](https://coralogix.com/docs/docs/dataprime/language-reference/limitations/.md#max-query-results)"            | "Max results is 1000000. Refine your query."                            | The query exceeded the maximum number of rows allowed for a single response. This usually indicates that the result set is too large; try reducing the time range or applying filters. |
| "[SCANNED\_BYTES\_LIMIT](https://coralogix.com/docs/docs/dataprime/language-reference/limitations/.md#scanned-bytes-limit)" | "Scanned bytes limit has been reached."                                 | The query attempted to scan more data than permitted by your tier or plan. Reduce the data scope, apply filters, or request access to higher query limits.                             |
| "[BLOCK\_LIMIT](https://coralogix.com/docs/docs/dataprime/language-reference/limitations/.md#block-limit)"                  | "Blocks limit has been reached."                                        | Too many data blocks were involved in processing the query. This often results from querying a large time range or high-cardinality data. Consider narrowing the query scope.          |
| "METASTORE\_DATA\_MISSING"                                                                                                  | "No data exists in your object storage bucket for the given timeframe." | The query timeframe points to archived storage, but there is no available metadata for this period. Check that logs were archived and the dates are correct.                           |
| "BUCKET\_ACCESS\_DENIED"                                                                                                    | "Access to bucket denied."                                              | The background query engine was unable to access the specified object storage bucket due to permission issues. Verify your integration or cloud storage access settings.               |
| "BUCKET\_READ\_FAILED"                                                                                                      | "Failed to read from bucket."                                           | A general I/O error occurred while attempting to read archived data. This may be due to connectivity, permissions, or a corrupted file.                                                |
| "BUCKET\_MISSING\_DATA"                                                                                                     | "Data partially missing from bucket."                                   | Some of the expected data blocks could not be found or read from your object store. Results may be incomplete.                                                                         |
| "SCROLL\_TIMEOUT"                                                                                                           | "Scroll timed out."                                                     | The server took too long to scroll through the result set, usually due to large volumes or resource constraints. Try running a smaller or more efficient query.                        |

### Rate limits[​](#rate-limits "Direct link to Rate limits")
{: #query-data-api-rate-limits}

Each background query API endpoint has its own rate limit:

| Endpoint                    | Limit                                                          |
| --------------------------- | -------------------------------------------------------------- |
| Submit a background query   | 100 requests per minute (queue admission, not query execution) |
| Cancel a background query   | 50 requests per minute                                         |
| Get background query status | 50 requests per minute                                         |
| Get background query data   | 30 requests per minute                                         |

## Deleting background queries[​](#deleting-background-queries "Direct link to Deleting background queries")
{: #query-data-api-delete-queries}

Background queries cannot be manually deleted, but they automatically expire after 30 days. If a background query is canceled, all associated data will be deleted immediately. However, the query's metadata will persist for 30 days.

## Queued background queries[​](#queued-background-queries "Direct link to Queued background queries")
{: #query-data-api-queued-queries}

A maximum queue of 50 background queries is allowed. When this limit is reached, new queries cannot be added to the queue until your team’s quota rises above zero.

## Execution time limitations[​](#execution-time-limitations "Direct link to Execution time limitations")
{: #query-data-api-time-limitations}

Queries are limited to a maximum execution time of 30 minutes for background queries.
