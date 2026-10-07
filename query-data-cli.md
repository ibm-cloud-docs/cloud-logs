---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-07"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


#  Querying data by using the CLI
{: #query-data-cli}

In {{site.data.keyword.logs_full_notm}}, you can query your log data by using Lucene queries, DataPrime queries, or by querying directly data from an {{site.data.keyword.cos_full_notm}} (COS) bucket. You can also apply filters to your queries.
{: shortdesc}



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

 ## Background Query (Asynchronous Archive Query)
    background-query-cancel, bgq-cancel       Cancel a background query.
    background-query-create, bgq-create       Submit a background query to be processed asynchronously.
    background-query-data, bgq-data           Data of background query to search the logs.
    background-query-status, bgq-status       Get the status of a background query.


 **background-query-data** - Data of background query to search the logs.

USAGE
  ibmcloud cloud-logs background-query-data --query-id QUERY-ID

ALIASES
  background-query-data, bgq-data

EXAMPLE
  ibmcloud cloud-logs background-query-data \
    --query-id 412036c3-04be-431a-b1e2-9ebf971be6c6 \
    --output-file tempdir/example-output.txt

OPTIONS
      --output-file string   Filename/path to write the resulting output to.
      --query-id string      Required. Generated query ID that can be later used to obtain data and results. The maximum length is 36
                             characters. The minimum length is 36 characters.
    --service-url string   Provide the base endpoint URL for the API.

## background-query-create

- Submits a query that runs in the background, allowing the client to continue without waiting for the results immediately.

USAGE
  ibmcloud cloud-logs background-query-create --query QUERY --syntax SYNTAX [--start-date START-DATE] [--end-date END-DATE] [--now-date NOW-DATE]

ALIASES
  background-query-create, bgq-create

EXAMPLE
  ibmcloud cloud-logs background-query-create \
    --query 'source logs | filter $d.apiVersion == 42' \
    --syntax dataprime_utf8_base64 \
    --start-date 2023-11-05T13:15:30.000Z \
    --end-date 2023-11-05T13:15:30.000Z \
    --now-date 2023-11-05T13:15:30.000Z

OPTIONS
      --end-date string     End of the time range for the query. Default: start + 15 minutes or current
                             time if start is not defined.
      --now-date string     Contextual 'now' for the query, default: current time. Used by functions
                             like now() in DataPrime.
      --query string        Required. The background query to be run. The maximum length is 4096 characters. The minimum length is 1 character.
      --start-date string   Beginning of the time range for the query, default: end - 15 minutes or current
                             time - 15 minutes if end is not defined.
      --syntax string       Required. The query syntax. Allowable values are: unspecified, lucene, dataprime, lucene_utf8_base64,
                            dataprime_utf8_base64.
    --service-url string   Provide the base endpoint URL for the API.



##   background-query-status

- Get the status of a background query.

USAGE
  ibmcloud cloud-logs background-query-status --query-id QUERY-ID

ALIASES
  background-query-status, bgq-status

EXAMPLE
  ibmcloud cloud-logs background-query-status \
    --query-id 412036c3-04be-431a-b1e2-9ebf971be6c6

OPTIONS
      --query-id string   Required. Generated query ID that can be used to obtain the status and results of a background query. The
                          maximum length is 36 characters. The minimum length is 36 characters.
    --service-url string   Provide the base endpoint URL for the API.


##  background-query-cancel
 - Cancel a background query.

USAGE
  ibmcloud cloud-logs background-query-cancel --query-id QUERY-ID

ALIASES
  background-query-cancel, bgq-cancel

EXAMPLE
  ibmcloud cloud-logs background-query-cancel \
    --query-id 412036c3-04be-431a-b1e2-9ebf971be6c6

OPTIONS
      --query-id string   Required. Generated query ID that can be later used to obtain status and results. The maximum length is 36
                          characters. The minimum length is 36 characters.

    --service-url string   Provide the base endpoint URL for the API.

## Query data from the UI
{: #query-data-ui}
{: ui}

In the Explore **Logs** page, you can:

* [Filter log data](/docs/cloud-logs?topic=cloud-logs-query-data-filter)
* [Search log data by using Lucene queries](/docs/cloud-logs?topic=cloud-logs-query-data-lucene)
* [Search log data by using DataPrime queries](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)


Filtering can be used in conjunction with searching using Lucene or DataPrime.

After you define a query, you can save it for later reuse by creating a view. For more information, see [Creating custom views](/docs/cloud-logs?topic=cloud-logs-custom_views&interface=ui#create_view).



##  Considerations when querying {{site.data.keyword.frequent-search}} data
{: #query-data-frequent-search}

There are considerations when querying log data in the {{site.data.keyword.logs_full_notm}} {{site.data.keyword.frequent-search}} pipeline:

- You can query logs that are ingested and processed through the [{{site.data.keyword.frequent-search}} data pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) by using a Lucene query or a DataPrime query.
- Filtering can be used in conjunction with searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).
- Logs in the [{{site.data.keyword.frequent-search}} pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) are indexed. If your instance reaches its maximum amount of indexed fields, additional fields are unavailable to query. For more information on indexing and data mapping, see [Understanding indexing and field mapping](/docs/cloud-logs?topic=cloud-logs-indexing_mapping).
- You can get a mapping exception when data that is ingested through the {{site.data.keyword.frequent-search}} data pipeline detects the same field sent by different log records with different types. Mapping exceptions make fields unavailable to query. For more information, see [Mapping exceptions](/docs/cloud-logs?topic=cloud-logs-query-mapping-exceptions).


##  Considerations when querying data from the data bucket
{: #query-data-all-logs}

You can query data from the Explorer logs page or by running an archive query.

There are considerations when querying log data from the data bucket:

- Data stored in the data bucket include data ingested through the {{site.data.keyword.frequent-search}}, {{site.data.keyword.monitoring}}, and {{site.data.keyword.compliance}} data pipelines. It also includes logs that are matched through a Parsing Block rule that has the *View blocked logs in Live tail and archive to IBM Cloud Object Storage* option enabled.
- You maintain the data in the bucket. You can keep the data for as long as you need and query it via the **Logs** page, selecting the **All logs** option.
- Filtering can be used in conjunction with searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).
- You can query data with unlimited time frames. There are no restrictions on how far back in time your data can go. You maintain the data and you ahve access to the data for as long as you keep it.
- You can query logs regardless of log priority and daily quota. Only blocked logs are not sent to the archive.
- Archive Query lets you to directly query your logs from your archive using any text or a wide range of syntax queries. You can query logs regardless of log priority, daily quota, or the time frame of your data. For more information, see [Querying archived data](/docs/cloud-logs?topic=cloud-logs-query-archive-data-bucket&interface=ui).

- Logs ingested through the {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}} data pipelines can only be [directly queried from the archive.](/docs/cloud-logs?topic=cloud-logs-query-archive-data-bucket&interface=ui).


## Limitations querying data through the Explorer
{: #query-data-limitations}
{: ui}

Limits exist when querying data in {{site.data.keyword.logs_full}}.


{{_include-segments/query-limits.md}}


## Archive query limitations
{: #query_archive_limits}

The following are the limitations placed on queries.

| Limitation | 	Description |
|---------|----------|
| Bytes processed |	Up to 30% of daily ingested bytes |
| Parquet files | Scanned	up to 500K files |
| Clone results |	Up to 1M results while running Archive Query |
| Time out |	Up to 5 minutes of query execution |
 {: caption="Archive query limitations" caption-side="bottom"}

You also need to be aware of the following when querying archived data:

* You can use the same query syntax ([Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime)) on the **Archive Queries** page.

* You might see slight delays when querying archived data when compared with other **Explore** queries.

* Once a limit is reached, a warning message is displayed. Refine your query results to avoid reaching a limit.


## Refining archive query results
{: #refine-archive-query}

You can refine your query results using the following methods:

* Apply more selective filters to your queries (for example, application or subsystem).

* If using the DataPrime [extract](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#extract) operator and subsequently filtering its results, create a parsing rule and filter on the parsed field instead.

* Avoid regular expressions or wildcards in filters.

* In [DataPrime](/docs/cloud-logs?group=dataprime), switch from using the contains operator on strings to the free text search operator (`~`).



## Query log data using CLI
{: #query-data-cli}
{: cli}

There are two ways to query log data using the CLI:

* `query`
* `background-query-create`

The `background-query-create` command runs an asynchronous query while `query` runs a synchronous query.

The background query lets you run a query and fetch the results at a later point in time. The query results are prepared and, once ready, you can download the results as a file using the CLI or the API.

With the background query up to 1M records can be returned. The `query` command is limited to returning 50K records.

The Query CLI supports only `logs-raw`, `logs-prettify`, and `json` as output. The default is `logs-raw`.
{: note}

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

### Running a background query
{: #background-query-data-cli}
{: cli}

You can query the log data asynchronously.

First you submit a background query. Then, you can use the ID with other commands.

```text
 ibmcloud logs background-query-create --query QUERY --syntax SYNTAX [--start-date START-DATE] [--end-date END-DATE] [--now-date NOW-DATE]
```
{: pre}

#### Command options
{: #cloud-logs-background-query-submit-cli-options}

`--query` (string)
:   The query to be run. This is a required parameter.

    The query syntax can be either Lucene or Dataprime. The syntax or type of the query is set using `--syntax` parameter.

`--syntax` (string)
:   The syntax in which the query is written. Allowable values are: `lucene` and `dataprime`.

`--start-date` (string)
:   Beginning of the time range for the query. This must be in UTC ISO 8601 format, for example: `2025-07-15T08:45:00Z`. The default is 15 minutes before the `--end-date` value. If `--end-date` is not specified, the default value is 15 minutes before the current time.

`--end-date` (string)
:   End of the time range for the query. This must be in UTC ISO 8601 format, for example: `2025-07-15T08:45:00Z`. The default is 15 minutes after the `--start-date` value. If `--start-date` is not defined the `--end-date` is the current-time and the `--start-date` is 15 minutes prior to current time.

Example

```text
ibmcloud logs background-query-create --query "Push and Query test" --syntax lucene --start-date 2025-06-16T12:00:00Z --end-date 2025-06-17T13:41:30Z
```
{: pre}

Example using DataPrime syntax

```text
ibmcloud logs background-query-create --query "source logs | filter \$d.text == 'Push and Query test'" --syntax dataprime --start-date 2025-08-03T12:00:00Z
```
{: pre}

### Determining the status of a background query
{: #background-query-status-cli}
{: cli}

You can determine the status of a [background query](/docs/cloud-logs?topic=cloud-logs-query-data&interface=cli#background-query-data-cli) by using the ID returned when running the background query command.

```text
ibmcloud logs background-query-status --query-id QUERY-ID
```
{: pre}

#### Command options
{: #cloud-logs-background-query-status-cli-options}

`--query-id` (strfmt.UUID)
:   Query ID returned from a [background query](/docs/cloud-logs?topic=cloud-logs-query-data&interface=cli#background-query-data-cli) command. Required.

    The value is 36 characters in length and must match the regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

Example

```text
ibmcloud logs background-query-status --query-id 8b5e7151-da2b-4633-be8c-9b269bed2c81
```
{: pre}

### Retrieving the resuts of a background query
{: #background-query-results-cli}
{: cli}

You can retrieve the query results of a [background query](/docs/cloud-logs?topic=cloud-logs-query-data&interface=cli#background-query-data-cli) by using the ID returned when running the background query command.

```text
ibmcloud logs background-query-data --query-id QUERY-ID --output OUTPUT
```
{: pre}

#### Command options
{: #cloud-logs-background-query-data-cli-options}

`--query-id` (strfmt.UUID)
:   Query ID returned from a [background query](/docs/cloud-logs?topic=cloud-logs-query-data&interface=cli#background-query-data-cli) command. Required.

    The value is 36 characters in length and must match the regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--output-file` (string)
:   Specifies the path to the file where the output is written.

`--output` (string)
:   The output format in which the results are returned. Valid values are `logs-raw`, `logs-prettify`, `json`, `yaml`, `tui`, or `table`. The default is `table`.

Example

```text
ibmcloud logs background-query-data --query-id df47fff7-131d-41dc-9328-05489a93e27c --output logs-raw
```
{: pre}

### Cancelling a background query
{: #background-query-cancel-cli}
{: cli}

You can cancel a [background query](docs/cloud-logs?topic=cloud-logs-query-data&interface=cli#background-query-data-cli) by using the ID returned when running the background query command.

```text
ibmcloud logs background-query-cancel --query-id QUERY-ID --force
```
{: pre}

#### Command options
{: #cloud-logs-background-query-cancel-cli-options}

`--query-id` (strfmt.UUID)
:   Query ID returned from a [background query](docs/cloud-logs?topic=cloud-logs-query-data&interface=cli#background-query-data-cli) command. Required.

    The value is 36 characters in length and must match the regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--force`|`-f`
:   Runs the command without further prompting of the user.

Example

```text
ibmcloud logs background-query-cancel --query-id df47fff7-131d-41dc-9328-05489a93e27c
```
{: pre}
