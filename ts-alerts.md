---

copyright:
  years:  2024, 2026
lastupdated: "2026-08-10"

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
{: troubleshoot}


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

![Finding the TCO pipeline for a log. The TCO value must display high or medium for alerts on the log to be sent.](/images/tsa_01.png){: caption="Finding the TCO pipeline for a log" caption-side="bottom"}

If the `TCO` value is `low`, then the log is being sent to the {{site.data.keyword.compliance}} pipeline and alerts cannot be triggered by logs in the {{site.data.keyword.compliance}} pipeline. 


## Has enough time elapsed?
{: #ts-alert-time}
{: troubleshoot}


Consider the following timing considerations with alerts.

* When you change your alert configuration, it can take up to 15 minutes for alerts to be triggered with the new or changed configuration.

* If an alert is configured to be sent immediately when a log with the matching criteria is received, the log can be seen in the UI before the alert is triggered.

   A 1-minute period must elapse between when {{site.data.keyword.logs_full_notm}} receives a log and an immediate alert is triggered.
   {: note}

## Is your alert correctly configured?
{: #ts-alert-config}
{: troubleshoot}


While you might think that a log matches the criteria for an alert to be triggered, an alert configuration error might exist that keeps the alert from being triggered.

Review your alert configuration for errors such as:

* Does the values of the `Application`, `Subsystem`, and `Severity` of the alert configuration match the values of the log that triggers the alert?

* Are any `field.keyword` values greater than 256 characters in length? {{site.data.keyword.logs_full_notm}} supports a maximum field length of 256 characters.

* Is your alert querying a value in an array? {{site.data.keyword.logs_full_notm}} does not support querying values in arrays. Use the [extract parsing rule](/docs/cloud-logs?topic=cloud-logs-parse-extract-rule&interface=ui) to extract the required array information to fields before querying.

* Does your alert query contain too many operators? Up to 48 operators (`AND`/ `OR`) can be included in an alert query.

* Are you using parentheses in your query to determine [operator precedence](/docs/cloud-logs?topic=cloud-logs-query-data-lucene#lucene-operators)? Are your parentheses correctly coded?



For more information, see [Configuring alerts in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-alerts-config). 

## Is {{site.data.keyword.en_full_notm}} correctly configured?
{: #ts-alert-en-config}

If {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.en_full_notm}} are not correctly configured, your alert will not trigger your intended notification. See [Configuring the integration with the {{site.data.keyword.en_short}} service](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure) for information about configuring the integration between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.en_full_notm}}.


## Why does the alert not fire?
{: #ts-alert-not-fire}
{: troubleshoot}


An alert is configured in {{site.data.keyword.logs_full_notm}} but does not trigger even though the expected logs are present.
{: shortdesc}

Follow the below checks to identify and resolve the issue

1. Does the alert query fire when rewritten as `.keyword` regex?

Rewrite the alert query in the following form: 


   ```text
   field.keyword:/.*value.*/
   ```
   {: codeblock}

   The `.keyword` sub-field stores the raw, un-tokenized value and bypasses the Lucene analyzer entirely, which produces consistent and predictable results in the alert engine. The `.*` anchors on both sides match any field value that contains the specified text.

If the rewritten query now matches the expected logs, replace the original query with the `.keyword` form and save the alert.

2. Are string values quoted and special characters escaped?

  You can check of all plain string values are enclosed in double quotation marks so that they are matched as a phrase. For example, use `status:"payment failed"` instead of `status:payment failed`.

3. Does the query value contain token shorter than three characters
  
  The Lucene analyzer drops tokens that are shorter than three characters during indexing. Values such as `v2`, `01`, or `5` are silently removed from standard text fields and cannot be matched by a direct field query.

  If your alert query includes a short value, move the query to the `.keyword` sub-field and use a regex pattern to bypass the analyzer. For example, use `log_level.keyword:/.*v2.*/` instead of `log_level:"v2"`.

4. Is the target field inside an array or a nested structure?
  
   The alert engine does not support querying values that are nested inside arrays or nested structures. If the field that you want to match is stored in an array, the alert query never matches it.

5. Are logs assigned to a higher or medium TCO tier?

  The alert engine evaluates only logs that are assigned to the Medium or High TCO tier. Logs in the Low tier are excluded from alert evaluation entirely.

  Confirm that the logs you want to alert on are assigned to the Medium or High priority tier. For more information about checking the TCO tier for a log, see [Are alerted logs sent to the compliance pipeline?](/docs/cloud-logs?topic=cloud-logs-ts-alerts#ts-alert-wrong-pipeline).

  If the logs are in the Low tier, reconfigure your TCO policy so that those logs flow to either the {{site.data.keyword.frequent-search}} or {{site.data.keyword.monitoring}} pipeline.

6. Did you wait 15 minutes after editing the alert?
   
   After you save a change to an alert, allow up to 15 minutes for the alert engine to apply the updated configuration. The alert engine continues to evaluate logs against the previous query until the update is active. Testing the alert immediately after saving a change can produce misleading results.

7. If the alert still does not fire
   
   If you have verified all of the preceding checks and the alert still does not fire, collect the following information and contact {{site.data.keyword.cloud_notm}} support:

     * A raw sample of a log that you expect to trigger the alert, including all field names and values.
     * The full alert definition, including the query, conditions, and notification settings.
     * The alert URL and, if available, the incident URL from the alert history.
     * The exact date and time when the alert was expected to fire but did not, including the time zone.


## Why does an alert fire when it should not?
{: #ts-alert-false-positive}
{: troubleshoot}

An alert fires repeatedly even though the conditions that should trigger it are not met.
{: shortdesc}

An alert is configured in {{site.data.keyword.logs_full_notm}} and fires, but the triggering conditions do not appear to be met. For absence or "less than" alert types, the alert fires even though the expected logs are present.

Follow the below checks to identify and resolve the issue

1. Is the query mis-parsing or matching nothing?

For absence and "less than" alert types, if the alert query fails to match any logs, the alert engine treats the absence condition as met and fires. This is the most common cause of false positives for these alert types.

Apply the following fixes to the query:

Rewrite the query by using the `.keyword` sub-field with an anchored regex pattern:

   ```text
   field.keyword:/.*value.*/
   ```
   {: codeblock}

   The `.keyword` sub-field stores the raw, un-tokenized value and bypasses the Lucene analyzer. The `.*` anchors on both sides match any field value that contains the specified text.

Escape any special characters in the value.

2. Is the query matching unintended logs because of a loose term match?
 
 An unquoted term query is passed through the Lucene analyzer, which can match unintended substrings.

 Tighten the query to an exact `.keyword` match so that only logs where the field value precisely equals the intended value are matched. For example, replace `status:error` with `status.keyword:/.*error.*/` and anchor the pattern as specifically as possible to the intended value.

3. Is the evaluation delay too short for absence alerts?
 
  Add or increase the evaluation delay in the alert configuration to allow sufficient time for all logs to be ingested before the window is evaluated. The appropriate delay depends on your typical ingestion latency. Start with a delay of at least 5 minutes and increase it if premature triggers persist.

4. If false positives persist with a correct query
  

If you have applied all of the preceding fixes and the alert still fires incorrectly, collect the following information and contact {{site.data.keyword.cloud_notm}} support:

   * A raw sample of the logs that were present during the false positive, including all field names and values.
   * The full alert definition, including the query, alert type, conditions, and evaluation delay setting.
   * The alert URL and the incident URL from the alert history.
   * The exact date and time of each false positive, including the time zone.
