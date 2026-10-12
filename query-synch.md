---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Querying data synchronously in {{site.data.keyword.logs_full_notm}}
{: #query-synch}

In {{site.data.keyword.logs_full_notm}}, you can run a synchronously query using DataPrime or Lucene syntax to query the data.
{: shortdesc}


## Running queries through the UI in {{site.data.keyword.logs_full_notm}}
{: #query-sync-ov-ui}
{: ui}

In {{site.data.keyword.logs_full_notm}}, you can query data through the *Logs Explorer* page by using any of the following options:

- [Querying data by using Lucene queries](/docs/cloud-logs?topic=cloud-logs-query-data-lucene)

- [Querying data by using DataPrime queries](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)

In the **Logs Explorer > Logs** page, you can choose any of the following options to query data:

- You can monitor {{site.data.keyword.frequent-search}} data through the *Priority Insights* option.

- You can monitor data through the *All Logs* option that is available in the COS data bucket and ingested through any data pipeline.


## Running synchronous queries through the CLI in {{site.data.keyword.logs_full_notm}}
{: #query-sync-ov-cli}
{: cli}

You can query logs synchronously by runing the `ibmcloud logs query` command.

```text
ibmcloud logs query ibmcloud cloud-logs query [--query "DATAPRIME_OR_LUCENE_QUERY"] \
[--metadata '{ --start-date START-DATE
               --end-date END-DATE
               --default-source DEFAULT-SOURCE
               --tier TIER
               --syntax SYNTAX
               --limit LIMIT
               --strict-fields-validation STRICT-FIELDS-VALIDATION
             }'
```
{: pre}

Where

`--query` (string)
:   Defines the query to be run.

    The maximum length is 4096 characters.

`--metadata` (string)
:   Metadata for the query execution. Use this configuration to provide the query execution parameters.

`--start-date` (string)
:   Beginning of the time range for the query.

    This must be in UTC ISO 8601 format, for example: `2025-07-15T08:45:00Z`.

    The default is 15 minutes before the `--end-date` value.

    If `--end-date` is not specified, the default value is 15 minutes before the current time.

`--end-date` (string)
:   End of the time range for the query.

    This must be in UTC ISO 8601 format, for example: `2025-07-15T08:45:00Z`.

    The default is 15 minutes after the `--start-date` value.

    If `--start-date` is not defined the `--end-date` is the current-time and the `--start-date` is 15 minutes prior to current time.

`--limit` (int)
:   Limit the number of records returned.

    If not specified, the default value is 2000.

    The maximum number of records returned when searching {{site.data.keyword.frequent-search}} is 12000. Otherwise the maximum number of records returned is: 50000.

`--default-source` (string)
:   Default value for the source to use when the source is omitted in a query.

    The maximum length is 4096 characters.

`--syntax` (string)
:   The syntax in which the query is written.

     Valid values are: `unspecified`, `lucene`, `dataprime`.

`--since` (duration)
:   Duration to look back from the current time when querying data.

    Using this flag overrides the `metadata-start-date` and `metadata-end-date`.

    For example, `1h` retrieves data from the past hour.

    The default value is set to `1h0m0s`.

`--tier` (string)
:   Tier on which the query runs.

    Valid values are: `archive`, and `frequent_search` ({{site.data.keyword.frequent-search}}).

`--strict-fields-validation`  (boolean)
:   Controls the fields that can be used in queries.

    When is set to false, you cannot use fields that are not detected in the ingested data.

    The default value is set to `false`.

`--output` (string)
:   The output format in which the results are returned. Valid values are `logs-raw` , `logs-prettify` and `json`.


For example, you can run the following samples:

```text
ibmcloud logs query --query "Push and Query test" --metadata '{"start_date": "2025-06-16T12:00:00Z", "end_date": "2025-06-17T13:41:30Z","syntax": "lucene"}' --output logs-raw
```
{: pre}

```text
ibmcloud logs query --query "source logs | filter \$d.text == 'Push and Query test'" --syntax dataprime --start-date 2025-08-03T12:00:00Z  --end-date 2025-08-04T13:41:30Z
```
{: pre}


## Running synchronous queries through the API in {{site.data.keyword.logs_full_notm}}
{: #query-sync-ov-api}
{: api}

You can query logs synchronously by running the API method `${URL}/v1/query`.


### API endpoint for synchronous queries in {{site.data.keyword.logs_full_notm}}
{: #query-sync-ov-api-endpoint}
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

### Retrieving an access token when using the API in synchronous queries in {{site.data.keyword.logs_full_notm}}
{: #query-sync-ov-api-token}
{: api}

You can retrieve your access token programmatically by first creating a [service ID API key](/docs/account?topic=account-serviceidapikeys){: external} for your application, and then exchanging your API key for an {{site.data.keyword.cloud_notm}} IAM token. For more information, see [Retrieving an access token with the API](/docs/cloud-logs?topic=cloud-logs-retrieve-access-token&interface=api).

### Running a synchronous query in {{site.data.keyword.logs_full_notm}}
{: #query-sync-ov-api-token}
{: api}

In {{site.data.keyword.logs_full_notm}}, the format of the API method to run a synchronous query is the following:

```text
curl -X POST --location --header "Authorization: Bearer ${iam_token}"   --header "Accept: text/event-stream"   --header "Content-Type: application/json"   --data   '{
    "metadata": {
      "end_date": "END_DATE",
      "limit": LIMIT,
      "start_date": "START_DATE",
      "strict_fields_validation": false,
      "syntax": "QUERY_SYNTAX",
      "tier": "TIER"
    },
    "query": "QUERY"
  }'   "${base_url}/v1/query"
  ```
  {: pre}

Where

`query` (string)
:   Defines the query to be run.

    The maximum length is 4096 characters.

`metadata` (string)
:   Metadata for the query execution. Use this configuration to provide the query execution parameters.

`start-date` (string)
:   Beginning of the time range for the query.

    This must be in UTC ISO 8601 format, for example: `2025-07-15T08:45:00Z`.

    The default is 15 minutes before the `--end-date` value.

    If `--end-date` is not specified, the default value is 15 minutes before the current time.

`end-date` (string)
:   End of the time range for the query.

    This must be in UTC ISO 8601 format, for example: `2025-07-15T08:45:00Z`.

    The default is 15 minutes after the `--start-date` value.

    If `--start-date` is not defined the `--end-date` is the current-time and the `--start-date` is 15 minutes prior to current time.

`limit` (int)
:   Limit the number of records returned.

    If not specified, the default value is 2000.

    The maximum number of records returned when searching {{site.data.keyword.frequent-search}} is 12000. Otherwise the maximum number of records returned is: 50000.

`syntax` (string)
:   The syntax in which the query is written.

     Valid values are: `unspecified`, `lucene`, `dataprime`.

`tier` (string)
:   Tier on which the query runs.

    Valid values are: `archive`, and `frequent_search` ({{site.data.keyword.frequent-search}}).

`strict-fields-validation`  (boolean)
:   Controls the fields that can be used in queries.

    When is set to false, you cannot use fields that are not detected in the ingested data.

    The default value is set to `false`.

For more information, see [Run a query to search the logs](/docs/apis/logs-service-api#query).
