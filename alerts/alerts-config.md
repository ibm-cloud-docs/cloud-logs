---

copyright:
  years:  2024
lastupdated: "2024-10-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring alerts
{: #alerts-config}

{{site.data.keyword.logs_full_notm}} alerts allow for timely detection of anomalies, proactive incident response, improved mean time to resolution (MTTR), reduced manual monitoring effort, customization, and flexibility. Powered by machine learning, alerting proactively notifies teams of potential problems, correlates incidents, and provides root cause analysis.
{: shortdesc}

Notification and escalation

   Once an alert is triggered and processed, the system sends notifications to the designated users or teams. Notifications can be delivered through various channels such as email, Slack, SMS, or integrated incident management platforms. If the situation remains unresolved, the alert can be escalated to higher-level teams or individuals.



Setting conditions for Notification groups

## group_by_fields
The group_by_fields is only not required on "Notify Immediately" alerts or on "New Value" alerts.


```
{
  "name": 'Dev - 20 or more "no route to host" in last 5 mintues-slack-54e116c62f',
  "is_active": true,
  "severity": "info_or_unspecified",
  "condition":
    {
      "more_than":
        {
          "parameters":
            {
              "threshold": 20,
              "timeframe": "timeframe_5_min_or_unspecified",
              "group_by": ["coralogix.metadata.applicationName"],
              "ignore_infinity": true,
              "relative_timeframe": "hour_or_unspecified",
            },
          "evaluation_window": "rolling_or_unspecified",
        },
    },
  "notification_groups":
    [
      {
        "group_by_fields": ["coralogix.metadata.applicationName"],
        "notifications": [{ "integration_id": 124 }],
      },
    ],
  "filters":
    {
      "text": 'NOT coralogix.metadata.subsystemName:/ibm-master-proxy-static.*/ NOT coralogix.metadata.subsystemName:/metrics-server.*/ NOT coralogix.metadata.subsystemName:/bob.*/ NOT coralogix.metadata.subsystemName:/docker.*/ tag.keyword:/registry.*/ "no route to host"',
      "filter_type": "text_or_unspecified",
    },
  "incident_settings":
    {
      "retriggering_period_seconds": 60,
      "notify_on": "triggered_and_resolved",
      "use_as_notification_settings": true,
    },
  "Headers": null,
}
```

```
{
    "name": "Dev - 20 or more \"no route to host\" in last 5 mintues-email-4aaf8cbf0a",
    "is_active": true,
    "severity": "info_or_unspecified",
    "condition": {
        "immediate": {}
    },
    "notification_groups": [
        {
            "notifications": [
                {
                    "integration_id": 124,
                    "retriggering_period_seconds": 60,
                    "notify_on": "triggered_and_resolved"
                }
            ]
        }
    ],
    "filters": {
        "text": "NOT coralogix.metadata.subsystemName:/ibm-master-proxy-static.*/ NOT coralogix.metadata.subsystemName:/metrics-server.*/ NOT coralogix.metadata.subsystemName:/bob.*/ NOT coralogix.metadata.subsystemName:/docker.*/ tag.keyword:/registry.*/ \"no route to host\"",
        "filter_type": "text_or_unspecified"
    },
    "incident_settings": {
        "retriggering_period_seconds": 60,
        "notify_on": "triggered_and_resolved",
        "use_as_notification_settings": true
    }
}
```
Problem seems to be the group by field which is not supported in "Notify Immediately" alert types


## Timeframe

supported time frame values and what is the respective seconds for that for retriggering_period_seconds

Here are the timeframe and corresponding retrigger values
Tmeframe                                  Suggested Retrigger_Period
timeframe_1_min                           60
timeframe_2_min                           120
timeframe_5_min_or_unspecified            300
timeframe_10_min                          600
timeframe_15_min                          900
timeframe_20_min                          1200
timeframe_30_min                          1800
timeframe_1_h                             3600
timeframe_2_h                             7200
timeframe_3_h                             10800
timeframe_4_h                             14400
timeframe_6_h                             21600
timeframe_12_h                            43200
timeframe_24_h                            86400
timeframe_36_h                            129600
timeframe_48_h                            172800
timeframe_72_h                            259200
timeframe_1_w                             604800
timeframe_1_m                             2592000
timeframe_2_m                             5184000
timeframe_3_m                             7776000


On the alert definition the condition is more than 5 minutes but the ‘notify every’ is set for 60 seconds.
What it means? that every minute you are rolling the window and triggering the alert based on the results
So if the log arrived at 00:04
alert will trigger at 00:05 (window 00:00 - 00:05)
also at 00:06 (window 00:01 - 00:06)
also at 00:07 ( window 00:02 - 00:07) ETC
The solution will be to set notify every the same as condition time frame.

who is getting three alerts every two minutes.
Which service and item can they change this setting?
