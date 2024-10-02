---

copyright:
  years:  2024
lastupdated: "2024-10-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_full_notm}} events
{: #destinations}

A destination in {{site.data.keyword.en_short}} defines the connectivity details for a notification channel.

You can only define one notification channel per destination.

For a complete list of supported destinations, see the [{{site.data.keyword.en_short}} documentation](/docs/event-notifications?topic=event-notifications-supported-destinations).
{: tip}



### Email notifications
{: #event-notifications-email}

You can use the [{{site.data.keyword.cloud_notm}} email service](/docs/event-notifications?topic=event-notifications-en-destinations-email) as a delivery channel for {{site.data.keyword.logs_full_notm}} event notifications. [Create an {{site.data.keyword.en_short}} subscription](/docs/event-notifications?topic=event-notifications-en-create-en-subscription) between an existing topic and the {{site.data.keyword.cloud_notm}} email service to forward your alerts to various recipients by email.

To receive detailed information about an event notification in your email, select the **Add notification payload** option when you create an {{site.data.keyword.en_short}} subscription. Your email displays the [notification payload details](#event-notifications-payload) that are associated with the event.
{: tip}


### Webhooks
{: #event-notifications-webhook}

You can configure a webhook destination so that an incoming notification can be consumed programmatically by an app or service. For more information about setting up webhooks, check out the [{{site.data.keyword.en_short}} documentation](/docs/event-notifications?topic=event-notifications-en-destinations-webhook).
