---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring time relative alerts
{: #alerts-config-time-relative}

Automatically detect abnormal behavior in your system by using the time relative alerts. Alerts are triggered when a fixed ratio reaches a set threshold compared to a past time frame.
{: shortdesc}

## Prereqs
{: #alerts-config-prereqs}
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

## Specify the logs that will be analyzed against the filtering criteria
{: step}
{: #alerts-config-3}
{: ui}


Complete the following steps to specify the logs that will be analyzed against the filtering criteria:

1. Specify a `Lucene` search query to specify the logs that will be returned as part of the alert.

    You can define a query that filters based on a free text string. For example, to trigger an alert when POST requests that have a return code of 403 are identified, you can enter `"POST 403"` as your search query. The query will look for logs that include the value `403` and `POST`.

    You can define a query that filters logs where a specific field matches the value in the query. For example, you can define a query to search for the value production in the environment field: `environment:"production"`

    You can define a query that filters logs where a specific field matches a range of numeric values using the format `[START_VALUE TO END_VALUE]`. For example, to search for logs that have 2xx status codes for a field `RC`, you can use the query: `rc.numeric:[400 TO 499]`

    You can define a query that filters logs where a specific field matches a regular expression (RegEx). Wrap the RegEx expression with `/`. For example, you can define a query to search for different regions such as `west-europe-1, west-europe-2, west-us-1` in a field region: `region:/west-(europe|us)-[12]/`

    You can define complex queries that use the Boolean operators `AND`, `OR`, and `NOT`. For example, you can define a query such as `environment:"production" AND status.numeric:[400 TO 499] NOT region:/west-(europe|us)-[12]/`

2. Add additional filtering of logs by choosing 1 or more applications.

3. Add additional filtering of logs by choosing 1 or more subsystems.

4. Add additional filtering of logs by choosing 1 or more log severites.

    Valid values are: `Debug`, `Verbose`, `Info`, `Warning`, `Error`, and `Critical`.


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

Trigger an alert. Once an alert is triggered and processed, the system sends notifications to the designated users or teams through various channels such as email, Slack, SMS, or integrated incident management platforms. You can then go to the *Incidents* page to see information about the alerts that are triggered. For more information, see [Managing triggered alerts in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-incidents).
