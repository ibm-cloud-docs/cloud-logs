---

copyright:
  years:  2024
lastupdated: "2024-11-25"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why are my alerts not being sent?
{: #ts-alerts}
{: troubleshoot}
{: support}

Depending on how your alerts are configured in {{site.data.keyword.logs_full}}, those alerts might not be triggered as intended.
{: shortdesc}

You have one or more alerts that are configured in {{site.data.keyword.logs_full_notm}}. However, the alerts are not being sent as intended.
{: tsSymptoms}

Alerts not being sent can be due to a number of issues.
{: tsCauses}

Some issues that can cause alerts to not be sent include:

* Logs are processed into a [TCO pipeline](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines) that does not support alerts.
* Insufficient time has passed for the alert to be issued.
* The alert is incorrectly configured.
* Integration between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.en_full_notm}} is not correctly configured.


To resolve your alerting issues, you need to determine the cause of the problem, and then make the appropriate changes to your environment.
{: tsResolve}

## Are alerted logs sent to the {{site.data.keyword.compliance}} pipeline?
{: #ts-alert-wrong-pipeline}

If the logs where you are expecting alerts are being sent to the [{{site.data.keyword.compliance}} TCO pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer), then alerts are never sent on those logs. Alerts are only sent on logs in the {{site.data.keyword.frequent-search}} and {{site.data.keyword.monitoring}} pipelines.

If you need to alert on these logs, reconfigure your TCO pipelines so the logs flow to either the {{site.data.keyword.frequent-search}} or {{site.data.keyword.monitoring}} pipeline.

You can determine the pipeline where the log is being sent by using a DataPrime query in the {{site.data.keyword.logs_full_notm}} UI logs view:

```text
source logs
| filter $m.logid == '<LOG ID>'
| create $d.TCO from $m.priorityclass
```
{: codeblock}

Where `<LOG ID>` is the log ID value for the log that you are questioning.

To determine the log ID value, from the {{site.data.keyword.logs_full_notm}} UI logs view, do the following.

1. Hover over the log line number in question and click the three dots.
2. Click **Copy Permalink**.
3. Paste the value to a text editor.
4. Find the `<LOG ID>` value. This value is prefixed by `logId=`. For example, `f5a16fe9-9817-4976-8aaa-5a2ef7c8c1e7`

![Finding the TCO pipeline for a log. The TCO value must display high or medium for alerts on the log to be sent.](/images/tsa_01.png){: caption="Finding the TCO pipelie for a log" caption-side="bottom"}

If the `TCO` value is `low`, then the log is being sent to the {{site.data.keyword.compliance}} pipeline and alerts cannot be triggered by logs in the {{site.data.keyword.compliance}} pipeline. 


## Has enough time elapsed?
{: #ts-alert-time}

Consider the following timing considerations with alerts.

* When you change your alert configuration, it can take up to 15 minutes for alerts to be triggered with the new or changed configuration.

* If an alert is configured to be sent immediately when a log with the matching criteria is received, the log can be seen in the UI before the alert is triggered.

   A 1-minute period must elapse between when {{site.data.keyword.logs_full_notm}} receives a log and an immediate alert is triggered.
   {: note}

## Is your alert correctly configured?
{: #ts-alert-config}

While you might think that a log matches the criteria for an alert to be triggered, an alert configuration error might exist that keeps the alert from being triggered.

Review your alert configuration for errors such as:

* Does the values of the `Application`, `Subsystem`, and `Severity` of the alert configuration match the values of the log that triggers the alert?

* Are any `field.keyword` values greater than 256 characters in length? {{site.data.keyword.logs_full_notm}} supports a maximum field length of 256 characters.

* Is your alert querying a value in an array? {{site.data.keyword.logs_full_notm}} does not support querying values in arrays. Use the [extract parsing rule](/docs/cloud-logs?topic=cloud-logs-parse-extract-rule&interface=ui) to extract the required array information to fields before querying.

* Does your alert query contain too many operators? Up to 48 operators (`AND`/ `OR`) can be included in an alert query.

* Are you using parentheses in your query to determine [operator precedence](/docs/cloud-logs?topic=cloud-logs-query-data-lucene#lucene-operators)? Are your parentheses correctly coded?

* Is your log affected by [configured suppression rules](/docs/cloud-logs?topic=cloud-logs-suppression_rules)?

   ![Log affected by suppression rules.](/images/tsa_03.png){: caption="Log affected by suppression rules." caption-side="bottom"}

For more information, see [Configuring alerts in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-alerts-config).


## Is {{site.data.keyword.en_full_notm}} correctly configured?
{: #ts-alert-en-config}

If {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.en_full_notm}} are not correctly configured, your alert will not trigger your intended notification. See [Configuring the integration with the {{site.data.keyword.en_short}} service](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure) for information about configuring the integration between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.en_full_notm}}.

