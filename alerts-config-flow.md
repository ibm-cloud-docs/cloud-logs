---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-16"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring flow alerts
{: #alerts-config-flow}

A flow alert is designed to notify you when any combination of alert events occurs in a specific sequence within a defined time frame.
{: shortdesc}

For example, to monitor when the rate of HTTP requests increase because of high CPU utilization, you can define a Flow Alert that triggers when an alert that monitors a high HTTP error rate triggers within a defined timeframe followed by a high CPU utilization alert.

Some uses of flow alerts include:

* Comprehensive data correlation: You can correlate alerting on logs, metrics, and security events. This multifaceted approach provides a holistic view of your system's performance, not just isolated slices of information, ensuring you have all the data you need to make informed decisions.

* Advanced root cause analysis: Flow alerts can be configured to identify the root cause of an issue. With the ability to define an alert that already pinpoints the root cause, you can promptly respond to issues, thus reducing system downtime and enhancing operational efficiency.

* Reduced alert fatigue: Traditional monitoring systems often flood users with redundant alerts, leading to alert fatigue and the potential overlooking of critical issues. By applying an ordered, time-bound criteria filter, flow alerts significantly reduce false alerts. This means that you only get alerted when all the set conditions are met, saving you from unnecessary notification noise.

   You can further declutter your notifications by enabling phantom mode for individual alerts comprising a flow alert. Then, only the flow alert triggers the notification sequence and creates an incident, while its constituent alerts remain silenced.

* Customizable alert sequences: With flow alerts you can define your alerting sequence with a simple drag-and-drop interface. Create a flow that triggers only if all criteria are met by order and time, providing an intuitive and custom monitoring experience.

* Efficient troubleshooting: With the ability to visualize the sequence of alerts on a canvas, troubleshooting becomes easier and more efficient. You can easily identify patterns, understand the chain of events leading to an alert, and quickly act to rectify the issue.

* Optimized resource utilization: You will save significant time and resources by reducing false alerts and enabling root cause identification. This optimization lets your team focus on more strategic tasks, rather than being occupied with a constant stream of false alerts.


## Understanding flow logs building blocks
{: #flow-logs-bb}

The flow builder tool is used to visually combine and then chain the user-defined alerts that will trigger a flow alert. The basic building blocks of the flow alert are stages and groups.

A group represents a logical combination of individual user-defined alerts. The group supports `OR`, `AND`, and `NOT` logical operators to combine multiple individual alerts.

![Example flow logs groups](/images/flow-logs-groups.png "Flow logs groups in flow builder tool"){: caption="Flow logs groups in flow builder tool" caption-side="bottom"}

A stage represents alert groups that need to trigger within a specified timeframe. Multiple groups can be present in a stage.

![Example flow logs stages](/images/flow-logs-stages.png "Flow logs stages in flow builder tool"){: caption="Flow logs stages in flow builder tool" caption-side="bottom"}


## Flow logs limitations
{: #flow-logs-limits}

Flow logs have the following limitations:

* The cumulative timeframe for all stages cannot exceed 168 hours (1 week). If you insert a timeframe exceeding the limit, the input will reset to zero.

* A maximum of 30 alerts can be included into a single flow alert.

* The following alert types do not support the `NOT` logical operator:

   * [New value alerts](/docs/cloud-logs?topic=cloud-logs-alerts-config-new-value)

   * [Unique count alerts](/docs/cloud-logs?topic=cloud-logs-alerts-config-unique-count)

   * [Notify immediately alerts](/docs/cloud-logs?topic=cloud-logs-alerts-config-standard)


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


## Define the alert flow
{: step}
{: #alerts-config-4-flow}

1. Click **Open Flow Builder**. The builder dialog dispays with the previously configured alerts in the **Existing alerts** panel.

2. Drag and drop existing alerts from the **Existing alerts** panel into the flow builder workspace area.

3. Organize alerts into groups and stages.

4. Set a timefram for each stage.

5. Click **Apply** to save the alert flow.

6. Select the **Group By** keys.

   The available keys will be the intersection group between the different alerts. For example, if *Alert A* is grouped by `Region` and by `Cluster`, and *Alert B* is grouped by `Region` and by `Pod`, the alert flow will only be able to be grouped by `Region`, and not by `Cluster` or `Pod`, since that is the only group by option available to both alerts in the flow. You can see which group by options are available for each alert in the alert builder by hovering over the alert and viewing the alert description.


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
