---

copyright:
  years:  2023, 2024
lastupdated: "2024-02-08"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Viewing log data by time interval
{: #query-data-time}

The log data displayed by {{site.data.keyword.logs_full_notm}} can be filtered by a specific time interval.
{: shortdesc}

Limiting by time interval can be used in conjunction with [filtering](/docs/cloud-logs?topic=cloud-logs-query-data-filter), searching using [Lucene](/docs/cloud-logs?topic=cloud-logs-query-data-lucene) or [DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).
{: tip}


{{site.data.content.query-ui}}

## Specifying a time interval
{: #use-time}

By default the **last 15 minutes** of data is displayed. You can change the time interval of log data displayed.

1. Click the time interval selection. If unchanged, this will read **Last 15 minutes**. If changed, the selected interval will be displayed.

2. Select the interval to be included:

   Quick
   :   Lets you quickly select a time interval. For example, all log data for **Today** or in the **Last 6 hours**. For **Quick** intervals, you can specify how often the query is automatically refreshed.

   Relative
   :   Lets you specify a time interval relative to the current time looking back the configured seconds, minutes, hours or days for the configured seconds, minutes, hours or days. For example, 6 days ago until 3 days ago.

   Custom
   :   Lets you specify a specific start and end date and time to be displayed.

   Tags
   :   Lets you filter logs by [tags](/docs/cloud-logs?topic=cloud-logs-benchmarks).


{{site.data.content.query-reset}}


{{site.data.content.save-view}}

