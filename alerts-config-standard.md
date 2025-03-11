---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-11"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring standard alerts
{: #alerts-config-standard}

Standard alerts are alerts that are triggered by changes to your logs. Triggered by crossing a set quantity threshold of specific logs, this feature allows you to monitor system performance, get notified when changes occur, and pinpoint potential causes. These alerts are useful when trying to measure the number of occurrences of a particular incident.
{: shortdesc}


{{/_include-segments/alerts-prereq.md}}


{{/_include-segments/alerts-alerts-mgmt.md}}


{{/_include-segments/alerts-choose-type.md}}


{{/_include-segments/alerts-choose-logs.md}}


## Specify the triggering condition
{: step}
{: #alerts-config-4-std}


Specify the triggering condition that is evaluated against the data included for analysis for this alert.

In the *Conditions* section, you must configure the fields in **Alert When** and **Group By**.

In **Alert When**, you must select whether to trigger the alert immediately, or you can define a rule that is based on the number of occurrences within a specified time window, or you can choose to configure a dynamic alert that detects abnormal behavior automatically.

- Choose `Notify Immediately` to be notified immediately, as soon as 1 log record is evaluated to match the filtering criteria.

   For `Notify Immediately` alerts, the alert is triggered as soon as 1 line meets the query criteria. {{site.data.keyword.logs_full_notm}} then waits for 1 minute before an additional `Notify Immediately` alert meeting the same query criteria is triggered. If the alert is not resolved, the `Notify` condition indicates how often you are notified of the same alert with a new event after it is triggered.

- Choose `More Than` to be notified when the count of the entries matching the alert definition is more than the chosen threshold.

   For `More Than` alerts configured for 0 lines within a time period, the alert is triggered as soon as 1 line meets the query criteria. The alert does not wait for the configured time threshold to trigger the alert.

- Choose `Less Than` to be notified when the count of the entries matching the alert definition is less than the chosen threshold.

- Choose `More Than Usual` to be notified immediately by triggering a dynamic alert that detects abnormal behavior automatically, without setting fixed threshold values. You must define the minimum threshold only. If you select this type, notice that it takes one week for the algorithms to learn the traffic pattern and trigger based on data flowing through the system.

The following table lists the options that you get to configure this type of alert:

| Alert when           | Occurrences | Time window |
|----------------------|-------------|-------------|
| `Notify Immediately` | Option not available | Option not available |
| `More Than`  `[*]`   | Set a number | Valid options are: 5 minutes, 10 minutes, 15 minutes, 20 minutes, 30 minutes, 1 hour, 2 hours, 4 hours, 6 hours, 12 hours, 24 hours, 36 hours |
| `Less Than`          | Set a number | Valid options are: 5 minutes, 10 minutes, 15 minutes, 20 minutes, 30 minutes, 1 hour, 2 hours, 4 hours, 6 hours, 12 hours, 24 hours, 36 hours |
| `More Than Usual`    | Set a number | Valid options are: 5 minutes, 10 minutes, 15 minutes, 20 minutes, 30 minutes, 1 hour, 2 hours, 4 hours, 6 hours, 12 hours, 24 hours |
{: caption="Standard alert conditions" caption-side="bottom"}

`[*]`When the alert is set to `More than`, you can select an Evaluation Window type that defines the frequency to evaluate the filtering criteria. Choose one of the following options:

- `Rolling Window`:  The Rolling Window defines a fixed period of time such as 5 minutes, regardless of matching data and any alerts triggered as a result of the query.

    For example, if you choose a rolling window with a time window of 5 minutes, the filtering criteria is evaluated each passing 5 minute interval, so from the moment it is enabled, the alert is evaluated every minute.

    By default, this option is set for new alerts.

    If you choose a small time window, like 5 minutes, and you continue to get logs that match the filtering criteria, you will get events generated every minute and the data evaluated might alredy be included to trigger the previous event.

- `Dynamic Duration`: The Dynamic Duration evaluation window changes the queried period when data matching the query triggers an alert.

    For example, if any event matches the conditions and is triggered, the alert's window will start once more from the time of the event going fwd

    With this option, the alert does not retrigger on already matched logs. However, there might be edge cases where an alert is not triggered while waiting to be reactivated after being triggered.


{{/_include-segments/alerts-group-by.md}}


{{/_include-segments/alerts-config-notif.md}}


{{/_include-segments/alerts-set-schedule.md}}


{{/_include-segments/alerts-save-config.md}}


{{/_include-segments/alerts-next-steps.md}}
