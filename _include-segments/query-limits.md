## Log query limits for Direct HTTP API Archive Query
{: #limit-query}


## Results returned
{: #limit_returned_results}

The maximum number of rows that are returned from a query depends if you are querying from {{site.data.keyword.frequent-search}} or data that is stored in {{site.data.keyword.cos_full_notm}}.

* The maximum number of results that are returned from {{site.data.keyword.frequent-search}} is 12 K.
* The maximum number of results that are returned from {{site.data.keyword.cos_full_notm}} (from a query using *All Logs*) is 50 K.


## Bytes scanned
{: #limit_bytes_scanned}

A maximum of 100 MB is scanned for {{site.data.keyword.frequent-search}} data. No limit exists when data stored in {{site.data.keyword.cos_full_notm}} is scanned.


## Rate limiting
{: #limit_rate_limit}

A maximum of 10 queries per minute can be submitted.

When the rate limit is exceeded, an HTTP 429 is returned.
