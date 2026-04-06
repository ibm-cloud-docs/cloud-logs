---

copyright:
  years:  2024, 2026
lastupdated: "2026-04-06"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


#  Schema Explorer
{: #schema-explorer}

Use the Schema Explorer to automatically detect, highlight, and report on differences detected in the structure of your logs as they are ingested such as duplicate fields with different data types that cause conflict.
{: shortdesc}

Logs often come from different sources and might have different naming conventions, causing inconsistencies that can quickly make analysis harder. In {{site.data.keyword.logs_full}}, you can use the `Schema Explorer` to centralize information about the structure of your logs, naming conventions and data types.


At ingestion, all fields are extracted regardless of structure or naming convention. After ingestion, the Schema Manager identifies duplicate or similar keys. Then, you can explore how each field is used, how often it appears, its unique values and any mapping exceptions.

You can use the Schema Explorer to automatically detect, highlight, and report on differences identified on the structure of your logs.
- Prevent duplicate fields.
- Reduce query errors caused by inconsistent keys.
- Discover and resolve duplicate or conflicting fields.
- Provide feedback to developers when fields are misaligned.

## Use-case scenarios
{: #schema-explorer-recommendations}

Consider the following use-case scenarios when using the Schema Explorer:

- Regularly check for new fields ingested to catch inconsistent naming early.

- Standardize fields names with your development teams to enhance querying and keep consistency across services and applications.

- Standardize the type of fields names with your development teams to reduce mapping exceptions.

- Identify fields that you must define as `Reserve fields` for critical analysis.



## Information per field
{: #schema-explorer-key-features}

You can use Schema Explorer to get a complete view of the fields that are ingested across your logs, For each field, you can see:
- `Path`: The field name and location
- `Mapping Status`: Indexing status for the selected time range:
- `Mapped`: Indexed
- `Unmapped`: Not Indexed
- `Partially mapped` - Indexed for part of the time range
- `Type` - Data type (string, numeric, object etc.).
- `Popularity over time`- How frequently the field appears.
- `Cardinality` - Number of unique values and how it changes over time.
- `First seen/Last seen`- When the field was ingested.

This helps you identify fields that may be redundant, inconsistent, or unexpectedly missing.



## Example Scenario
{: #schema-explorer-example-scenario
}
You have three services sending user data:
- `Service A uses surname`
- `Service B uses familyname`
- `Service C uses family-name`
Without Schema Management, your queries might miss data because the fields don't match. With Schema Management, you can detect these variations and map them to a unified key such as last_name by using a parsing rule.


## Launching Schema Explorer
{: #schema-explorer-ui}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. In the dashboard, click **Data Pipeline** > **Schema Manager**.

    The Schema Explorer opens.

Next, you can:
- Use the search bar to find specific fields.
- Review each field's popularity, type, mapping status, and cardinality to identify duplicates or inconsistencies
- Check Mapping Exceptions to align similar fields into a single schema.
