---

copyright:
  years:  2024
lastupdated: "2024-10-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring alerts
{: #alerts-config}

Create an alert in {{site.data.keyword.logs_full_notm}} for early detection of anomalies, proactive incident response, or improved mean time to resolution (MTTR).



{{../_include-segments/alerts-prereq.md}}


{{../_include-segments/alerts-mgmt.md}}

## Choose the type of alert to configure
{: #alerts-config-2}
{: step}

In the *Details* section, complete the following steps:

1. Enter a name and a description.

    - The maximum length of the name is 4096 characters.

    - The maximum length of the description is 4096 characters.

2. Define the severity of the alert.

    Valid values are: `Info`, `Warning`, `Error`, and `Critical`.

3. Add labels.

    Labels are key:value pairs that you can use later for quick searching.

4. Choose the alert type. For more information, see [Alert types](/docs/cloud-logs?topic=cloud-logs-alerts#alert-types).


## Specify the logs that will be analyzed against the filtering criteria
{: #alerts-config-3}
{: step}

Complete the following steps to specify the logs that will be analyzed against the filtering criteria:

- Specify a search query to specify the logs that will be returned as part of the alert.

    You can define a query that filters based on a free text string. For example, to trigger an alert when POST requests that have a return code of 403 are identified, you can enter `POST 403` as your search query. The query will look for logs that include the value `403` and `POST`.

    You can define a query that filters logs where a specific field matches the value in the query. For example, you can define a query to search for the value production in the environment field.

    You can define a query that filters logs where a specific field matches a range of numeric values using the format `[START_VALUE TO END_VALUE]`. For example, to search for logs that have 2xx status codes for a field `RC`, you can use the query `rc.numeric:[400 TO 499]`.

    You can define a query that filters logs where a specific field matches a regular expression (RegEx). Wrap the RegEx expression with `/`. For example, you can define a query to search for different regions such as `west-europe-1, west-europe-2, west-us-1` in a field region: `region:/west-(europe|us)-[12]/`

    You can define complex queries that use the Boolean operators `AND`, `OR`, and `NOT`. For example, you can define a query such as `environment:production AND status.numeric:[400 TO 499] NOT region:/west-(europe|us)-[12]/`

- Add additional filtering of logs by choosing 1 or more applications.

- Add additional filtering of logs by choosing 1 or more subsystems.

- Add additional filtering of logs by choosing 1 or more log severites.

    Valid values are: `Debug`, `Verbose`, `Info`, `Warning`, `Error`, and `Critical`.


## Specify the triggering condition
{: #alerts-config-4}
{: step}

Specify the triggering condition that is evaluated against the data included for analysis for this alert.

In the *Conditions* section, you must configure the fields in **Alert When** and **Group By**.

This condition is different based on the type of alert that you configure. {: note}

### Standard alerts
{: #alerts-config-4-std}

In **Alert When**, you must select whether to trigger the alert immediately, or you can define a rule that is based on the number of occurrences within a specified time window, or you can choose to configure a dynamic alert that detects abnormal behavior automatically.

- Choose `Notify Immediately` to be notified immediately, as soon as 1 log record is evaluated to match the filtering criteria.

- Choose `More Than` to be notified when the count of the entries matching the alert definition is more than the chosen threshold.

- Choose `Less Than` to be notified when the count of the entries matching the alert definition is less than the chosen threshold.

- Choose `More Than Usual` to be notified immediately by triggering a dynamic alert that detects abnormal behavior automatically, without setting fixed threshold values. You must define the minimum threshold only. If you select this type, notice that it takes one week for the algorithms to learn the traffic pattern and trigger based on data flowing through the system.

The following table lists the options that you get to configure this type of alert:

| Alert when           | Occurrences | Time window |
|----------------------|-------------|-------------|
| `Notify Immediately` | Option not available | Option not available |
| `More Than`  `[*]`   | Set a number | Valid options are: 5 minutes, 10 minutes, 15 minutes, 20 minutes, 30 minutes, 1 hour, 2 hours, 4 hours, 6 hours, 12 hours, 24 hours, 36 hours |
| `Less Than`          | Set a number | Valid options are: 5 minutes, 10 minutes, 15 minutes, 20 minutes, 30 minutes, 1 hour, 2 hours, 4 hours, 6 hours, 12 hours, 24 hours, 36 hours |
| `More Than Usual`    | Set a number | Valid options are: 5 minutes, 10 minutes, 15 minutes, 20 minutes, 30 minutes, 1 hour, 2 hours, 4 hours, 6 hours, 12 hours, 24 hours |
{: caption="Table 1. Standard alert conditions" caption-side="bottom"}

`[*]`When the alert is set to `More than`, you can select an Evaluation Window type that defines the frequency to evaluate the filtering criteria. Choose one of the following options:

- `Rolling Window`:  The Rolling Window defines a fixed period of time such as 5 minutes, regardless of matching data and any alerts triggered as a result of the query.

    For example, if you choose a rolling window with a time window of 5 minutes, the filtering criteria is evaluated each passing 5 minute interval, so from the moment it is enabled, the alert is evaluated every minute.

    By default, this option is set for new alerts.

    If you choose a small time window, like 5 minutes, and you continue to get logs that match the filtering criteria, you will get events generated every minute and the data evaluated might alredy be included to trigger the previous event.

- `Dynamic Duration`: The Dynamic Duration evaluation window changes the queried period when data matching the query triggers an alert.

    For example, if any event matches the conditions and is triggered, the alert's window will start once more from the time of the event going fwd

    With this option, the alert does not retrigger on already matched logs. However, there might be edge cases where an alert is not triggered while waiting to be reactivated after being triggered.


In **Group By**, you can configure up to 2 JSON fields whose values are aggregated and determine when an alert is triggered.

- An alert is triggered when any of the aggregated values appear more than the threshold configured in the filtering conditions section within the specified timeframe.

- An alert is triggered when the condition threshold is met for a specific aggregated value within the specified timeframe.

- If you configure 2 values, matching logs will first be aggregated by the parent field, then by the child field. An alert will fire when the threshold meets the unique combination of both parent and child.



## Configure the notification details
{: #alerts-config-5}
{: step}

Complete the following steps:

1. Configure **Notify every** to define how often you want to get an event once the alert is triggered. By default is set to 0 hours and 10 minutes.

2. Enable **Notify when resolved** to get an event when the event has been resolved.

    When the alert's condition is no longer triggering events, the event that is trigered initially is marked as resolved.

3. Enable **Enable phantom mode** to indicate that this alert is a phantom alert.

    A Phantom alert serves as a building block for flow alerts.

    A Phantom alert does not trigger independent event notifications.

    When you enable this option, *Notifications* section  is removed from the alert definition.

4. Add an integration.

    You must have an outbound integration defined to be able to add an integration. For more information, see [Configuring the integration with the Event Notifications service](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure).



## Step 6. Set a schedule and what log content to include
{: #alerts-config-6}
{: step}

Complete the following steps:

1. In the *Schedule* section, set a Schedule to control when this alert is enabled. You can choose specific days and times.

2. In the *Notification Content* section, define whether you want to include a sample log line or only some fields in the event that is triggered.

    Choose specific JSON keys to include in the alert notification, or leave this blank to include the full log text in the alert message:

    - Option 1: Leave blank to include one log line that matches the filtering conditions of the alert.

    - Option 2: Specify JSON keys to include selected fields in the format of key:value pairs. Notice that to be able to add fields, your log records must be in JSON format.

    - Option 3: Specify a  JSON path as the filter.




## Save the alert configuration
{: #alerts-config-7}
{: step}

Complete the following steps:

1. Verify the alert.

    Click **Verify** to evaluate data to find out how many times the alert matched the criteria in the last 24 hours.

    Verify evaluates data in the {{site.data.keyword.frequent-search}} pipeline only. If your alert is configured to trigger on data that is available in the {{site.data.keyword.monitoring}} pipeline, notice that this feature is not available.{: important}

2. Click **CREATE ALERT**.


## Next
{: #alerts-config-next}

Once an alert is triggered and processed, the system sends notifications to the designated users or teams. Notifications can be delivered through various channels such as email, Slack, SMS, or integrated incident management platforms. If the situation remains unresolved, the alert can be escalated to higher-level teams or individuals.
