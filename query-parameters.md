---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-16"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Using query parameters in your DataPrime queries
{: #query-parameters}

The {{site.data.keyword.logs_full}} DataPrime `$p` variable lets you incorporate variables into your DataPrime queries for custom dashboards and time-related parameters.
{: shortdesc}

This feature externalizes variables as if they were written directly in a query. This enhances flexibility for filtering, calculations, and visualizations by allowing user-defined inputs and contextual data handling.

How does `$p` work?

* `$p` represents query parameters that can be used in widgets, queries, and external filters, such as a dashboard time picker.

* `$p` enables dynamic filtering and other actions without requiring manual query modifications.

* Users can pass and manipulate these parameters in the dashboard.

## Defining query parameters
{: #qp-define}

You can use the `$p` variable when configuring custom dashboards and when creating queries in the **Logs** view.

### Custom dashboards
{: #qp-define-cd}

Once a variable is created in custom dashboards, the variable values chosen by the user are reflected as query parameters in a DataPrime query using `$p.<variable_name>`.

Variables in custom dashboards are treated as string or multi-string values, meaning numeric variables cannot be defined directly. Numeric variables can be used in queries, for example, `filter duration > $p.minDuration`.
{: note}

### Logs
{: #qp-define-logs}

In the **Logs** view, you can do time calculations in your DataPrime query using `$p.timeRange.*`, with `$p` allowing you to source data from the time window determined by the UI time picker.

## Time-related parameters
{: #dp-time}

Time-related parameters are automatically created. You can source data from a time window determined by the UI time picker using `timeRange` in custom dashboards and the **Logs** view.

Time-related parameters include:

`$p.timeRange.startTime`
:   The start time of the UI time picker (for example, 2024-03-06T08:00:00Z)

`$p.timeRange.endTime`
:   The end time of the UI time picker (for example, 2024-03-06T12:00:00Z)

## Query parameter usage examples
{: #qp-usage}

The following sections provide `$p` usage examples.

### Working with a single-value variable
{: #qp-single}

The following query example incorporates a single-value variable, as denoted by the use of `==`.

```text
source logs
| filter cluster_name == $p.cluster
```
{: codeblock}

This filters logs where `cluster_name` matches the user-defined, single-value variable `$p.cluster`.

Users can dynamically modify this value using the custom dashboards UI.

## Working with multi-selection variables
{: #dp-multi}

Multi-selection variables let users pass multiple potential values in a single parameter.

### Handling "any value" selection
{: #dp-any}

When a user selects "any value," the system treats this as `null`, meaning that the filter is ignored.

```text
source logs
| filter $p.clusters == null || $p.clusters.arrayContains($d.clusterId)
```
{: codeblock}

If the user selects "any value" for `$p.clusters`, it is treated as null, removing the filter. Otherwise, the filter ensures that `$d.clusterId` exists within the selected values of `$p.clusters`.

## Static list of values
{: #dp-list}

Create a `minDurationSeconds` variable with a static list of values (for example. 1, 5, 10, 30, 60). These values are handled as strings, but can be used as a number within the query as follows:

```text
source logs
| filter duration ≥ $p.minDuration:number
```
{: codeblock}

## Defining a dynamic `groupby` field using a variable
{: #dp-groupby}

Using dynamic variables, `groupby` lets queries adapt based on user-defined criteria, enabling more flexible data aggregation and analysis. The following query groups data based on the field specified by the `$p.myGroupByVar` variable, then aggregates the results by counting the number of occurrences in each group.

```text
groupby $d[$p.myGroupByVar] agg count()
```
{: codeblock}

This differs from `groupby $p.my_group_by_variable agg count()`. Since the variable is a string, running this query would be effectively identical to `groupby 'my_value' agg count()`, which means that it will do a `groupby` on a static string, aggregating all results into a single group called `my_value`.
{: note}

## Filtering logs within a specific time range
{: #dp-time-filter}

This filters logs within the specified time range while ensuring the duration field is greater than or equal to `$p.minDuration`.

```text
source logs between $p.timeRange.startTime and $p.timeRange.endTime
| filter duration >= $p.minDuration
```
{: codeblock}

## Rounding to the nearest hour
{: #dp-round-hour}

This example adjusts the time range to the nearest full hour before filtering logs based on duration. Any time calculation can be done using `$p.timeRange.*`.

```text
source logs between $p.timeRange.startTime/1h and $p.timeRange.endTime/1h+1h
| filter duration >= $p.minDuration
```
{: codeblock}

## Joining last week’s data for the same timeframe
{: #dp-join-time}

Using the `join` command, the following query joins and compares the number of logs per subsystem from today to those exactly one week prior.

```text
source logs 
| groupby $l.subsystemname agg count() as cnt
| join (source logs timeshifted -7d
        | groupby $l.subsystemname agg count() as cnt) using subsystemname into a_week_before
```
{: codeblock}

This verbose example provides a way to gain more control over the time range, if needed.

```text
source logs 
| groupby $l.subsystemname agg count() as cnt
| join (source logs between $p.timeRange.startTime-7d and $p.timeRange.endTime-7d
        | groupby $l.subsystemname agg count() as cnt) using subsystemname into a_week_before
```
{: codeblock}
