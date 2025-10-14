---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-14"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Configuring custom enrichments
{: #enrich-howto}

You can enhance {{site.data.keyword.logs_full}} log data with additional business, operational, or security context to improve log analysis and understandability.
{: shortdesc}

Custom enrichment lets you enhance your logs by adding critical contextual data that might not be available at runtime. This enrichment is done by appending fields to your JSON logs based on specific matches using a custom data source that you define.

Some use cases for custom enrichments include:

* Monitoring

   For example, you can gain visibility into customer names based on customer IDs.

   Suppose you have a log with a UUID representing a customer, but no field containing the customer's name. By including a field with the customer's name, you can visualize and search logs based on this information. With custom enrichment, you can set up a CSV file mapping each UUID to a customer name, enriching the logs automatically as they are ingested.

* Security

    For example, receiving alerts when users browse domains outside of your allowlist.

    Consider a log field with a domain name representing where the user is browsing. You want to create an alert for any attempts to access your application from unauthorized domains. By setting up a CSV file with a list of allowlisted domains, you can enrich logs with a field containing the word "allowed" for each allowlisted domain. Then, create an alert for logs not containing this field, using a query such as `NOT domain_enriched:allowed`.

## Example
{: #enrich-howto-example}

Enriching logs with user details provides immediate context about actions performed, enabling better security monitoring and incident response. This example demonstrates how a log is transformed with string-to-string or string-to-JSON mapping.

Consider the following original log:

```json
{
  "action": "DeleteFile",
  "user_id": "1234"
}
```
{: codeblock}

You can enriched the log with string-to-string mapping.

```json
{
  "action": "DeleteFile",
  "user_id": "1234",
  "user_id_enriched": "John White"
}
```
{: codeblock}

You can also enriched the log with string-to-JSON mapping.

```json
{
  "action": "DeleteFile",
  "user_id": "1234",
  "user_id_enriched": {
    "name": "John White",
    "role": "DevOps Engineer",
    "department": "IT"
  }
}
```
{: codeblock}

## Required permissions
{: #enrich-howto-iam}

Depending on which actions you want to take with custom enrichments, you must have an IAM role with the required actions:

| Action | Description |
|--------|-------------|
| logs.custom-enrichment.read | Read custom enrichment configuration. |
| logs.custom-enrichment.manage | Manage custom enrichment configuration. |
| logs.custom-enrichment-data.read | Read data for custom enrichment configuration. |
| logs.custom-enrichment-data.manage |	Manage data for custom enrichment configuration. |
{: caption="IAM actions required for custom enrichments" caption-side="bottom"}

## Log enrichment methods
{: #enrich-howto-methods}

Custom enrichment supports two methods:

* Automatic enrichment during ingestion.

* Dynamic enrichment using [DataPrime](/docs/cloud-logs?topic=cloud-logs-dataprime-ref) syntax.

### Automatic enrichment
{: #enrich-howto-auto}

Automatic enrichment appends additional data to logs as they are ingested. This ensures enriched logs are consistently available for queries across {{site.data.keyword.logs_full_notm}}, including in [alerts](/docs/cloud-logs?topic=cloud-logs-event-notifications-about) and [custom dashboards](/docs/cloud-logs?topic=cloud-logs-create_dashboards).

### DataPrime query enrichment
{: #enrich-howto-dp}

With the DataPrime [`enrich`](/docs/cloud-logs?topic=cloud-logs-dataprime-ref#enrich) query you can dynamically enrich at query time without increasing the stored log size. This approach lets you enrich previously ingested logs.

With DataPrime you can expose custom enrichments as fully queryable datasets. The custom enrichment feature lets you enhance your logs by adding critical contextual data that might not be available at runtime. This enrichment is done by appending fields to your JSON logs based on specific matches using a custom data source that you define. 

For example:

```text
source ... | enrich ... using my_enrichment | ... 
```
{: codeblock}

## Preparing a CSV file
{: #enrich-howto-csv}

To define your custom data source, create a CSV file with either string-to-string or string-to-JSON mappings. CSV files must contain a minimum of two columns. Columns must include titles. Users can select any column from the file that maps to the log field and the columns used to enrich the logs.

### String-to-string mapping
{: #enrich-howto-s2s}

For simple key-value mapping, use a CSV file with two columns.

For example:

```text
key, value
5c8593f4-136d-450b-9226-ef6137ad0fa3, customer1
b2f3f7e6-362a-4838-97d4-69886552fd88, customer2
978bfb69-b9ab-4550-8133-0f3f8b4d302b, customer3
58a2d452-51b0-4667-bfe5-a11f864f1c57, customer4
c80452a8-9573-4e3c-b3f6-88ae740c776c. customer5 
```
{: codeblock}

### String-to-JSON mapping
{: #enrich-howto-s2j}

For richer context, include multiple columns in a CSV file. There is no limitation on the number of columns that can be included.

For example:

```text
key, name, size
5c8593f4-136d-450b-9226-ef6137ad0fa3, customer1, big
b2f3f7e6-362a-4838-97d4-69886552fd88, customer2, small
978bfb69-b9ab-4550-8133-0f3f8b4d302b, customer3, big
58a2d452-51b0-4667-bfe5-a11f864f1c57, customer4, medium
c80452a8-9573-4e3c-b3f6-88ae740c776c. customer5, medium
```
{: codeblock}



## Configuring a data enrichment
{: #enrich-howto-steps}
{: ui}

1. [Launch the {{site.data.keyword.logs_full_notm}} UI.](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

2. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Data Enrichment**.

3. Click **+ Add custom enrichment**.

4. Configure the enrichment by providing a name and description.

5. Upload your CSV file.

   You can also replace a CSV file that you have uploaded.
   {: note}

6. To enable automatic enrichment, define how logs should be enriched during ingestion:

   * Field: Select one or more fields for enrichment.

   * Enriched Field Name: Specify the enriched field name.

   * Lookup Column: Choose the CSV column that maps to the log field.

   * Columns for Enrichment: Select additional CSV columns to enrich the logs.

7. Click **Create enrichment**.



## Configuring a data enrichment using the API
{: #enrich-howto-api}
{: api}

You can also configure custom enrichments using the API. For more information, see:

* [Listing enrichments](/apidocs/logs-service-api#get-enrichments)
* [Creating enrichments](/apidocs/logs-service-api#create-enrichment)
* [Deleting enrichments](/apidocs/logs-service-api#remove-enrichments)

## Limitations
{: #enrich-howto-limit}

* CSV files are limited to 150,000 rows.

* Files exceeding 10,000 rows can only be used for [DataPrime query enrichment](/docs/cloud-logs?topic=cloud-logs-dataprime-ref#enrich), not [automatic ingestion enrichment](#enrich-howto-auto).
