---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-28"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Querying data by using an asynchronous background query in {{site.data.keyword.logs_full_notm}}
{: #query-background}

In {{site.data.keyword.logs_full_notm}}, you can run a long-running query asynchronously by running a *Background query*. You can use DataPrime or Lucene syntax to query the data.
{: shortdesc}

This feature queries data in the {{site.data.keyword.cos_full_notm}} (COS) data bucket.
{: important}

To run a background query, you submit a query request. Once the query results are prepared and ready, you can download the results as a file using the UI, the CLI or the API at a later point in time.

Use a background query for recurring, extensive analytical tasks such as monthly or quarterly analysis.
{: tip}

## Running background queries in {{site.data.keyword.logs_full_notm}}
{: #query-background-ov}

In {{site.data.keyword.logs_full_notm}}, consider the following information:

- `startDate` and `endDate` must be valid ISO 8601 date-time strings.

    If your local time zone is not UTC, you can either convert the timestamp to UTC format such as `2026-08-07T18:20:00.00Z` or include the time zone offset as follows  `2027-08-07T11:20:00.00-07:00` for Pacific Daylight Time, or `2027-08-07T11:20:00.00+05:30` for India Standard Time.

- When the query timeframe is half-open, `[startDate, endDate)`, `startDate` is inclusive and `endDate` is exclusive. A record whose timestamp equals `endDate` is not returned.

- When you query archived logs using the API, you must explicitly specify the *tier* to **TIER_ARCHIVE** in the metadata object of your request. Otherwise, the default tier **TIER_FREQUENT_SEARCH** is used.

- After you submit a background query, you have 30 days to download the data.

- Background queries that are older than 30 days are automatically removed from the instance.

- You can list all background queries through the UI in **Explorer > Archive Query**.

- When you create a background query through the CLI or API, the query ID is part of the name of the query. For example, in this query `background_query_d840dad0-2b2c-41df-89aa-c1faabc8c275`, the value `d840dad0-2b2c-41df-89aa-c1faabc8c275` is the query ID that you must use to check its status, cancel the query, or download the data.

- With the background query, you can get up to 1M records.

- You cannot delete background queries. They automatically expire after 30 days.

- You can submit a maximum of 50 background queries. When this limit is reached, new queries cannot be submitted until existing ones expire.

- Each query is limited to a maximum execution time of 30 minutes.

- If you cancel a background query, you cannot access partial data. However, the query's metadata will persist for 30 days and count towards the total number of queries that you can submit.


## Managing background queries through the CLI in {{site.data.keyword.logs_full_notm}}
{: #query-background-ov-cli}
{: cli}

The following table lists the CLI commands that you can use to manage background queries:

| Command                                  | Description |
|------------------------------------------|-------------|
| `background-query-create` (`bgq-create`) | Submit a background query to be processed asynchronously. |
| `background-query-status` (`bgq-status`) | Get the status of a background query. |
| `background-query-data`   (`bgq-data`)   | Get the data of the background query. |
| `background-query-cancel` (`bgq-cancel`) | Cancel a background query. This request stops a query that is running in the background. |
{: caption="{{site.data.keyword.logs_full_notm}} background query (asynchronous archive query) CLI commands" caption-side="bottom"}

You can run the `ibmcloud cloud-logs background-query-create` command to run a query asynchronously.

After you submit a background query, you can check the status of the query by running the command `ibmcloud cloud-logs background-query-status`.

If you need to stop a query that is still running, you can run the command `ibmcloud cloud-logs background-query-cancel`.

If you want to download the data, you can run the command `ibmcloud cloud-logs background-query-data`.

When you create a background query through the CLI or API, the query ID is part of the name of the query. For example, in this query `background_query_d840dad0-2b2c-41df-89aa-c1faabc8c275`, the value `d840dad0-2b2c-41df-89aa-c1faabc8c275` is the query ID that you must use to check its status, cancel the query, or download the data. To see the IDs of background queries that you have requested via API, go to UI and select **Explore logs > Archive Query**.
{: tip}

### ibmcloud logs background-query-create
{: #query-background-create-cli}
{: cli}

Use the `ibmcloud cloud-logs background-query-create` command to submit a query that runs asynchronously in the background.

```sh
ibmcloud cloud-logs background-query-create --query QUERY --syntax SYNTAX [--start-date START-DATE] [--end-date END-DATE] [--now-date NOW-DATE] --service-url URL
```
{: codeblock}

Where
- `QUERY` represents the background query to run asynchronously.

    The maximum length is 4096 characters.

    The minimum length is 1 character.

- `SYNTAX` represents the query language syntax. Valid values are: `unspecified`, `lucene`, `dataprime`, `lucene_utf8_base64`, `dataprime_utf8_base64`.

    To avoid SQL injection detection false positives, set the syntax parameter to `lucene_utf8_base64` or `dataprime_utf8_base64`. DataPrime queries look a bit like SQL queries and they might be treated as SQL.  You must encode the query string.{: important}

- `END-DATE` represents the end of the time range for the query.

    The default value is set to `start + 15 minutes` or `current time` if start is not defined.

- `START-DATE` represents the beginning of the time range for the query.

    The default value is set to `end - 15 minutes` or `current time - 15 minutes` if end is not defined.

- `NOW-DATE` represents the current time.

    You can set this parameter to substitute `now()` in a DataPrime query.

- `URL` represents the base endpoint URL `https://{API_endpoint}` for the API. For more information, see [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).


For example, this is a sample command:

```sh
ibmcloud cloud-logs background-query-create \
    --query 'source logs | filter $d.apiVersion == 42' \
    --syntax dataprime_utf8_base64 \
    --start-date 2026-07-05T13:15:30.000Z \
    --end-date 2026-07-05T13:15:30.000Z \
    --now-date 2023-11-05T13:15:30.000Z
```
{: codeblock}


### ibmcloud logs background-query-data
{: #query-background-data-cli}
{: cli}

Use this command to download the data returned from running a background query.

```sh
ibmcloud cloud-logs background-query-data --query-id QUERYID --service-url URL
```
{: codeblock}

Where
- `QUERYID` is the query ID that is assigned to the query when you run the command `ibmcloud cloud-logs background-query-create`. The maximum length is 36 characters. The minimum length is 36 characters.

- `URL` represents the base endpoint URL `https://{API_endpoint}` for the API. For more information, see [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).


### ibmcloud logs background-query-status
{: #query-background-status-cli}
{: cli}

Use this command to get the running status of a background query.

```sh
ibmcloud cloud-logs background-query-status --query-id QUERYID --service-url URL
```
{: codeblock}

Where
- `QUERYID` is the query ID that is assigned to the query when you run the command `ibmcloud cloud-logs background-query-create`. The maximum length is 36 characters. The minimum length is 36 characters.

- `URL` represents the base endpoint URL `https://{API_endpoint}` for the API. For more information, see [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).



### ibmcloud logs background-query-cancel
{: #query-background-cancel-cli}
{: cli}

Use this command to cancel a background query that is running.

```sh
ibmcloud cloud-logs background-query-cancel --query-id QUERYID --service-url URL
```
{: codeblock}

Where
- `QUERYID` is the query ID that is assigned to the query when you run the command `ibmcloud cloud-logs background-query-create`. The maximum length is 36 characters. The minimum length is 36 characters.

- `URL` represents the base endpoint URL `https://{API_endpoint}` for the API. For more information, see [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).



## Managing background queries through the UI in {{site.data.keyword.logs_full_notm}}
{: #query-background-ov-ui}
{: ui}

In the UI, you can manage background queries that are created in the UI, by using the CLI or through the API.

After you run a background query, you can view your results through the **Logs Preview** or the **Download TSV** options.


### Creating a background query in {{site.data.keyword.logs_full_notm}}
{: #query-background-create-ui}
{: ui}

Complete the following steps to create a background query:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Archive Query**.

3. Select **Archive Query**.

4. In the *Details* section, enter a name and a description.

    The query name must consist only of lowercase letters, with optional numbers and underscores. It cannot begin with a number or an underscore.

5. In the *Filters* section, enter the following information:

    Enter the Lucene or DataPrime query.

    Select the time range.

    Add filters by application, subsystem and severity.

6. Click **Run archive query**.


### Viewing a preview of the results in {{site.data.keyword.logs_full_notm}}
{: #query-background-preview-ui}
{: ui}

After you run a background query, you can view a preview of the results through **Logs Preview**.

Complete the following steps to see a preview of the results from a background query:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Archive Query**.

3. Select **Results preview**. A new window opens where you can see the data. From this new window, you can also download the data.




### Download the results in {{site.data.keyword.logs_full_notm}}
{: #query-background-download-ui}
{: ui}

After you run a background query, you can download the results through the option **Download TSV**.

Complete the following steps to download the data from running a background query:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Archive Query**.

3. Select **Download TSV**. The file downloads locally.




### Cloning a background query in {{site.data.keyword.logs_full_notm}}
{: #query-background-clone-ui}
{: ui}

If you need to modify an existing background query, you can duplicate a query configuration and modify it by selecting **Clone**.

Complete the following steps to clone a background query:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Archive Query**.

3. Select **Clone**.

4. Modify any data.

5. Click **Run archive query**.



## Managing background queries through the API in {{site.data.keyword.logs_full_notm}}
{: #query-background-ov-api}
{: api}

The following table lists the API methods that you can use to manage background queries in {{site.data.keyword.logs_full_notm}}:

| Command                                  | Description | More info |
|------------------------------------------|-------------|-----------|
| `POST ${URL}/v1/background_query` | Submit a background query to be processed asynchronously. | [Submit a background query](/docs/apis/logs-service-api#submit-background-query) |
| `GET ${URL}/v1/background_query/{query_id}/status` | Get the status of a background query. | [Get the status of a background query](/docs/apis/logs-service-api#get-background-query-status) |
| `GET ${URL}/v1/background_query/{query_id}/data`  | Get the data of the background query. | [Get the data of a background query](/docs/apis/logs-service-api#get-background-query-data) |
| `POST ${URL}/v1/background_query/{query_id}/cancel` | Cancel a background query. This request stops a query that is running in the background. | [Cancel a background query](/docs/apis/logs-service-api#cancel-background-query) |
{: caption="{{site.data.keyword.logs_full_notm}} background query (asynchronous archive query) API methods" caption-side="bottom"}


When you create a background query through the CLI or API, the query ID is part of the name of the query. For example, in this query `background_query_d840dad0-2b2c-41df-89aa-c1faabc8c275`, the value `d840dad0-2b2c-41df-89aa-c1faabc8c275` is the query ID that you must use to check its status, cancel the query, or download the data. To see the IDs of background queries that you have requested via API, go to UI and select **Explore logs > Archive Query**.
{: tip}

### API endpoint for background queries in {{site.data.keyword.logs_full_notm}}
{: #query-background-api-endpoint}
{: api}

The following table outlines the endpoint details in background queries in {{site.data.keyword.logs_full_notm}}:

| Detail                  | Value |
|-------------------------|-------|
| `URL`                   | `<INSTANCE_ID>.api.<REGION>.logs.cloud.ibm.com/logs/v1/background_query` |
| Header `Content-Type`   | `application/json`|
| Header `Authorization`  | `Bearer $IAM_TOKEN`|
| Header `Accept`         | `application/json` |
{: caption="API endpoint details" caption-side="top"}

Where

- `INSTANCE_ID`: GUID of the {{site.data.keyword.logs_full_notm}} instance where you want to run the background query.
- `REGION`: Region where the {{site.data.keyword.logs_full_notm}} instance is located.
- `IAM_TOKEN`: [IAM bearer token](/docs/cloud-logs?topic=cloud-logs-send-logs-api#send-logs-token) used to request authorization to run a background query.

### Retrieving an access token when using the API in {{site.data.keyword.logs_full_notm}}
{: #query-background-api-token}
{: api}

You can retrieve your access token programmatically by first creating a [service ID API key](/docs/iam?topic=iam-serviceidapikeys&interface=ui){: external} for your application, and then exchanging your API key for an {{site.data.keyword.cloud_notm}} IAM token. For more information, see [Retrieving an access token with the API](/docs/cloud-logs?topic=cloud-logs-retrieve-access-token&interface=api).


### Submit a background query in {{site.data.keyword.logs_full_notm}}
{: #query-background-api-submit}
{: api}


Use the following cURL command to submit a background query in {{site.data.keyword.logs_full_notm}}:

```sh
curl -X POST --location "${base_url}/v1/background_query"
--header "Authorization: Bearer $IAM_TOKEN" \
--header "Accept: application/json"  \
--header "Content-Type: application/json" \
--data '{ "query": "QUERY", "syntax": "QUERY_SYNTAX" }'
```
{: pre}

Where

- `query` defines the query to run asynchronously in the background.

    You can define a query with a maximun of 4096 characters that matches the regular expression `^[\p{L}\p{N}\p{P}\p{Z}\p{S}\p{M}]+$`.

    For example: `source logs | filter $d.apiVersion == 42`

- `syntax` define the query syntax.

    Valid values are: `unspecified`,`lucene`, `dataprime`, `lucene_utf8_base64`, `dataprime_utf8_base64`

    Queries might be misinterpreted as SQL queries when you go through a proxy server and rejected.

- `start_date` defines the beginning of the time range for the query.

    The default value is `end - 15 minutes` or `current time - 15 minutes` if end is not defined.

    For example: `2026-11-20T12:15:30.000Z`

- `end_date` defines the end of the time range for the query.

    The default value is `start + 15 minutes` or `current time` if start is not defined.

    For example: `2026-11-20T12:15:30.000Z`

- `now_date` defines Contextual now for the query,

    The defaultvalue is the current time.

    It is used by functions like `now()` in DataPrime.

    For example: `2026-11-20T12:15:30.000Z`


## Errors running background queries in {{site.data.keyword.logs_full_notm}}
{: #query-background-errors}

When you run a background query, you may encounter system-enforced limits or errors related to data volume, storage access, or execution time.

The following table outlines the most common error codes and messages you might receive:

| Error                    | Error Description                                                     |
|--------------------------|-----------------------------------------------------------------------|
| `MAX_RESULTS`            | Max results is 1000000. Refine your query.                            |
| `SCANNED_BYTES_LIMIT`    | Scanned bytes limit has been reached.                                 |
| `BLOCK_LIMIT`            | Blocks limit has been reached.                                        |
| `METASTORE_DATA_MISSING` | No data exists in your object storage bucket for the given timeframe. |
| `BUCKET_ACCESS_DENIED`   | Access to bucket denied.                                              |
| `BUCKET_READ_FAILED`     | Failed to read from bucket.                                           |
| `BUCKET_MISSING_DATA`    | Data partially missing from bucket.                                   |
| `SCROLL_TIMEOUT`         | Scroll timed out.                                                     |
{: caption="{{site.data.keyword.logs_full_notm}} background query (asynchronous archive query) CLI commands" caption-side="bottom"}

When you receive any of the following errors, consider the following information to resolve them:

- `MAX_RESULTS`: The query exceeded the maximum number of log lines allowed for a single response. This usually indicates that the result set is too large. Refine your query and narrow the query scope; for example, try reducing the time range or apply filters.

- `SCANNED_BYTES_LIMIT`: The query attempted to scan more data than permitted by the tier. Reduce the data scope, apply filters, or check if you can use a different type of query that returns a highr volume of data.

- `BLOCK_LIMIT`: Too many data blocks were involved in processing the query. This often results from querying a large time range or high-cardinality data. Refine your query and narrow the query scope; for example, try reducing the time range or applying filters.

- `METASTORE_DATA_MISSING`: The query timeframe points to archived data, but there is no available metadata for this period. Check that logs are available in the data bucket for the time range of the query.

- `BUCKET_ACCESS_DENIED`: The background query engine was unable to access the specified data bucket due to permission issues. Verify the authorization between {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.logs_full_notm}} (COS) is properly configured.

- `BUCKET_READ_FAILED`: A general I/O error occurred while attempting to read data from the COS bucket. This may be due to connectivity, permissions, or a corrupted file.

- `BUCKET_MISSING_DATA`: Some of the expected data blocks could not be found or read from your data bucket. Results may be incomplete.

- `SCROLL_TIMEOUT`: The server took too long to scroll through the result set, usually due to large volumes or resource constraints. Try running a smaller or more efficient query.



## Deleting background queries in {{site.data.keyword.logs_full_notm}}
{: #query-background-delete}

You cannot delete a background query.

A background query automatically expires after 30 days.
