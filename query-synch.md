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


## Managing queries through the UI in {{site.data.keyword.logs_full_notm}}
{: #query-sync-ui}
{: ui}

In {{site.data.keyword.logs_full_notm}}, you can query data through the *Logs Explorer* page by using any of the following options:

- [Querying data by using Lucene queries](/docs/cloud-logs?topic=cloud-logs-query-data-lucene)

- [Querying data by using DataPrime queries](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)

In the **Logs Explorer > Logs** page, you can choose any of the following options to query data:

- You can monitor {{site.data.keyword.frequent-search}} data through the *Priority Insights* option.

- You can monitor data through the *All Logs* option that is available in the COS data bucket and ingested through any data pipeline.


## Managing background queries through the CLI in {{site.data.keyword.logs_full_notm}}
{: #query-background-cli}
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


##   query - Run a query to search the logs.

USAGE
  ibmcloud cloud-logs query [--query DATAPRIME_OR_LUCENE_QUERY] [--metadata METADATA | --start-date START-DATE --end-date END-DATE --default-source DEFAULT-SOURCE --tier TIER --syntax SYNTAX --limit LIMIT --strict-fields-validation STRICT-FIELDS-VALIDATION]

EXAMPLE
  ibmcloud logs query \
	  --query "source logs" \
	  --metadata '{"start_date": "2019-01-01T12:00:00.000Z", "end_date": "2019-01-01T12:00:00.000Z", "default_source": "exampleString", "tier": "unspecified", "syntax": "unspecified", "limit": 38, "strict_fields_validation": true}'

OPTIONS
      --default-source string      Default value for the source to be used when the source is omitted in a query. The maximum length is
                                   4096 characters. The minimum length is 1 character.
      --end-date string            End of the time range for the query. Default: start + 15 min or current time if start is not defined.
      --ignore-metadata            Use this flag to ignore printing metadata in the logs output.
      --limit int                  Limit the number of results. Default: 2000; max for TIER_FREQUENT_SEARCH: 12000; max for TIER_ARCHIVE:
                                   50000.
      --local-time                 Convert the timestamp of the logs to local time.
      --metadata string            Configuration for query execution.
      --query string               Required. The query for which you are seeking results. The maximum length is 4096 characters. The
                                   minimum length is 1 character.
      --since duration             Query lookback window. Using this flag overrides metadata-start-date and metadata-end-date. (default 1h0m0s)
      --start-date string          Beginning of the time range for the query. Default: end - 15 min or current time - 15 min if end is not
                                   defined.
      --strict-fields-validation   Prohibit the use of unknown fields, i.e., those not detected in the ingested data. Default: false.
      --syntax string              The syntax in which the query is written. Allowable values are: unspecified, lucene, dataprime.
      --tier string                Tier on which the query runs.
       --service-url string   Provide the base endpoint URL for the API.


### Running a synchronous query
{: #query-data-cli-query}

You can query the log data synchronously by runing the **`ibmcloud logs query`** command.

```text
ibmcloud logs query --query QUERY --syntax QUERY_SYNTAX --metadata '{"start_date": START-DATE, "end_date": c, "syntax": SYNTAX , "limit": LIMIT, "strict-fields-validation": STRICT-FIELDS-VALIDATION, "tier": TIER}'
```
{: pre}

or

```text
ibmcloud logs query --query QUERY --syntax QUERY_SYNTAX --start-date START-DATE --end-date END-DATE --syntax SYNTAX --limit 10
```
{: pre}

#### Command options
{: #cloud-logs-query-cli-options}

`--query` (string)
:   The query to be run. This is a required parameter.

    The query syntax can be either Lucene or Dataprime. The syntax or type of the query is set using `--syntax` parameter.

`--metadata` (string)
:   Metadata for the query execution. Use this configuration to provide the query execution parameters.

`--start-date` (string)
:   Beginning of the time range for the query. This must be in UTC ISO 8601 format, for example: `2025-07-15T08:45:00Z`. The default is 15 minutes before the `--end-date` value. If `--end-date` is not specified, the default value is 15 minutes before the current time.

`--end-date` (string)
:   End of the time range for the query. This must be in UTC ISO 8601 format, for example: `2025-07-15T08:45:00Z`. The default is 15 minutes after the `--start-date` value. If `--start-date` is not defined the `--end-date` is the current-time and the `--start-date` is 15 minutes prior to current time.

`--limit` (int)
:   Limit the number of records returned. If not specified, the default is 2000. The maximum number of records returned when searching {{site.data.keyword.frequent-search}} is 12000. Otherwise the maximum number of records returned is: 50000.

`--syntax` (string)
:   The syntax in which the query is written. Allowable values are: `lucene` and `dataprime`.

`--since` (duration)
:   Duration to look back from the current time when querying data. Using this flag overrides the `metadata-start-date` and `metadata-end-date`. For example, `1h` retrieves data from the past hour (default `1h0m0s`).

`--tier` (string)
:   Tier on which the query runs. Allowable values are: `archive`, `frequent_search` ({{site.data.keyword.frequent-search}}).

`--output` (string)
:   The output format in which the results are returned. Valid values are `logs-raw` , `logs-prettify` and `json`.

Example

```text
ibmcloud logs query --query "Push and Query test" --metadata '{"start_date": "2025-06-16T12:00:00Z", "end_date": "2025-06-17T13:41:30Z","syntax": "lucene"}' --output logs-raw
```
{: pre}

The `query` command also supports `--start-date`, `--end-date` and `--syntax` outside the `metadata` parameter. For example:

```text
ibmcloud logs query --query "source logs | filter \$d.text == 'Push and Query test'" --syntax dataprime --start-date 2025-08-03T12:00:00Z  --end-date 2025-08-04T13:41:30Z
```
{: pre}
