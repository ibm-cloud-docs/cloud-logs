---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-11"

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


{{/_include-segments/alerts-prereq.md}}


{{/_include-segments/alerts-alerts-mgmt.md}}


{{/_include-segments/alerts-choose-type.md}}


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



{{/_include-segments/alerts-config-notif.md}}


{{/_include-segments/alerts-set-schedule.md}}


{{/_include-segments/alerts-save-config.md}}


{{/_include-segments/alerts-next-steps.md}}
