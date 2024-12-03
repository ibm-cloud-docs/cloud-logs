---

copyright:
  years:  2024
lastupdated: "2024-10-28"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Monitoring operational logs
{: #cl-operational-logs}

You can send infrastructure and application logs to an {{site.data.keyword.logs_full_notm}} instance by using the {{site.data.keyword.agent}} or by using the REST API. You can also configure a Linux {{site.data.keyword.agent}} on a Linux server to collect and route (r)Syslog data to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}



## By deploying the {{site.data.keyword.agent}}
{: #cl-operational-logs-agent}

The {{site.data.keyword.agent}} is based on the Fluent Bit open-source agent which is used to collect and process log data. You can deploy the {{site.data.keyword.agent}} in supported environments and manage data from various sources and formats. For more information, see [About the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about).


The following diagram shows the high level view of sources where you can deploy the {{site.data.keyword.agent}} to send logs directly to an {{site.data.keyword.logs_full_notm}} instance:

![Sources where the agent is supported](images/sending-logs-agent.svg "Sources where the agent is supported"){: caption="Flow of logs from agent" caption-side="bottom"}


## By using the Ingestion REST API
{: #cl-operational-logs-api}

You can send logs to an {{site.data.keyword.logs_full_notm}} instance by using the ingestion API. For more information, see [Sending logs by using the REST API](/docs/cloud-logs?topic=cloud-logs-send-logs-api).


## Using a Linux {{site.data.keyword.agent}} on a Linux server to collect and route rsyslog data
{: #cl-operational-logs-agent-collector}

You can configure a Linux {{site.data.keyword.agent}} on a Linux server to collect and route (r)Syslog data to an {{site.data.keyword.logs_full_notm}} instance.

{{site.data.keyword.logs_full_notm}} does not support a syslog endpoint.

The following diagram shows the high level view of a source, such as PowerVS, where you can configure rsyslog to send logs to a Linux server:

![Sources such as PowerVS where the agent is supported](images/sending-logs-agent-collector.svg "Sources where the agent is supported"){: caption="Flow of logs from agent" caption-side="bottom"}
