---

copyright:
  years:  2024
lastupdated: "2024-10-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring alerts
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

This condition you specifies differs depending on the alert type. 

| Alert type | Condition configuration information |
|------------|-------------------------------------|
| Standard alerts | [link](/docs/cloud-logs?topic=cloud-logs-alerts-config-standard#alerts-config-4-std) |
| Time relative alerts | [link](/docs/cloud-logs?topic=cloud-logs-alerts-config-time-relative#alerts-config-4-tr) |
| Unique count alerts | [link](/docs/cloud-logs?topic=cloud-logs-alerts-config-unique-count#alerts-config-4-uc) |
| Ratio alerts | [link](/docs/cloud-logs?topic=cloud-logs-alerts-config-ratio#alerts-config-4-ratio) |
| New value alerts | [link](/docs/cloud-logs?topic=cloud-logs-alerts-config-new-value#alerts-config-4-nv) |
| Flow alerts | [link](/docs/cloud-logs?topic=cloud-logs-alerts-config-flow#alerts-config-4-flow) |
{: caption="Condition configuration details by alert type" caption-side="bottom"}


{{/_include-segments/alerts-config-notif.md}}


{{/_include-segments/alerts-set-schedule.md}}


{{/_include-segments/alerts-save-config.md}}


{{/_include-segments/alerts-next-steps.md}}
