---

copyright:
  years:  2024
lastupdated: "2024-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Considerations and limitations sending data to {{site.data.keyword.logs_full_notm}}
{: #limits}

There are processing considerations and limitations you need to be aware of when using the {{site.data.keyword.agent}}.
{: shortdesc}

## Log length
{: #limit-log-length}

Logs processed by the {{site.data.keyword.agent}} cannot exceed 16 K in length.

## Handling of stringify JSON
{: #stringify-json}

How stringify JSON is handled depends on how the log information that is sent.

* If you sent data by using the [{{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about), which uses Fluent Bit, any stringify JSON is unchanged.

* If you sent data by using the [{{site.data.keyword.logs_full_notm}} API](/docs/cloud-logs?topic=cloud-logs-send-logs-api), stringify JSON has escape characters remove from text, log, and JSON fields as part of the API processing.
