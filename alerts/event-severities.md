---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Event severities
{: #event-severities}


The following table lists the severities that {{site.data.keyword.logs_full_notm}} can send to {{site.data.keyword.en_short}} and are used to set the priority of the event when an alert is triggered:





| Event severity       | Alert Priority | Description |
|----------------------|----------------|-------------|
| `INFO`               | `P5`           | Use for information purposes. |
| `LOW`                | `p4`           | Use for information purposes.
| `WARNING`            | `P3`           | Use to issue a warning. |
| `ERROR`              | `P2`           | Use to report errors detected. |
| `CRITICAL`           | `P1`           | Use to report critical situations. |
{: caption="Event severities" caption-side="bottom"}




The alert priority value is used to classify alerts that are triggered in the *Incidents* page.
