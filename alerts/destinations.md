---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-31"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Working with notification channels
{: #destinations}

A destination in {{site.data.keyword.en_short}} defines the connectivity details for a notification channel.

You can only define one notification channel per destination.

For a complete list of supported destinations, see the [{{site.data.keyword.en_short}} documentation](/docs/event-notifications?topic=event-notifications-en-destination).
{: tip}



## Slack
{: #destinations-email}


You can configure a slack destination. For more information, see [Configuring a slack destination](/docs/event-notifications?topic=event-notifications-en-destinations-slack).

You can configure a custom template. For more information, see [Slack Notification Template](/docs/event-notifications?topic=event-notifications-en-slack-notification-template).

When a message of length greater than 3000 characters is sent to slack, the message text gets truncated with leaders [...].
{: note}



## Webhooks
{: #destinations-webhook}

You can configure a webhook destination so that an incoming notification can be consumed programmatically by an app or service. For more information about setting up webhooks, check out the [{{site.data.keyword.en_short}} documentation](/docs/event-notifications?topic=event-notifications-en-destinations-webhook).

If a call to the webhook URL fails even after retry attempts, the notification is lost. For more information, see [Webhook retry policy](/docs/event-notifications?topic=event-notifications-en-destinations-webhook#en-webhook-retry).
{: note}

You can configure a custom template. For more information, see [Webhook Notification Template](/docs/event-notifications?topic=event-notifications-en-webhook-notifications-template).


## PagerDuty
{: #destinations-pagerduty}

You can configure a PagerDuty destination. For more information, see [Configuring a PagerDuty destination](/docs/event-notifications?topic=event-notifications-en-destinations-pagerduty).

Only [event alerts](https://developer.pagerduty.com/docs/send-alert-event){: external} are sent to Pagerduty.{: note}


PagerDuty enforces a 512 KB event size limit that applies to the full event payload that {{site.data.keyword.logs_full_notm}} sends to {{site.data.keyword.en_short}}.
{: note}

The following table outlines the mapping of fields between the {{site.data.keyword.en_short}} service and PagerDuty:

| PagerDuty field | {{site.data.keyword.en_short}} mapping |
|-----------------|----------------------------------------|
| `routing_key`   | `routing_key`  (Destination configuration)   |
| `event_action`  | Only `trigger` action is supported |
| `payload.summary` | Set to the event `ibmendefaultlong` field |
| `payload.source` |
| `payload.severity` | Set to the event `ibmenseverity` field.  |
| `payload.timestamp` | Set to the event `time` field |
| `payload.custom_details` | Set to the event `data` object |
{: caption="Supported PagerDuty alert events" caption-side="bottom"}

The following table outlines th emapping of severity across the different components:

| {{site.data.keyword.logs_full_notm}} severity | {{site.data.keyword.en_short}} severity | PagerDuty severity |
|---------------------------------------|-----------------------------------------|--------------------|
| `CRITICAL`                            | `Critical`                              | `critical`         |
| `ERROR`                               | `Error`                                 | `error`            |
| `WARNING`                             | `Warning`                               | `warning`          |
| `INFO`                                | `Info`   (Default Severity)             | `info`             |
| Anything Else | Info |
{: caption="{{site.data.keyword.en_short}} severity to PagerDuty severity mapping" caption-side="bottom"}



## Email notifications
{: #destinations-email}

You can configure email as a type of destination. Only

Event Notifications provides the following email destination types:

- Inbuilt Email

    Inbuilt Email destination provides a SMTP relay for sending transactional and informational event notification emails to recipients who need to be aware of events that happen within your {{site.data.keyword.cloud_notm}} account.

    This destination can be used to send email notifications for events originating only from {{site.data.keyword.cloud_notm}} sources.
    {: important}

    The content sent cannot be modified.

    This destination is provided out of the box, and is available whenever you create an instance of the {{site.data.keyword.en_short}} service.

    These emails originate from `no-reply@cloud.ibm.com` or `event-notifications@cloud.ibm.com`.

    You can add your own reply-to address.

    You can add this type of destination directly to a subscription along with the email addresses of interest.

    Read the information in this topic before [Creating a subscription to the IBM Cloud Email service destination type](/docs/event-notifications?topic=event-notifications-en-create-en-subscription#en-Email-destination).

    To receive detailed information about an event notification in your email, select the **Add notification payload** option when you create an {{site.data.keyword.en_short}} subscription. Your email displays the [notification payload details](/docs/cloud-logs?topic=cloud-logs-event-payload) that are associated with the event.
    {: tip}

    For more information, see [Inbuilt Email](/docs/event-notifications?topic=event-notifications-en-destination-email-destination-default).

- {{site.data.keyword.cloud_notm}} Email service with custom domain

    Custom Domain Email destination empowers you to tailor your communication by adding your own domain.

    You now have the flexibility to send emails using the email address associated with your specific domain, creating a personalized touch to your correspondence, by sending your own email content.

    You can configure a custom email template. For more information, see [Email Templates](/docs/event-notifications?topic=event-notifications-en-email-templates).

    For more information, see [IBM Cloud Email service with custom domain](/docs/event-notifications?topic=event-notifications-en-destinations-custom-email).


## ServiceNow
{: #destinations-servicenow}

You can configure a ServiceNow destination. For more information, see [Configuring a ServiceNow destination](/docs/event-notifications?topic=event-notifications-en-destinations-servicenow).
