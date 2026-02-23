---

copyright:
  years:  2024, 2026
lastupdated: "2026-02-23"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Creating an {{site.data.keyword.en_short}} template
{: #event-notifications-create-template}

An {{site.data.keyword.en_full_notm}} template defines the layout and content of notifications (email, webhook, Slack, etc.). Templates can include images, static text, and dynamic content (variables, conditional logic) based on events.
{: shortdesc}

{{site.data.keyword.en_short}} supports two types of templates:

1. User-defined templates: You can design your own templates to structure notification messages.

1. [Pre-defined templates](/docs/event-notifications?topic=event-notifications-en-predefinedTemplates): These are standard templates defined for a pair of specific source and destination. You can customize pre-defined templates to create a user defined template.


## Creating a user-defined template
{: #en-create-template}

1. In the {{site.data.keyword.cloud_notm}} console, click the **menu** icon ![hamburger icon](images/icon_hamburger.svg) > **Platform Automation** > **Event notifications**.
1. Click the name of your {{site.data.keyword.en_short}} instance.
1. Select **Templates** from the left panel. Then, click **Create**.
1. Enter details about the template such as the name and description.
1. Select a template type and add the template block.

    * [Custom Email Notification](/docs/event-notifications?topic=event-notifications-en-email-templates)
    * [Custom Email Invitation](/docs/event-notifications?topic=event-notifications-en-email-templates)
    * [Webhook Notification](/docs/event-notifications?topic=event-notifications-en-webhook-notifications-template)
    * [Slack Notification](/docs/event-notifications?topic=event-notifications-en-slack-notification-template)
    * [PagerDuty Notification](/docs/event-notifications?topic=event-notifications-en-pagerduty-notification-template)
    * [Event Streams Notification](/docs/event-notifications?topic=event-notifications-en-event-streams-notification-template)
    * [Code Engine Notification](/docs/event-notifications?topic=event-notifications-en-code-engine-notification-template&interface=ui)
    * [App Configuration Notification](/docs/event-notifications?topic=event-notifications-en-app-configuration-notification-template&interface=ui)

    For more information, see [{{site.data.keyword.en_short}} supported templates](/docs/event-notifications?topic=event-notifications-en-create-en-template#en-create-template).

1. Click **Add** to save your updates.
