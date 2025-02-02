---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Understanding indexing and field mapping
{: #indexing_mapping}

To best query your logs in {{site.data.keyword.frequent-search}}, it is important to understand how {{site.data.keyword.logs_full_notm}} indexes your data after it is analyzed.
{: shortdesc}

Indexing logs lets you quickly retrieve matching by logs using:

* Free-text searches
* Regular expressions
* Field searches

{{site.data.keyword.logs_full_notm}} has daily index limits that might affect your {{site.data.keyword.frequent-search}} queries. For more information about these limits and how to manage them in your environment, see [Daily index limit considerations for {{site.data.keyword.logs_full_notm}} {{site.data.keyword.frequent-search}}](/docs/cloud-logs?topic=cloud-logs-priority-insight-index-limits)
{: important}

It is recommended to serialize your logs as JSON to get maximum value from {{site.data.keyword.logs_full_notm}} analytics features. See [Configuring unstructured text into JSON](/docs/cloud-logs?topic=cloud-logs-parse-rule&interface=ui) for more information about parsing unstructured logs to JSON.
{: tip}


## Data types
{: #indexing_mapping_data_types}

{{site.data.keyword.logs_full_notm}} supports the following data types:

Text
:   This type represents unstructured, human-readable content that is analyzed into terms before indexing.

Keyword
:   This type represents text that does not pass through the analyzer before indexing. This data type is suitable for regular expressions, aggregation, and sorting.

    The syntax to use the keyword data type in your query is: `<fieldName>.keyword`.

    {{site.data.keyword.logs_full_notm}} can not create a keyword type when a field is longer than 256 characters.
    {: important}

Numeric
:   This type is suitable for range queries and arithmetic aggregations (`avg`, `max`, `min`, `sum`).

    The syntax to use the numeric data type in your query is: `<fieldName>.numeric`.

Date
:   This type lets you filter by timestamp or plot time-series graphs. Values should be formatted as epoch milliseconds.

Geopoint
:   This type allows you to plot longitude and latitude pairs on a Grafana map.

Object
:   This type represents a hierarchy. This means that it can contain fields of any other type (including objects).



## Data type considerations
{: #type-considerations}

Consider the following when querying data:

* Explicit mapping is supported for timestamps and geopoints. Appending `_timestamp` or `_geopoint` to your field name will map it respectively as a date or geopoint. For example, a field named `duration_timestamp` is mapped as a date.

* Dynamic mapping is used for all other fields. This means that at the time of indexing, a new field’s value determines the mapped data type.

* Arrays are valid JSON. However, there is no dedicated array data type in {{site.data.keyword.logs_full_notm}}. This means that:

   * A field can contain multiple values, and all values should be of the same data type. Otherwise, a mapping exception will occur.

   * The first value in an array determines the field mapping.

   * For an array of objects, it is not possible to query each object independently.

*  Each field in the log is mapped as one of 3 data types:

   * Text, Object, Date, or Geopoint
   * Keyword
   * Numeric
