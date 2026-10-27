---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-16"

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

## Prereqs
{: #alerts-config-metric-prereqs}
{: ui}

- Learn about alerts in {{site.data.keyword.logs_full_notm}}. For more information, see [Alerting](/docs/cloud-logs?topic=cloud-logs-alerts).
- Check that you have an [{{site.data.keyword.en_short}} instance](/catalog/services/event-notifications){: external} that is in the same account as your {{site.data.keyword.logs_full_notm}} instance and permisions to configure resources in the {{site.data.keyword.en_short}} instance.
- Check that the outbound integration between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_short}} instance is configured. For more information, see [Configuring an outbound integration to connect](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure).


## Launch alerts management
{: step}
{: #alerts-config-1}
{: ui}

Complete the following steps:

1. In the console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Resource list**.
2. Select your instance of {{site.data.keyword.logs_full_notm}}.
3. In the {{site.data.keyword.logs_full_notm}} navigation, click the **Alerts** icon ![Alerts icon](../icons/alerts_icon.svg "Alerts") > **Alerts Management**.
4. Click **New alert**.


## Choose the type of alert to configure
{: step}
{: #alerts-config-2}
{: ui}

Complete the following steps:

1. Choose the alert type. For more information, see [Alert types](/docs/cloud-logs?topic=cloud-logs-alerts#alert-types).

2. In the *Details* section, complete the following steps:

    1. Enter a name.

        - The maximum length of the name is 4096 characters.

    2. [Optional] Enter a description.

        - The maximum length of the description is 4096 characters.



    3. [Optional] Add one or more labels.

        Labels are key:value pairs that you can use later for quick searching.




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

If you are using the *Less than threshold* condition, you will have the option to manage undetected values.

Undetected values occur when a permutation of a *Less than* alert stops being sent causing multiple triggers of the alert (for every timeframe in which it was not sent).

When you view an alert with undetected values, you have the option to retire these values manually, or select a time period after which undetected values will automatically be retired. You can also disable triggering on undetected values to immediately stop sending alerts when an undetected value occurs.



### Customizing anomaly detection
{: #alerts-config-metric-anomaly}

Anomaly detection analyzes incoming metrics. Using data from the previous 24 hours, {{site.data.keyword.logs_full_notm}} forecasts expected behavior for the next 24 hours. The predictive model establishes upper and lower thresholds of expected behavior, setting those thresholds as boundaries. When data crosses these thresholds, an alert is triggered. A baseline is calculated between the average behavior and each threshold. You can specify a deviation percentage relative to this baseline to adjust the sensitivity of the alert triggering.

When setting a **More than usual** or **Less than usual** condition you can configure an advanced setting to alert only when the **Percentage deviation** is exceeded by that percentage amount.

For example, if the baseline is 50 and the upper threshold is 150 and the **Percentage deviation** is 10%, the alert will only be triggered if the value exceeds 155.




### Examples
{: #alerts-config-4b-metric-examples}

For example, you can choose if your alert will be triggered if it is *less than*, *less than or equals*, *more than*, *more than or equals* a certain value, or *more than usual* or *less than usual* for a minimum threshold. When the query passes the value or threshold set for the conditions, the alert is triggered.

By specifying a percentage (*for over x %*) and timeframe (*of the last x minutes*) determines how much of the timeframe you want to cross the threshold for the alert to trigger.
Select the percentage (*at least x %*) of the timeframe that needs values for the alert to trigger.

For example, you determine that over 50% of my 10-minute timeframe needs to have the set value for the alert to trigger. If I reach the value for 5 out of the 10 data points, it will not be enough to trigger an alert, as it is not over 50%. If I reach the value for 6 out of the 10 data points, an alert will be triggered.


In **Group By**, you can configure up to 2 JSON fields whose values are aggregated and determine when an alert is triggered.

- An alert is triggered when any of the aggregated values appear more than the threshold configured in the filtering conditions section within the specified timeframe.

- An alert is triggered when the condition threshold is met for a specific aggregated value within the specified timeframe.

- If you configure 2 values, matching logs will first be aggregated by the parent field, then by the child field. An alert will fire when the threshold meets the unique combination of both parent and child.


## Configure the notification details
{: step}
{: #alerts-config-5}
{: ui}

Complete the following steps:

1. Configure **Notify every** to define how often you want to get an event once the alert is triggered. By default is set to 0 hours and 10 minutes.

2. Enable **Resolve automatically** to get an event when the event has been resolved.

    When the alert's condition is no longer triggering events, the event that is triggered initially is marked as resolved.

3. Enable **Enable phantom mode** to indicate that this alert is a phantom alert.

    A Phantom alert serves as a building block for flow alerts.

    A Phantom alert does not trigger independent event notifications.

    When you enable this option, *Notifications* section  is removed from the alert definition.

4. Add an integration.

    You must have an outbound integration defined to be able to add an integration. For more information, see [Configuring the integration with the Event Notifications service](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure). 


## Set a schedule and what log content to include
{: step}
{: #alerts-config-6}
{: ui}


Complete the following steps:

1. In the *Schedule* section, set a Schedule to control when this alert is enabled. You can choose specific days and times.

2. In the *Notification Content* section, define whether you want to include a sample log line or only some fields in the event that is triggered.

    Choose specific JSON keys to include in the alert notification, or leave this blank to include the full log text in the alert message:

    - Option 1: Leave blank to include one log line that matches the filtering conditions of the alert.

    - Option 2: Specify JSON keys to include selected fields in the format of key:value pairs. Notice that to be able to add fields, your log records must be in JSON format.

       JSON keys containing a `.` in their name cannot be used as selected fields.
       {: restriction}

    - Option 3: Specify a  JSON path as the filter.

When an alert is triggered, there are limitations to the amount of data that is included in the event. For more information on these limitations, see [Data size](/docs/cloud-logs?topic=cloud-logs-event-payload#event-payload-2).
{: note}

## Save the alert configuration
{: #alerts-config-7}
{: step}
{: ui}

Complete the following steps:

1. Verify the alert.

    Click **Verify** to evaluate data to find out how many times the alert matched the criteria in the last 24 hours.

    Verify evaluates data in the {{site.data.keyword.frequent-search}} pipeline only. If your alert is configured to trigger on data that is available in the {{site.data.keyword.monitoring}} pipeline, notice that this feature is not available.
    {: important}

2. Click **CREATE ALERT**.

## Verifying your alert
{: #alerts-config-next}
{: step}

Trigger an alert. After an alert is triggered and processed, the system sends notifications to the designated users or teams through channels such as email, Slack, SMS, or integrated incident management platforms. Go to the **Incidents** page to see information about triggered alerts. For more information, see [Managing triggered alerts in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-incidents).

## Dynamic alerts limits
{: #limit-dynamic alert}

A dynamic alert is an alert with a **More than usual** or **Less than usual** condition. Each dynamic alert is allocated 500 permutations with a maximum of 10,000 permutations allowed for any {{site.data.keyword.logs_full_notm}} instance.

The permutation limit means that a maximum of 20 dynamic alerts can be configured for an {{site.data.keyword.logs_full_notm}} instance.

You can still create other non-dynamic alerts when you have reached the 20 dynamic alerts limit.
