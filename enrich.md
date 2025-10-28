---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-28"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Enriching data
{: #enriching-data}

You can easily enrich your log data with {{site.data.keyword.logs_full_notm}}. You can automatically add fields to your JSON logs based on specific matches in your log data by using a pre-defined custom data source of your own. This way, you can enhance your log data with business, operations, or security information that is not available at run time.
{: shortdesc}

You can enrich your logs in two possible ways:

* Select a log key to be used to look up a key value and enrich the logs automatically during ingestion. The logs are saved with the enriched fields. The advantages of this mode are:

   * Logs are automatically enriched.

   * The logs include the enrichment data, which can be consumed everywhere (for example, in any query and also by third-party products that read the logs from the bucket).

* Use the DataPrime query [`enrich`](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#enrich) to look up a value in a table and enrich the log dynamically for the query. The advantages of this mode are:

   * You can enrich old logs already ingested into {{site.data.keyword.logs_full_notm}}.

   * The enrichment does not increase the size of the stored logs, since the enrichment is done dynamically, and is only used for the query results.

## Data enrichment use cases
{: #enrich-use-cases}

Some example use cases where enrichment can be helpful are:

### Monitoring
{: #enrich-monitoring}

In this example, assume we have logs with a UUID representing a customer. However, no field exists in the log with the customer name.

You can enrich the log by adding a field containing the customer name so you can visualize and search the logs base on the name. With custom enrichment, you create the enrichment by setting up a CSV file to map each UUID to a customer name.

### Security
{: #enrich-security}

In this example, the logs contain a field with a domain name that represents where an application is accessed. You want to create an alert that creates a notification if an attempt to access the application is made from an unauthorized domain.

You can create a CSV file with a list of allowlisted domains so each log is enriched with a field (`domain_enriched`) with the word `allowed` for domains in the list. You can then create an alert for logs that do not contain this field (for example `NOT domain_enriched:allowed`).


## Geo Enrichment
{: #geo-enrichment}

Logs can include IP information.

With the geo enrichment, you can automatically add IP-based geographical information, including ASN (Autonomous System Number) information, to your logs as new fields that can be queried, visualized, and reported.

For example, you can add the country name, city name, continent name, postal code, and location geo point.

If you don’t have IP fields set, or your data isn’t JSON-formatted, you can use {{site.data.keyword.logs_full_notm}} rules to extract the IP addresses that are found in your log records by using the [`Extract`](/docs/cloud-logs?topic=cloud-logs-parse-extract-rule&interface=ui#parse-extract-3-ui) or [`Parse`](/docs/cloud-logs?topic=cloud-logs-parse-rule&interface=ui#parse-rule-3-ui) rules.

After you define the IP field, {{site.data.keyword.logs_full_notm}} adds geographical information to the logs based on the selected fields.

These fields are not added if the enrichment database does not have the queried IP.
{: important}
