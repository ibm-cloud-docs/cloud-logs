---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-11"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring new value alerts
{: #alerts-config-new-value}

The new value alert is triggered by the first occurrence of a new value within a time interval. All values are tested against a list that is dynamically created while the alert is active. The alert is set by a specific query that identifies a subset of logs (if needed), and is defined with a key to track for new values within the wanted interval.
{: shortdesc}

In many use cases, this alert lets you automatically detect possible abnormal behavior within your system.

For example:

Security: An alert might be triggered by a new domain connection.

Monitoring: An alert might be triggered by a new application error code. Many applications send an `error_code` field. A new value for this field indicates a new issue with the application.


{{/_include-segments/alerts-prereq.md}}


{{/_include-segments/alerts-alerts-mgmt.md}}


{{/_include-segments/alerts-choose-type.md}}


{{/_include-segments/alerts-choose-logs.md}}


## Specify the triggering condition
{: step}
{: #alerts-config-4-nv}


Specify the triggering condition that is evaluated against the data included for analysis for this alert.

In the *Conditions* section, configure your triggering condition:

In **Key to track** select the key you want to monitor for the alert.

In **Notify on new value in the last** select the time period to be monitored.

If there is a new value detected for the key within the selected time period, the alert will be triggered.


{{/_include-segments/alerts-group-by.md}}


{{/_include-segments/alerts-config-notif.md}}


{{/_include-segments/alerts-set-schedule.md}}


{{/_include-segments/alerts-save-config.md}}


{{/_include-segments/alerts-next-steps.md}}

