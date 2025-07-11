---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-11"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring metric alerts
{: #alerts-config-metric}

Metrics alerts are alerts based on calculations on metrics recorded by {{site.data.keyword.logs_full}} using Event2Metrics.
{: shortdesc}

Metric alerts are notifications triggered by predefined thresholds being met or exceeded for specific metrics in your {{site.data.keyword.logs_full_notm}} dashboard.

Metric alerts are designed to monitor critical performance indicators surrounding infrastructure and other metrics. When specific thresholds or conditions are exceeded, these alerts act as an early warning system, notifying teams of potential issues requiring immediate attention. For instance, they help monitor server CPU utilization, response times, error rates, and resource utilization in cloud environments.


{{/_include-segments/alerts-prereq.md}}


{{/_include-segments/alerts-alerts-mgmt.md}}


{{/_include-segments/alerts-choose-type.md}}




## Specify a metrics query
{: step}
{: #alerts-config-4a-metric}

Using PromQL, enter a query against metrics stored in your {{site.data.keyword.logs_full}} insstance.

As you enter your PromQL query, you will get auto-complete suggestions.

Aggregate the metrics using the value of your choice, for example: application, subsystem, machine id, or other data. For example, you might want to track a total exception count with a single metric for all applications and add metric labels to represent new code areas. If the exception counter is called `application_error_count` and it covered code area `x`, you can add a corresponding metric label.

```text
application_error_count{area="x"}
```
{: codeblock}

Use the `by` aggregation operator to choose which dimensions (metric labels) to use to aggregate  and how to split your alert notification groups. For example, the query `sum by(instance) (node_filesystem_size_bytes)` returns the total `node_filesystem_size_bytes` for each instance.

## Specify the triggering condition
{: step}
{: #alerts-config-4b-metric}

Specify the triggering condition that is evaluated against the data returned from your query.

* For **Is** specify when you want the alert to trigger. For example, if the metric query occurs *More than usual*.

* For **Value** specify number of times when the query returns a match that will trigger the alert.

* For **For over** specify a percentage of time the query matches in the the time specified in **Of**.

Sometimes data might have missing values. Ifn you don’t replace missing values with zero and leave them empty, the data you do have is considered to be 100% of the data.

Let’s say that you query for a time frame of 10 minutes. 6 data points have values and 4 data points have no values. If you haven’t replaced the missing values with 0, the 6 minutes with values will be considered 100% of the timeframe. This can lead to false triggers.

You can replace missing values with 0 in the **Advanced settings**.

You can adjust the sensitivity of the alert triggering by adjusting the percentage for **At least % of the timeframe needs to have values for this alert to trigger** in the **Advanced settings**.

* The percentage values setting is designed to disable the alert when there are not enough data points to consider the alert reliable. When the amount of data is under the set percentage, the alert will not trigger, regardless of the actual metric value and whether it is over or under a threshold.

* If the percentage is set to 0 and the query crosses the threshold once, an alert is triggered.

* If the percentage is set to 100, this means all of the time window values should cross the threshold. If at any point a value does not, an alert is triggered.

The percentage value setting is not displayed when **Replace missing values with zeros** is selected. Once missing values are replaced with zero, then there is a guarantee that 100% of the data exists.
{: note}

If you are using the *Less than* condition, you will have the option to manage undetected values.

Undetected values occur when a permutation of a *Less than* alert stops being sent causing multiple triggers of the alert (for every timeframe in which it was not sent).

When you view an alert with undetected values, you have the option to retire these values manually, or select a time period after which undetected values will automatically be retired. You can also disable triggering on undetected values to immediately stop sending alerts when an undetected value occurs.

### Examples
{: #alerts-config-4b-metric-examples}

For example, you can choose if your alert will be triggered if it is *less than*, *less than or equals*, *more than*, *more than or equals* a certain value, or *more than usual* or *less than usual* for a minimum threshold. When the query passes the value or threshold set for the conditions, the alert is triggered.

By specifying a percentage (*for over x %*) and timeframe (*of the last x minutes*) determines how much of the timeframe you want to cross the threshold for the alert to trigger.
Select the percentage (*at least x %*) of the timeframe that needs values for the alert to trigger.

For example, you determine that over 50% of my 10-minute timeframe needs to have the set value for the alert to trigger. If I reach the value for 5 out of the 10 data points, it will not be enough to trigger an alert, as it is not over 50%. If I reach the value for 6 out of the 10 data points, an alert will be triggered.



{{/_include-segments/alerts-group-by.md}}


{{/_include-segments/alerts-config-notif.md}}


{{/_include-segments/alerts-set-schedule.md}}


{{/_include-segments/alerts-save-config.md}}


{{/_include-segments/alerts-next-steps.md}}

