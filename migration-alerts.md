---

copyright:
  years:  2024
lastupdated: "2024-09-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating alerts
{: #migration-alerts}

You can use the Migration tool to help you migrate alerts that you have configured in your {{site.data.keyword.at_full_notm}} instances and {{site.data.keyword.la_full_notm}} instances.
{: shortdesc}


## Before you begin
{: #migration-alerts-prereqs}

- Learn about migration. For more information, see [Migrating {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-migration-intro).

- Learn about the Migration tool. For more information, see [Migrating tool](/docs/cloud-logs?topic=cloud-logs-migration-tool).

- Learn about enabling event notifications for {{site.data.keyword.logs_full_notm}}. For more information, see [Enabling event notifications](/docs/cloud-logs?topic=cloud-logs-event-notifications-events).

- Learn about alerts. For more information, see [Alerting](/docs/cloud-logs?topic=cloud-logs-alerts).

- Learn about the {{site.data.keyword.en_full_notm}} service. For more information, see [What is Event Notifications?](/docs/event-notifications?topic=event-notifications-en-about).



### Alerting in {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}}
{: #migration-alerts-1}

When you configure alerts in an {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} instance, consider the following information:
- You must define a view and attach the alert to the view.
- You can define presence or absence alerts. For more information, see [Types of alerts](/docs/activity-tracker?topic=activity-tracker-alerts).
- You can notify through email, slack, webhook, {{site.data.keyword.mon_full_notm}}, and PagerDuty. For more information, see [Notification channels](/docs/activity-tracker?topic=activity-tracker-alerts#alerts_channels).
- When alerts are triggered, you cannot manage the triggered alerts through the UI.



### Alerting in {{site.data.keyword.logs_full_notm}}
{: #migration-alerts-2}


When you configure alerts in an {{site.data.keyword.logs_full_notm}} instance, consider the following information:
- Alerts are a type of resource. They are not dependent on views.
- You can define different types of alerts such as standard alerts, flow alerts, and new value alerts. For information on the alert types that are supported, see [Alerts](/docs/cloud-logs?topic=cloud-logs-alerts&interface=ui#alert-types).
- You can use the `Incidents` page to manage alerts that are triggered.
- Alerts are triggered through the {{site.data.keyword.en_full_notm}} service. You configure the notification channels and conditions that trigger the alert in the {{site.data.keyword.en_full_notm}} service.



## Integration with the {{site.data.keyword.en_full_notm}} service
{: #migration-alerts-3}



To configure alerting in {{site.data.keyword.logs_full_notm}}, complete the following steps:
1. In {{site.data.keyword.logs_full_notm}}, alerts are triggered through the {{site.data.keyword.en_full_notm}} service. If you do not currently use the service and have alerts configured in your {{site.data.keyword.at_full_notm}} instances or your {{site.data.keyword.la_full_notm}} instances, you must provision an instance of the {{site.data.keyword.at_full_notm}} service. For more information, see [Enabling event notifications for {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-event-notifications-events).

2. In IAM, define a service to service authorization between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance. For more information, see [Creating a S2S authorization to work with the {{site.data.keyword.en_full_notm}} service](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-en).

3. Configure an outbound integration in your {{site.data.keyword.logs_full_notm}} instance to connect it with the {{site.data.keyword.en_full_notm}} instance. For more information, see [Connecting to Event Notifications in the console](/docs/cloud-logs?topic=cloud-logs-event-notifications-events&interface=ui#event-notifications-enable-ui).

    This task creates a **source** definition in the {{site.data.keyword.en_full_notm}} instance, and an integration configuration in the {{site.data.keyword.logs_full_notm}} instance.

4. Define your alerts in the {{site.data.keyword.logs_full_notm}} instance. Select the outbound integration through which you want to notify when the alert is triggered.

5. Configure the {{site.data.keyword.en_full_notm}} instance to route event notifications when an alert is triggered in {{site.data.keyword.logs_full_notm}} to your target destinations.

    - Define 1 or more topics.

        A topic defines the alert conditions that you want to group together.

        For example, if you have multiple alert definitions in your {{site.data.keyword.logs_full_notm}} instance that notify through the same slack channel, you can configure these alerts within the same topic.

        Another example, if you have multiple alert definitions in your {{site.data.keyword.logs_full_notm}} instance that notify through different slack channels, you must configure as many topics as slack channels you use, and include in a topic the alerts that notify through the same slack channel.

    - Define 1 or more destinations.

        A destination defines a notification channel that you can use to notify when an alert is triggered.

        For more information on destinations, see [Supported destinations](/docs/event-notifications?topic=event-notifications-supported-destinations).

    - Define 1 or more subscriptions.

        A subscription links 1 topic with 1 destination.

        You must add subscriptions to define the alerts configured in a topic are the ones notified through the destination selected in the subcription configuration.


The following figure shows the high level view of an {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} service that you might configure:

![High-level view of an {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance](/images/alerts-cl-en-integration.svg "High-level view of an {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance"){: caption="Figure 1. High-level view of an {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance" caption-side="bottom"}



## Migrating alerts
{: #migration-alerts-4}

When you migrate an instance by using the Migration tool, alerts are migrated, an outbound integration is created and destinations are created. For more information, see [Migrating instances](/docs/cloud-logs?topic=cloud-logs-migration-instance).
{: note}



## Known issues
{: #migration-alerts-issues}



## Known Migration tool limitations
{: #migration-alerts-limitations}

- Currently, the Migration tool creates only 1 topic to handle notifications of all the alerts through that topic.
