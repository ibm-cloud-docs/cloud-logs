---

copyright:
  years:  2024
lastupdated: "2024-10-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Managing triggered alerts in {{site.data.keyword.logs_full_notm}}
{: #incidents}

In {{site.data.keyword.logs_full_notm}}, you can use the *Incidents* page to view all triggered alerts and their status, and be able to drill-down into the underlying logs and metrics. You can also apply filters to display only the alerts that are triggered within a specific timeframe.


An incident defines one or more events of an alert that is triggered.

When an alert is triggered, you can see the alert displayed as an incident in the *Incidents* page.

Events within an incident are organized by key-value pairs under the *Group By* as tags.
- You can aggregate and display events based on these tags.
- If you configure the notification of your alert to trigger a separate alert for each key-value combination that meets your Group By conditions, you will see separate incidents for each key-value tag combination.
- If you configure the notification of your alert to trigger a single alert when at least one key-value tag combination meets your Group By conditions, all events for that alert will be consolidated within one incident in your Incidents screen.


## Incidents page
{: #incidents-page}

In the *Incidents* page, you can:

- View all the alerts which are currently triggered or those alerts that triggered within a specific time frame.

- Organize incidents by alert definition.

- Search alerts by name.

- Filter alerts by type, or severity.

- Manage the status by selecting and modifying the incident status.

- Drill-down into any triggered event to view its contextual information and underlying data.

- View alerts that are triggered in chronological order.


You can use the *Alert Explorer* to display all triggered alerts without grouping them into incidents and in chronological order. You can filter these alerts using the same methods as on the Incidents page.
{: tip}


## Changing the Incident status
{: #incidents-status}

You can see any of the following values to define the status of an incident:
- `TRIGGERED`
- `ACKNOWLEDGED`
- `RESOLVED`

The status of an incident can change automatically or a user can change it.

An incident changes status automatically from `TRIGGERED` to `RESOLVED` when:
- You have activated the **Notify When Resolved** setting in your alert definition.
- When the alert's condition is no longer triggering events, the event that is trigered initially is marked as resolved.
after an alert that has triggered

After an incident is marked as `RESOLVED`, an incident is closed and a new incident is created to report that the alert has triggered again after being resolved.

To change the status of an incident manually, click on the status `TRIGGERED`. A drop-down menu displays in which you can choose to `ACKNOWLEDGE` or `RESOLVE` an incident.

## Incident history and data
{: #incidents-history}

If you click on an incident, the detail page opens where you can get information on when the alert was triggered, the alert configuration and the log lines that were evaluated and matched the condition.

You can also click **Incident history** to get a full report on when this alert has been triggered in your environment.
