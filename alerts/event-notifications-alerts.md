---

copyright:
  years:  2024
lastupdated: "2024-10-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Configuring {{site.data.keyword.en_full_notm}}
{: #event-notifications-alerts}


After you enable notifications for {{site.data.keyword.logs_full_notm}}, create topics and subscriptions in {{site.data.keyword.en_short}} so that alerts can be forwarded and delivered to your selected destinations.

For a complete list of supported destinations, see the [{{site.data.keyword.en_short}} documentation](/docs/event-notifications?topic=event-notifications-supported-destinations).
{: tip}

### Email notifications
{: #event-notifications-alerts-destinations-email}

You can use the [{{site.data.keyword.cloud_notm}} email service](/docs/event-notifications?topic=event-notifications-en-destinations-email) as a delivery channel for {{site.data.keyword.logs_full_notm}} event notifications. [Create an {{site.data.keyword.en_short}} subscription](/docs/event-notifications?topic=event-notifications-en-create-en-subscription) between an existing topic and the {{site.data.keyword.cloud_notm}} email service to forward your alerts to various recipients by email.

To receive detailed information about an event notification in your email, select the **Add notification payload** option when you create an {{site.data.keyword.en_short}} subscription. Your email displays the [notification payload details](#event-notifications-payload) that are associated with the event.
{: tip}


### Webhooks
{: #event-notifications-alerts-destinations-webhook}

You can configure a webhook destination so that an incoming notification can be consumed programmatically by an app or service. For more information about setting up webhooks, check out the [{{site.data.keyword.en_short}} documentation](/docs/event-notifications?topic=event-notifications-en-destinations-webhook).
