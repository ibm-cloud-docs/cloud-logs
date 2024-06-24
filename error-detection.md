---

copyright:
  years:  2024
lastupdated: "2024-06-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Getting a daily report on error and critical log anomalies
{: #error-detection}

{{site.data.keyword.logs_full_notm}} learns from the received logs and groups similar logs into templates to help you determine logs requiring your attention and others that might not. You can configure your {{site.data.keyword.logs_full_notm}} instance to get reports that inform about detection of error and critical log anomalies daily.
{: shortdesc}

Not for GA
{: inportant}


After {{site.data.keyword.logs_full_notm}} analyzes incoming logs and flows over 5 days, {{site.data.keyword.logs_full_notm}} emails a daily digest to all users. The email includes all new errors and critical logs that occur in the system for the first time over the past 2 weeks. The email also includes a list of the top-10 errors for the past day.

After you review the email, you can use the {{site.data.keyword.logs_full_notm}} UI to view and analyze the detected logs by clicking links in the email.
