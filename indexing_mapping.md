---

copyright:
  years:  2024
lastupdated: "2024-10-09"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Understanding indexing and field mapping
{: #indexing_mapping}

To best query your logs, it is important to understand how {{site.data.keyword.logs_full_notm}} indexes your data after it is analyzed.
{: shortdesc}

Indexing logs lets you quickly retrieve matching by logs using:

* Free-text searches
* Regular expressions
* Field searches

It is recommended to serialize your logs as JSON to get maximum value from {{site.data.keyword.logs_full_notm}} analytics features. See [Configuring unstructured text into JSON](/docs/cloud-logs?topic=cloud-logs-parse-rule&interface=ui) for more information about parsing unstructured logs to JSON.
{: tip}

For a service instance, the daily default limit of indexed fields is set to 3000. Having too many fields in your index can lead to a mapping problem. The daily default limit of 3000 fields exists to avoid search and performance degradation.
{: note}

You can find out how many indexed fields you have used in **Usage** in the **Mapping stats** section.
{: tip}

## Data types
{: #data-types}

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

* {{site.data.keyword.logs_full_notm}} has a default limit of 3000 indexed fields per instance per day. You can view your team's mapped field statistics under **Usage** section ![Usage icon](/icons/usage.svg "Usage") > **Mapping stats**.

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
