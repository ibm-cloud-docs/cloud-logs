---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.logs_full_notm}} multi-condition alerts
{: #multi-condition}



With {{site.data.keyword.logs_full}}, you can configure one alert with up to 5 condition rules. Each condition rule defines a threshold, a time frame, and a priority. When a condition rule is met, an alert is triggered with the priority associated with that condition rule. If more than 1 condition rule meets the trigering criteria, the alert that trigers corresponds to the condition rule with the highest priority.
{: shortdesc}

Triggered alert conditions with their associated priority can be viewed in Incidents.

{{site.data.keyword.logs_full_notm}} has 5 priority values from highest priority to lowest priority:

* `P1`
* `P2`
* `P3`
* `P4`
* `P5`

These priority values determine the importance of the issue that is alerted.

Multiple conditions can be configured for the following alert types:

* [Standard alerts](/docs/cloud-logs?topic=cloud-logs-alerts-config-standard) [*]
* [Ratio alerts](/docs/cloud-logs?topic=cloud-logs-alerts-config-ratio)
* [Time-relative](/docs/cloud-logs?topic=cloud-logs-alerts-config-time-relative)
* [Metric](/docs/cloud-logs?topic=cloud-logs-alerts-config-metric)

[*] - Multiple conditions are not supported for notify immediately alerts.


## Condition processing
{: #mc-order}

When configuring multiple conditions for an alert, you need to be aware of how those conditions are processed and displayed.

### Alert triggering
{: #mc-trigger}

The condition rules determine an alert's priority when the alert condition is met and the alert is triggered.

If an alert matches the conditions for multiple priorities, the highest priority value is applied. For example, if an alert would trigger for a condition that is defined as `P1` and a condition that is defined as `P2` as well, the `P1` priority is applied to the alert. `P1` is the highest priority.

On the [*Incidents* page](/docs/cloud-logs?topic=cloud-logs-incidents) the alert will be displayed with a `P1` priority and the information that triggered the alert.

### Alert Management display
{: #mc-alert-mgmt}

When you configure alert conditions using the UI or API, only the priority of the first configured condition will be displayed on the [*Alert Management* page](/docs/cloud-logs?topic=cloud-logs-alerts-config) even if multiple conditions are configured.

If you always want the highest priority configured for the alert to be displayed on the *Alert Management* page, make sure the highest priority condition is the first configured condition.
{: tip}

## Time frame groups
{: #mc-tf-group}

Time frames for all conditions that are configured for an alert must be within the same time frame group.
{: note}

| Group | Time frame |
|-------|-----------|
| 1 | 1 minute - 30 minutes |
| 2 | 1 hour - 6 hours |
| 3 | 12 hours  - 36 hours |
{: caption="Timeframe groups" caption-side="bottom"}

For example, if you configure an alert condition with a time frame in group 2, all other conditions for that alert must also be in group 2.


## Conditions for metrics alerts
{: #mc-metrics}

For metric alerts, you can set the threshold when conditions are met `for at least`, `at least once`, or `for over x%` in a specific time period.

`for at least`
:   This option specifies that the condition must be met for the entire specified time period. For example, if you set `for at least 5 minutes`, the metric must exceed the threshold continuously for the entire 5-minute duration.

`at least once`
:   This option is the most minimal condition. The alert triggers if the threshold is crossed at least one time within the specified time period. For example, `at least once in 5 minutes` means that if the metric exceeds the threshold even one time within that 5-minute window, the alert is triggered.

`for over x%`
:   Use this option to set a duration percentage rather than a number of times the condition occurs. The `for over x%` option specifies that the condition must be true for more than a certain percentage of the time within the selected time window. For example, if you set `for over 10% of 10 minutes`, the metric must exceed the threshold for more than 1 minute (10% of 10 minutes) in that time period for the alert to trigger. If the percentage is set to 0 and the query crosses the threshold one time, an alert is triggered. If the percentage is set to 100, all of the time window values must exceed the threshold for the alert to trigger.
