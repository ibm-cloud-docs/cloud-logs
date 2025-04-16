---

copyright:
  years:  2024, 2025
lastupdated: "2025-04-16"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Streaming data
{: #streaming}

Stream data from an {{site.data.keyword.logs_full}} instance to other corporate tools such as Security Information and Event Management (SIEM) tools by integrating {{site.data.keyword.logs_full}} and {{site.data.keyword.messagehub}}.
{: shortdesc}

When you stream data to data lakes, other analysis tools, or other SIEM tools, you can add additional capabilities to the ones provided by the {{site.data.keyword.logs_full_notm}} service:
- You can gain visibility into enterprise data across on-premises and cloud-based environments.
- You can identify and prioritize security threats that might affect your organization.
- You can detect vulnerabilities by using Artificial Intelligence (AI) to investigate threats and incidents.

For example, when you enable streaming on an {{site.data.keyword.logs_full}} instance, you configure {{site.data.keyword.logs_full}} to send data to an {{site.data.keyword.messagehub}} instance. Then, you can configure Kafka Connect to consume the data and forward it to your destination tool. Once the data is persisted within {{site.data.keyword.messagehub}}, you can configure any application or service to create a subscription and take action on the log data being streamed.

![Streaming example with {{site.data.keyword.messagehub}}](images/logs_streams.svg "Streaming examples with {{site.data.keyword.messagehub}}"){: caption="Streaming example with {{site.data.keyword.messagehub}}" caption-side="bottom"}


If you have any regulatory requirement for data residency and compliance needs, you must control the location where {{site.data.keyword.logs_full_notm}}, {{site.data.keyword.messagehub}}, Kafka Connect and the destination tool are available.
{: important}


## Configure streaming
{: #streaming-1}

For information on how to configure streaming, see [Integrating {{site.data.keyword.logs_full_notm}} with {{site.data.keyword.messagehub}}](/docs/cloud-logs?topic=cloud-logs-streaming-config).

Consider the following information when configuring the streaming feature between an {{site.data.keyword.logs_full_notm}} instance and an {{site.data.keyword.messagehub}} instance:
- The {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.messagehub}} instance must be provisioned in the same account.
- You must have the **manager** role for the {{site.data.keyword.logs_full_notm}} to configure streaming in the {{site.data.keyword.logs_full_notm}} instance.
- To connect the {{site.data.keyword.logs_full_notm}} instance to the {{site.data.keyword.messagehub}} instance, you need to define a service to service authentication. The credential that {{site.data.keyword.logs_full_notm}} uses to publish data in {{site.data.keyword.messagehub}} must have **writer** role. This role includes the **messagehub.topic.write** IAM action role that allows an app or service to write data to 1 or more topics.
- To create a topic in {{site.data.keyword.messagehub}}, you must have the **manager** role for the {{site.data.keyword.messagehub}} instance. This role includes the **messagehub.topic.manage** IAM action role that allows an app or user to create or delete topics.
- You can define DataPrime data rules to filter the data that you stream from {{site.data.keyword.logs_full_notm}} to {{site.data.keyword.messagehub}}. For more information, see [Configuring streaming data rules](/docs/cloud-logs?topic=cloud-logs-streaming_rules).




## Activity tracking events
{: #streaming-at}

The following activity tracking events are generated when you mange your streaming configuration:

| Action | Required permission |  Description |
|--------|-------------|-------------|
| `logs.logs-stream-setup.get` | reader | This event is generated when details about a specific streaming configuration between {{site.data.keyword.logs_full_notm}} to {{site.data.keyword.messagehub}} is retrieved. |
| `logs.logs-stream-setup.list` | reader | This event is generated when a list of all streaming configurations between {{site.data.keyword.logs_full_notm}} to {{site.data.keyword.messagehub}} is requested. |
{: caption="Events generated when configuring streaming" caption-side="bottom"}
