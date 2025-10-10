---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-10"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring time relative alerts
{: #alerts-config-time-relative}

Automatically detect abnormal behavior in your system by using the time relative alerts. Alerts are triggered when a fixed ratio reaches a set threshold compared to a past time frame.
{: shortdesc}


{{/_include-segments/alerts-prereq.md}}


{{/_include-segments/alerts-alerts-mgmt.md}}


{{/_include-segments/alerts-choose-type.md}}


{{/_include-segments/alerts-choose-logs.md}}


## Specify the triggering condition
{: step}
{: #alerts-config-4-tr}

Specify the triggering condition that is evaluated against the data included for analysis for this alert.

In the *Conditions* section, you must configure the fields in **Alert if ratio is** and **Group by**.

In **Alert if ratio is**, you must select whether the alert is triggered when the query is matched more or less than the number of configured times within the defined time window.

- Choose `More than threshold` to be notified when the ratio between the two time periods is more than the chosen threshold.

- Choose `Less than threshold` to be notified when the ratio between the two time periods is less than the chosen threshold.

The following table includes the time windows you can configure:

| Time window | Definition |
|-------------|------------|
| `Previous hour` | Compares the query results of the previous hour to the current hour |
| `Same hour yesterday` | Compares the query results from the current hour to the results of the same hour yesterday (24 hours ago) |
| `Same hour last week` | Compares the query results from the current hour to the results of the same hour on the same day last week (7 days ago) |
| `Yesterday` | Compares the query results from the current day (24 hours) to the previous day (24 hours) |
| `Same day last week` | Compares the query results from the current day (24 hours) to the same day last week (7 days ago) |
| `Same day last month` | Compares the query results from the current day to the results from the same day in the prior month |
{: caption="Time window conditions" caption-side="bottom"}

Timeframe comparisons are made every 5 minutes for hourly comparisons (`Previous hour`, `Same hour yesterday`, `Same hour last week`) and every 10 minutes for daily comparisons (`Yesterday`, `Same day last week`, `Same day last month`).

For example, if in the last hour a query returns 180 error logs. The query in the previous hour returned 60 error logs. In this case the ratio between the two hours is 3. If the alert is configured for a ratio of more than 1 compared to the previous hour the alert will be triggered.

If you are using the *Less than threshold* condition, you will have the option to manage undetected values.

Undetected values occur when a permutation of a *Less than threshold* alert stops being sent causing multiple triggers of the alert (for every timeframe in which it was not sent).

When you view an alert with undetected values, you have the option to retire these values manually, or select a time period after which undetected values will automatically be retired. You can also disable triggering on undetected values to immediately stop sending alerts when an undetected value occurs.

### Triggering alerts on infinity
{: #alerts-config-4a-tr}

If the second query result returns a zero value, the calculated ratio would be an infinite number.

You can specify whether or not to trigger the alert on this condition by selecting or deselecting **Do not tigger on Infinity**.


{{/_include-segments/alerts-group-by.md}}


{{/_include-segments/alerts-config-notif.md}}


{{/_include-segments/alerts-set-schedule.md}}


{{/_include-segments/alerts-save-config.md}}


{{/_include-segments/alerts-next-steps.md}}
