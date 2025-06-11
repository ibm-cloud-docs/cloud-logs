---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-11"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Daily index limit considerations for {{site.data.keyword.logs_full_notm}} {{site.data.keyword.frequent-search}}
{: #priority-insight-index-limits}

The {{site.data.keyword.frequent-search}} feature in {{site.data.keyword.logs_full}} parses log records into typed fields and stores them in an index to provide reduced latency and very fast queries. However, {{site.data.keyword.frequent-search}} limits the number of fields that can be stored in the daily index of an {{site.data.keyword.logs_full_notm}} service instance.
{: shortdesc}

When you reach the index field limit, new fields in log records are no longer indexed. When you use filters or queries in {{site.data.keyword.frequent-search}} on the **Logs** page on fields that are not indexed, log records with non-index fields will not be returned. In this case, you might have the impression that log records are missing. In fact, log records are there, but are not found by searches in {{site.data.keyword.frequent-search}}.

This topic explains:

* How log records are parsed into fields.
* What is a field-based search.
* What is the daily index.
* What happens when the daily index field limit is reached.
* How to determine whether the daily index field limit is reached.
* How to determine whether a field is in the daily index.
* What you can do to stay below the daily index limit.

The {{site.data.keyword.compliance}} feature in {{site.data.keyword.logs_full_notm}} works differently than {{site.data.keyword.frequent-search}}. {{site.data.keyword.compliance}} has no indexing limits. If you are missing log records in {{site.data.keyword.frequent-search}} queries, use the same query in **All Logs** on the **Logs** page or submit it on the **Archive** query page. The {{site.data.keyword.compliance}} feature requires that you have connected an [{{site.data.keyword.cos_full_notm}} (COS) bucket](/docs/cloud-logs?topic=cloud-logs-about-bucket) to your {{site.data.keyword.logs_full_notm}} service instance.
{: tip}

## Parsing log records into fields
{: #pi-parse}

Log records sent to {{site.data.keyword.logs_full_notm}} can be text in many different formats: JSON, logfmt, Extended Log File Format, Syslog, Common Log Format, HAProxy log formats, and so on or any text that does not follow a known format.

If a log record is in JSON format, its JSON members are parsed into named fields together with their contents. For example: `{ "key": "value" }` is parsed into a field named `key` with content `value`.

If a log record is not in JSON format, or mixed with non-JSON data such as a timestamp at the beginning of the log record, [parsing rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) can be used in {{site.data.keyword.logs_full_notm}} to transform the log record into JSON format that can be parsed. Parsing rules can also be used to extract portions of the log record into named fields.

If a log record is in proper JSON format, the log record is parsed into named fields with its contents and the fields are indexed. Parsing rules can be applied to fix improper JSON format or to extract log record content into named fields with its contents. After the parsing rules are applied, the log record is indexed.

When a log record is stored in {{site.data.keyword.frequent-search}}, it is also stored in {{site.data.keyword.compliance}} if a [{{site.data.keyword.logs_full_notm}} COS data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket) is connected. That is, the log record is stored in two places in parallel.
{: note}

## What happens when {{site.data.keyword.frequent-search}} processes log records?
{: #pi-processing}

{{site.data.keyword.frequent-search}} keeps track of all known fields in its index. When a log record is processed, {{site.data.keyword.frequent-search}} checks whether the field names in the log record are already known. For an unknown field, a field mapping is added to the index that determines the field type plus other instructions about how to index the field.

After unknown fields have been added to the index, field values from the log record are indexed for fast field-based and full-text search. In addition, the full log record is stored.

## Label and metadata fields
{: #pi-fields}

Log records in {{site.data.keyword.logs_full_notm}} have label and metadata fields:

* `Application` or `Subsystem` are log record [label fields](/docs/cloud-logs?topic=cloud-logs-metadata). In Lucene queries, these fields need to be prefixed with `coralogix.`. In DataPrime queries, these fields need to be prefixed with `$l.`.
* `Timestamp`, `Severity`, and `priorityclass` are log record metadata fields. In Lucene queries, these fields need to be prefixed with `coralogix.`. In DataPrime queries, these fields need to be  prefixed with `$m.`.

Label and metadata fields are received by {{site.data.keyword.logs_full_notm}} together with the log record data or are populated by {{site.data.keyword.logs_full_notm}}. All label and metadata fields are known fields in the {{site.data.keyword.frequent-search}} index. {{site.data.keyword.logs_full_notm}} users can not add label and metadata fields to the index or remove them.

For more information, see:

* [Metadata fields](/docs/cloud-logs?topic=cloud-logs-metadata)
* [Sending logs by using the API](/docs/cloud-logs?topic=cloud-logs-send-logs-api)
* [DataPrime reference: Expressions](/docs/cloud-logs?topic=cloud-logs-dataprime-ref#expressions)

## Full-text and field-based search
{: #pi-search}

If you don't restrict queries in {{site.data.keyword.frequent-search}} to a searching a field, the search will be made on all indexed log record fields, also known as *full-text query*:

* Lucene queries: Don't prefix a query term with `<field>` when searching on indexed log record fields. This includes log record label and metadata fields. For example:

   ```text
   "application unvailable"
   ```
   {: codeblovk}

* DataPrime queries: Use a query similar to `source logs | filter $d ~~ '<text>'` when searching on indexed log record data fields. Searching log record data, label, and metadata fields at the same time requires a more complex query.

You can use *field-based search* and filters in {{site.data.keyword.frequent-search}} to search only specified indexed log record fields:

* Filters: On the **Filter** pane, you can select field values from a list of detected values. Only log records that match the selected field values will be returned. By default, the `Application`, `Subsystem`, and `Severity` fields are available for filtering. Other fields detected in log records can be added to define filters.
* Queries: Lucene and DataPrime queries can be used to search for only specified indexed fields.
   * Lucene: Use the `<field>:<query term>` syntax to apply the specified query term only to the specified field. For example:

   ```text
   message: "application unvailable" 
   ```
   {: codeblock}

   * DataPrime: Use field accessors `$d.<data field>`, `$l.<label field>`, or `$m.<metadata field>` to query the specified field. For example:

   ```text
   filter $d.message ~ 'application unavailable'
   ```
   {: codeblock}

Use *field-based searches* whenever possible to optimize your searches and reduce overall query time.
{: tip}

For more information, see:

* [Filtering log data](/docs/cloud-logs?topic=cloud-logs-query-data-filter)
* [Querying data by using Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene)
* [DataPrime reference](/docs/cloud-logs?topic=cloud-logs-dataprime-ref)

## Daily indices
{: #pi-daily}

Each {{site.data.keyword.logs_full_notm}} service instance has a separate set of {{site.data.keyword.frequent-search}} indices. The first index in the set is created when the service instance is created. Once a day, at 00:00am UTC, a new index is created and added to the set. At the same time, the oldest index is removed if it has reached its expiration date.

A new daily index only contains the known label and metadata fields. These already count towards the daily index limit. Every day, all other fields in the index are learnt anew from the processed log records. As a result, fields in daily indices can differ if processed log records differ.

## Daily index limits
{: #pi-daily-limits}

{{site.data.keyword.frequent-search}} limits the number of fields that can be stored in the daily index of an {{site.data.keyword.logs_full_notm}} service instance.

Once the daily index field limit is reached, the following will happen when {{site.data.keyword.frequent-search}} processes log records:

* Unknown fields are no longer added to the daily index and their field values are not indexed. These fields and their values are not lost because {{site.data.keyword.frequent-search}} always stores the full log record. Fields that are not index cannot be searched either in full-text or field-based searches.
* Field values of fields that are already known in the daily index will be indexed as usual.

For example:

* {{site.data.keyword.frequent-search}} processes a new log record with two fields: `{ "known": "indexed", "unknown": "stored" }`.
* Field `known` already has a field mapping in the daily index. Since it is known, its value `indexed` is indexed.
* Field `unknown` has no field mapping yet in the daily index. It is unknown. {{site.data.keyword.frequent-search}} cannot add a field mapping because the daily index limit is reached. Its value `stored` is not indexed.
* {{site.data.keyword.frequent-search}} stores the full log record.
* The following queries will return the log record:
   * Lucene query `indexed`.
   * Lucene query `known:indexed`.
   * DataPrime query `source logs | filter $d ~~ 'indexed'`.
   * DataPrime query `source logs | filter $d.known ~ 'indexed'`.
* The following queries will *not* return the log record because field `unknown` has no field mapping in the daily index and value `stored` is not indexed for field `unknown`:
   * Lucene query `stored`.
   * Lucene query `unknown:stored`.
   * DataPrime query `source logs | filter $d ~~ 'stored'`.
   * DataPrime query `source logs | filter $d.unknown ~ 'stored'`.

A new daily index automatically contains the known label and metadata fields. These are counted towards the daily index limit.
{: note}

Since new fields are added to the index in the order in which they appear and no more fields are added after the limit is reached, the set of fields in the index and the indexed field values, can differ day-to-day. For this reason, searches for a field might work one day but might not work the next.
{: important}

## Check daily index usage
{: #pi-check-daily-index}

You can check the usage of the current daily index from the {{site.data.keyword.logs_full_notm}} UI by clicking ![Usage icon](/icons/usage.svg "Usage") **Usage** > **Mapping stats** . Check the **Used keys today** statistic. If all keys are used, the daily index field limit is reached.

You can only check usage for the current day, not for previous days. Typically, this statistic is meaningful unless you check immediately after the daily index is created or your log records contain many new fields shortly before the current daily index closes.

## Determine if a field is in the daily index
{: #pi-in-daily}

On the the {{site.data.keyword.logs_full_notm}} UI, click ![Explore logs icon](/icons/explore.svg "Explore logs") **Explore Logs** > **Logs**.  Then select {{site.data.keyword.frequent-search}} and the **Logs** tab. Open **Settings** on the result list header. Select to **Show mapping errors** under **Annotations**. With that annotation option, all log record fields of the selected log record in the result list that have no mapping in the daily {{site.data.keyword.frequent-search}} index will be marked with a red exclamation mark indicator symbol. If you hover the mouse pointer over the indicator symbol, {{site.data.keyword.logs_full_notm}} will display a message.

There are two main reasons why a field is not indexed:

* You reached the daily index field limit of your {{site.data.keyword.logs_full_notm}} service instance.
* The field is only contained in log records that have a mapping exception. 

## Staying below daily index field limit
{: #pi-control-limit}

There are different strategies to stay below the daily index field limit:

* [Modify your log structure.](#pi-modlog)
* Use [TCO policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) to only store high priority log records in {{site.data.keyword.frequent-search}}.
* Use [Stringify JSON field parsing rules](/docs/cloud-logs?topic=cloud-logs-parse-convert-to-json-string) to turn the value of complex JSON object values into escaped JSON.
* Use [Remove Fields parsing rules](/docs/cloud-logs?topic=cloud-logs-parse-remove-rule) to remove fields from log records.
* Use [TCO policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) or [Block parsing rules](/docs/cloud-logs?topic=cloud-logs-parse-block-rule) to prevent log records from being stored.

### Modifying your log structure
{: #pi-modlog}

If you are sending logs from an application that you control, you might be able to modify your log structure. Try to optimise your log structure to contain only fields that are relevent to your searchs and investigations. All other information can be sent under a text field if indexing is not relevant. 

You can always use free text searches to find full or partial matches within a text field.
{: note}

### TCO policies
{: #pi-tco}

[TCO policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) in {{site.data.keyword.logs_full_notm}} can be used to classify received log records into different priority classes. Only logs records with high priority are processed and stored by {{site.data.keyword.frequent-search}}. Only logs records that are frequently searched should be sent to {{site.data.keyword.frequent-search}}.

Reducing the amount of logs sent to {{site.data.keyword.frequent-search}} will typically also reduce the number of indexed fields.

TCO policies can be applied by `Application Name`, `Subsystem Name` and `Severity` of the logs. For example, you might want to send `info` or `debug` logs to the {{site.data.keyword.monitoring}} or even the {{site.data.keyword.compliance}} tier, keeping only the most critical logs in {{site.data.keyword.frequent-search}} for quick searches.

### Stringify JSON field
{: #pi-stringify}

Use a [Stringify JSON field parsing rules](/docs/cloud-logs?topic=cloud-logs-parse-convert-to-json-string) to rename a field with a complex JSON object value and turn the value into escaped JSON. {{site.data.keyword.frequent-search}} only parses values in JSON format into named fields with content, but not escaped JSON. With the parsing rule, the transformed field is no longer an object field but a text field. {{site.data.keyword.frequent-search}} will no longer parse the former complex JSON object value into nested fields. Content of the transformed field will no longer work with filters or field-based queries, but can still be searched with full-text queries.

This approach is useful for complex log records in JSON format where most of the nested fields will rarely be used in filters or field searches.

For example, IBM Cloud activity tracking events have `requestData` and `responseData` fields that have JSON object values. If you need audit events in {{site.data.keyword.frequent-search}} instead of {{site.data.keyword.monitoring}} or {{site.data.keyword.compliance}}, you can define Stringify JSON field parsing rules to change the values of `requestData` and `responseData` fields into escaped JSON.

### Remove fields
{: #pi-remove}

Use a [Remove Fields parsing rules](/docs/cloud-logs?topic=cloud-logs-parse-remove-rule) to permanently delete unnecessary fields from log records. Removed fields are not stored in {{site.data.keyword.frequent-search}} or {{site.data.keyword.compliance}} and can not be used in alert conditions. There is no way to recover removed fields.

### Block log records
{: #pi-block}

[TCO policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) or [Block parsing rules](/docs/cloud-logs?topic=cloud-logs-parse-block-rule) can be used to permanently prevent log records from being processed and stored by {{site.data.keyword.frequent-search}}. There is no way to recover blocked logs.

Reducing the amount of logs in {{site.data.keyword.frequent-search}} will typically also reduce the number of indexed fields.

By default, blocked logs are not processed or stored by {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}} either. Block parsing rules offer an option to partially block log records and still process and store then in {{site.data.keyword.compliance}}.
{: tip}
