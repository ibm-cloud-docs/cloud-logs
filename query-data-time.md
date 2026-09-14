---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Viewing log data by time interval in {{site.data.keyword.logs_full_notm}}
{: #query-data-time}

The log data displayed by {{site.data.keyword.logs_full_notm}} can be filtered by a specific time interval using a time picker or using relative time queries handles through Dataprime expressions, dynamic time range variables or by using the `timeshifted` keyword.
{: shortdesc}

Limiting by time interval can be used in conjunction with [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter), searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).
{: tip}

## Methods to include a time interval in a query in {{site.data.keyword.logs_full_notm}}
{: #query-data-time-methods}

You can use any of the following methods to include a time interval in a query in {{site.data.keyword.logs_full_notm}}:

- Use the time picker to select only what is necessary.

- Use relative time queries.

    Relative time queries are handled via DataPrime time expressions. For example, use `now()` combined with standard time arithmetic and intervals (such as 1h, 15m, or 30s) to filter events dynamically or filter logs that are newer than one hour `($m.timestamp > now() - 1h)`. For more information, see [DataPrime date / time functions](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-date-time-func).

    You can also use dynamic time range variables (`$p`) to automatically respect active dashboard time pickers. For example, you can reference `$p.timeRange.startTime` or `$p.timeRange.endTime` in your queries. For more information, see [Using query parameters in your DataPrime queries in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-query-parameters).

    You can shift the evaluation window backward inside specific Dataprime commands to analyze historical baselines or compare current operational data against past performance. The `timeshifted` keyword modifies the timerange within the scope of the query. For example, when a custom dashboard has a global timerange of Today but your query only makes sense when looking at yesterday's data, you can use the keyword `timeshifted` followed by a time interval (`source logs timeshifted 1h`).


## Specifying a time interval through the time picker in {{site.data.keyword.logs_full_notm}}
{: #query-data-time-use-time}

By default the **last 15 minutes** of data is displayed.

You can change the time interval of log data displayed.
- In the *Logs* page, you can change the time picker that is applied when you run a query.
- In a custom dashboard, you can change the time picker for all widgets in the dashboard.
- In a widget in a custom dashboard, you can change the time picker to be only applied to the query run through the widget that is different from the one that is applied at the dashboard level.

Complete the following steps to specify a time interval through the time picker in {{site.data.keyword.logs_full_notm}}:

1. Launch the *Logs* page, open a widget within a custom dashboard, or add a widget to a custom dashboard.

2. Click the time interval selection.

    If unchanged, this will read **Last 15 minutes**. If changed, the selected interval will be displayed.

3. Select the interval to be included. You can select any of the following options:

   Quick
   :   Lets you quickly select a time interval. For example, all log data for **Today** or in the **Last 6 hours**. For **Quick** intervals, you can specify how often the query is automatically refreshed.

   Relative
   :   Lets you specify a time interval relative to the current time looking back the configured seconds, minutes, hours or days for the configured seconds, minutes, hours or days. For example, 6 days ago until 3 days ago.

   Custom
   :   Lets you specify a specific start and end date and time to be displayed.

   Tags
   :   Lets you filter logs by [tags](/docs/cloud-logs?topic=cloud-logs-benchmarks).
