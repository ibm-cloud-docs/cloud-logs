---

copyright:
  years:  2024, 2025
lastupdated: "2025-04-28"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Streaming data from {{site.data.keyword.logs_full_notm}} to SIEM tools
{: #siem}

You can stream data from {{site.data.keyword.logs_full_notm}} to other corporate tools such as Security Information and Event Management (SIEM) tools.
{: shortdesc}

Streaming is handled by integrating {{site.data.keyword.logs_full_notm}} with {{site.data.keyword.messagehub}}.

See [Streaming data](/docs/cloud-logs?topic=cloud-logs-streaming) for information about streaming.

You can use {{site.data.keyword.messagehub}} with {{site.data.keyword.logs_full_notm}} to stream and manage log data. {{site.data.keyword.messagehub}} is a scalable, managed Apache Kafka service that lets applications send data by creating messages and sending them to a topic. Applications can subscribe to these topics to receive messages, enabling real-time data processing and analytics. 

See [Integrating {{site.data.keyword.logs_full_notm}} with {{site.data.keyword.messagehub}}](/docs/cloud-logs?topic=cloud-logs-streaming-config) for information about configuring the integration.

To [connect to your {{site.data.keyword.messagehub}} instance](/docs/EventStreams?topic=EventStreams-connecting#establishing_connection), you need the endpoint URLs for the APIs and the credentials for authentication.

To establish a connection, clients must be configured to use SASL PLAIN or SASL OAUTHBEARER over TLSv1.2 at a minimum and to require a username, and a list of the bootstrap servers. TLSv1.2 ensures that connections are encrypted and validates the authenticity of the brokers (to prevent man-in-the-middle attacks). SASL enforces authentication on all connections. For more information, see [Configuring your Kafka API client](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_api_client).
