---

copyright:
  years:  2024
lastupdated: "2024-10-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Alerting
{: #alerts}


{{site.data.keyword.logs_full_notm}} alerts allow for timely detection of anomalies, proactive incident response, improved mean time to resolution (MTTR), reduced manual monitoring effort, customization, and flexibility. Powered by machine learning, alerting proactively notifies teams of potential problems, correlates incidents, and provides root cause analysis.



## How alerting works
{: #alerts-how}

Alerts follow a general workflow for how they are generated, triggered, and delivered to users.

![Alerting in {{site.data.keyword.logs_full_notm}}](../images/alert-overview.svg "Alerting in {{site.data.keyword.logs_full_notm}}"){: caption="Figure 1. Alerting in {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}

1. Set alert rules

   Administrators, developers, or DevOps define alert rules within the observability platform. These rules specify the conditions under which an alert is triggered. For instance, they might set a rule to alert when specific error messages appear in the logs.

2. Data collection and analysis

   {{site.data.keyword.logs_full_notm}} continuously collects data from the system, including logs and metrics. It processes and analyzes this data against the defined alert rules.

3. Alert triggering

   When the monitored data meets the conditions that are specified in the alert rules, an alert is triggered. Triggering can be a result of a sudden spike in error rates, high latency, low resource availability, or any other predefined anomaly.

4. Alert aggregation and deduplication

   The alerting system might aggregate multiple similar alerts into a single notification to prevent overwhelming users with redundant notifications. Also, it may deduplicate alerts to avoid sending users repetitive information.

5. Notification and escalation

   Once an alert is triggered and processed, the system sends notifications to the designated users or teams. Notifications can be delivered through various channels such as email, Slack, SMS, or integrated incident management platforms. If the situation remains unresolved, the alert can be escalated to higher-level teams or individuals.

6. Alert resolution and acknowledgment

   The recipients of the alert acknowledge the alert and take appropriate actions to address the issue. Once the problem is resolved, they mark the alert as “Done”.

7. Monitoring and reporting

   Throughout the alerting process, {{site.data.keyword.logs_full_notm}} continuously monitors the system’s status. It can keep track of acknowledgment status, resolution time, and other metrics to generate reports and help with post-incident analysis and improvement.

## Alert types
{: #alert-types}

{{site.data.keyword.logs_full_notm}} provides 6 types of alerts that you can configure.

For more information on how to configure alerts, see ![Alerts icon](../icons/alerts.svg "Alerts") [Configuring alerts](/docs/cloud-logs?topic=cloud-logs-alerts-config).

### Standard alerts
{: #alert-standard}

Standard alerts are alerts that are triggered by changes to your logs. Triggered by crossing a set quantity threshold of specific logs, this feature allows you to monitor system performance, get notified when changes occur, and pinpoint potential causes. These alerts are useful when trying to measure the number of occurrences of a particular incident.

With standard alerts feature, you can:

* Monitor system performance in real-time. Obtain real-time insights based on the criteria of your choice.

* Construct the queries for your specific needs. Define a query that captures the logs that you want to inspect, and make the query more specific by filtering by application, subsystem, and severity. Then, select the range of conditions to trigger an alert. For example, you might set to trigger an alert when more than 10 logs are received over a specific time frame.

* Use a machine learning-based approach. Using this setting, {{site.data.keyword.logs_full_notm}} profiles your data and automatically detects abnormal behavior.

* Receive personalized notifications. Receive real-time push notifications to your preferred communication channel.

Standard alerts are the simplest alerts that are offered by {{site.data.keyword.logs_full_notm}}. These can be used to cover your most obvious use cases as a foundation for your observability system.


### Time relative alerts
{: #alert-timerelative}

Automatically detect abnormal behavior in your system by using the time relative alerts. Alerts are triggered when a fixed ratio reaches a set threshold compared to a past time frame.

Use time relative alerts to:

* Receive automatic alerts about changes in your system’s security, operations, or business behaviors over time.

* Compare between behaviors across different time periods. For example,

   Security
   :   Receive automatic alerts that compare suspicious behavior. Compare, for example, the number of NX domain name responses or admin logins across days or weeks.

   Operations
   :   Receive automatic alerts about error rates and page loading times in your applications. Compare, for example, error rates and page loading times in the past day or hour.

   Business
   :   Receive automatic alerts when a shift in sales or user signups occurs. Compare, for instance, the number of purchases on the same day last week or the user signups over the last month.

### Unique count alerts
{: #alert-uniquecount}

As data volumes grow and the number of alerts that are generated by logs, metrics, and security systems exponentially increases, one of the most powerful indicators of alert importance is the number of elements affected by the alert. Examples can include: the number of users who encountered a 5XX error when calling an API, the number of Kafka consumer groups that returned errors, the number of CDN locations that are currently loading your site for more than 3 seconds, or the number of different passwords that a single user attempts to log in with to your cloud service console.

The problem with most alerts is that they describe the problem. However, to understand the severity or broadness of the issue, users need to drill into the data or rely on dashboards.

Unique Count alerts trigger on the number of unique values inside a selected key that matches a specific search criteria. That is, the cardinality of a specific key matched to a search.

### Ratio alerts
{: #alert-ratio}

You can calculate a ratio between two log queries and trigger an alert when the ratio reaches a set threshold.

Use this ratio alerts to monitor:

* Operational health: Monitor the number of outgoing responses to incoming requests or the ratio of specific error codes to the overall number of errors.

* Marketing: Monitor the ratio between traffic from specific regions to overall traffic that follows regional campaigns.

* Security: Monitor the ratio of denied requests, specific administration operations, or requests originating from blocked network domains compared to all requests.

### New value alerts
{: #alert-value}

The new value alert is triggered by the first occurrence of a new value within a time interval. All values are tested against a list that is dynamically created while the alert is active. The alert is set by a specific query that identifies a subset of logs (if needed), and is defined with a key to track for new values within the wanted interval.

This alert can help you automatically detect a possible abnormal behavior within your system.

An example uses for this alert type include:

* Security: An alert can be triggered by a new domain connection. Since {{site.data.keyword.logs_full_notm}} security logs all security information across all network traffic, a new domain connection can result with the field `security.highest_registered_domain` having a new value. A new domain connection can point to a possible security attack.

* Monitoring: An alert can be triggered by a new application error code. Many applications send an `error_code` field. A new value for this field can indicate a new issue with the application.

### Flow alerts
{: #alert-flow}

A flow alert is designed to notify you when any combination of alert events occurs in a specific sequence within a defined time frame.

For example, to be notified of an increase in HTTP error rate caused by high CPU utilization, a flow alert can be configured to trigger when a high CPU utilization alert is followed by a high HTTP error rate alert within a defined time frame.

The following are some benefits of using flow alerts:

* Comprehensive data correlation: With flow alerts, you can correlate alerting on logs, metrics, and security events. This approach provides a holistic view of your system’s performance, not  isolated pieces of information. The correlated information helps you have all the data that you need to make informed decisions.

* Advanced root cause analysis: Flow alerts can be configured to identify the root cause of an issue. With the ability to define an alert that pinpoints the root cause of the issue, you can promptly respond to issues, thus reducing system downtime and enhancing operational efficiency.

* Reduced alert fatigue: Traditional monitoring systems often flood users with redundant alerts, leading to alert fatigue and the potential of overlooking critical issues. Flow alerts can reduce false alerts by applying an ordered, time-bound criteria filter. This means you are alerted when all the set conditions are met, reducing unnecessary notification noise.

* Customizable alert sequences: With this flow alerts unique feature that you can define your alerting sequence with a simple drag-and-drop interface. Create a flow that triggers only if all criteria are met by order and time.

* Efficient troubleshooting: With the ability to visualize the sequence of alerts on a canvas, troubleshooting becomes more efficient. You can easily identify patterns, understand the chain of events that lead to an alert, and quickly act to rectify the issue.

* Optimized resource utilization: By reducing false alerts and enabling root cause identification, you will save time and resources. With optimization your team can focus on more strategic tasks, rather than being occupied with a constant stream of false alerts.

{{site.data.keyword.logs_full_notm}} provides a flow builder tool to visually combine, and then chain together, the user-defined alerts that trigger a flow alert. The basic building blocks of the flow alert are stages and groups.

A group represents a logical combination of individual user-defined alerts. The group supports OR, AND, and NOT logical operators to combine multiple individual alerts.

A stage represents alert groups that need to trigger within a specified time frame. Multiple groups can be present in a stage.

Flow alerts have the following limitations:

* The flow alert must have a minimum of 2 stages.
* The first stage of a flow alert can contain only 1 group.
* The duration of the time frame in all stages cannot exceed 36 hours.
* You can combine a maximum of 30 alerts into a single flow alert.
* The following flow alert alert types do not support the NOT logical operator:
   * New value alerts
   * Unique count alerts
   * Notify immediately
   * Standard alerts
