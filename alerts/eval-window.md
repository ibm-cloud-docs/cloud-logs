---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Changing the alert evaluation window
{: #eval-window}

Lags in your data pipeline can cause delays in log and metric ingestion by {{site.data.keyword.logs_full}}, potentially leading to false alerts. While alert conditions are evaluated in real-time, delayed data that arrives later can retroactively affect whether those conditions are met.
{: shortdesc}

When an alert is to be triggered when a user-defined threshold is exceeded, missing data might delay the alert or lead to an incorrect resolution. Conversely, when an alert is to be triggered when less-than a user-defined threshold, incomplete data can cause a false-positive alert or delayed alert resolution.

By configuring a delay in the alert evaluation, you can mitigate timing issues by shifting an alert's evaluation time frame backward by a specific amount of time. This adjustment can ensure that alert conditions are evaluated against a complete dataset, accounting for late-arriving logs or metrics.

By delaying the alert evaluation, you can reduce the risk of false positives or negatives that are caused by real-time data fluctuations and improve the accuracy and reliability of your alerts.

You can configure an alert evalution delay for the following alert types:

* [Standard](/docs/cloud-logs?topic=cloud-logs-alerts-config-standard)
* [Ratio](/docs/cloud-logs?topic=cloud-logs-alerts-config-ratio)
* [Time Relative](/docs/cloud-logs?topic=cloud-logs-alerts-config-time-relative)
* [Metric](/docs/cloud-logs?topic=cloud-logs-alerts-config-metric)

## Configuring an alert evaluation delay
{: #eval-window-config}

To configure an evaluation delay for an alert:

1. Create a new alert or edit an existing alert.

2. Under **Conditions** click **Advanced settings**.

3. Select **Delay alert evaluation** and select the number of seconds to delay the evaluation.

   The delay can be a maximum of 3 hours (10800 seconds).


