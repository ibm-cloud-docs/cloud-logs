---

copyright:
  years:  2024, 2026
lastupdated: "2026-04-01"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


#  Schema Explorer
{: #schema-explorer}

In {{site.data.keyword.logs_full_notm}}, you can use the Schema Explorer to unify and control the structure of your logs in {{site.data.keyword.logs_full_notm}}. Since logs often come from your many sources with different naming conventions, inconsistencies can quickly make analysis harder.
{: shortdesc}

The Schema Explorer automatically detects, highlights, and reports on these differences so you can:
- Prevent duplicate fields.
- Reduce query errors caused by inconsistent keys.
- Discover and resolve duplicate or conflicting fields.
- Provide feedback to developers when fields are misaligned.


## Key Features
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


## How it Works
{: #schema-explorer-how-it-works}

1. Ingestion - Ingests all log fields, regardless of structure or naming convention.
2. Detection - Schema Management identifies duplicate or similar keys.
3. Analysis - You can explore how each field is used, how often it appears, and its unique values.
4. Unification - Align conflicting keys into a single schema, ensuring consistency across teams and services.


## Example Scenario
{: #schema-explorer-example-scenario
}
You have three services sending user data:
- `Service A uses surname`
- `Service B uses familyname`
- `Service C uses family-name`
Without Schema Management, your queries might miss data because the fields don't match. With Schema Management, you can detect these variations and map them to a unified key such as last_name.


## UI Walkthrough
{: #schema-explorer-UI-Walkthrough}
1. Go to **Data Flow > Schema Explorer**
2. Use the search bar to find specific fields.
3. Review each field's popularity, type, mapping status, and cardinality to identify duplicates or inconsistencies
4. Use Mapping Exceptions to align similar fields into a single schema.



## Recommendations
{: #schema-explorer-recommendations}

- `Regularly check for new fields ingested to catch inconsistent naming early`.
- `Standardize fields names with your development teams to reduce mapping exceptions`.
- `Reservice fields for critical identifiers that must remain consistent across services`.
To take schema governance a step further, {{site.data.keyword.logs_full_notm}} provides Reserved Fields which are a way to explicitly define the fields that matter most for your queries, alerts, and dashboards. While Schema Explorer helps you discover and analyze fields, Reserved Fields let you lock in critical ones, ensuring they are always indexed with the correct type and available for use.
