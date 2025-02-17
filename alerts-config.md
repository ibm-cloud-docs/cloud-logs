---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-04"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring alerts in {{site.data.keyword.logs_full_notm}}
{: #alerts-config}

Create an alert in {{site.data.keyword.logs_full_notm}} for early detection of anomalies, proactive incident response, or improved mean time to resolution (MTTR).



{{/_include-segments/alerts-prereq.md}}


{{/_include-segments/alerts-alerts-mgmt.md}}


{{/_include-segments/alerts-choose-type.md}}


{{/_include-segments/alerts-choose-logs.md}}


## Specify the triggering condition
{: step}
{: #alerts-config-4}


Specify the triggering condition that is evaluated against the data included for analysis for this alert.

You must define your triggering condition. Do not leave the triggering condition configuration blank or you will have all logs generating alerts.
{: important}

This condition you specifies differs depending on the alert type. 

| Alert type | Condition configuration information |
|------------|-------------------------------------|
| Standard alerts | [link](/docs/cloud-logs?topic=cloud-logs-alerts-config-standard#alerts-config-4-std) |
{: caption="Condition configuration details by alert type" caption-side="bottom"}


{{/_include-segments/alerts-config-notif.md}}


{{/_include-segments/alerts-set-schedule.md}}


{{/_include-segments/alerts-save-config.md}}


{{/_include-segments/alerts-next-steps.md}}
