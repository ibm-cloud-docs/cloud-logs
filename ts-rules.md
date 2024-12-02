---

copyright:
  years:  2024
lastupdated: "2024-12-02"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why is the severity of some of my logs different from what I am expecting?
{: #ts-rules}
{: troubleshoot}
{: support}

The severity of log records that you can see through the UI does not match the severity that is set before sending it to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

You have one or more log records with a severity that does not match the severity that you expect.
{: tsSymptoms}



Some issues that can cause severity to be set with a different value of what you expect:
{: tsCauses}

- The data that you send by using the {{site.data.keyword.agent}} sets the severity based on information in your log record or `info` if the agent is unable to determine the severity of the log record. For more infoirmation, see [About the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about#agent-about-ov).
- The data that you send by using the Ingestion REST API sets the severity based on the data in the parameter *severity*. If the parameter severity is not included, `debug` is set as the default value.
- A parsing rule in your instance is enabled and sets the severity of a log record overriding the agent's behaviour or the ingestion by using the REST API. For more information, see [Parsing rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules).



Check that you set the log records that you send to {{site.data.keyword.logs_full_notm}} with a severity. If it is, check if you have parsing rules configured in your instance that change the value set for the severity field associated to each log record.
{: tsResolve}
