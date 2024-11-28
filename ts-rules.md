---

copyright:
  years:  2024
lastupdated: "2024-11-28"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why are the log priority levels different from what I am expecting in my logs?
{: #ts-rules}
{: troubleshoot}
{: support}

The severity of log records that defines the log priority does not match the log priority that is set before sending it to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

You have one or more log records with severities that do not match the log priority that is set before sending it to {{site.data.keyword.logs_full_notm}}.
{: tsSymptoms}



Some issues that can cause log priority levels to be set with a different of what you expect:
- You might not be setting the log priority before sending it to log priority that is set before sending it to {{site.data.keyword.logs_full_notm}}.
- A parsing rule in your instance is enabled and sets the severity of a log record.
{: tsCauses}




Check that you set the log records that you send to {{site.data.keyword.logs_full_notm}} with a log priority. If it is, check if you have parsing rules configured in your instance that change the value set for the Severity field associated to each log record.
{: tsResolve}
