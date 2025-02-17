---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating to {{site.data.keyword.logs_full_notm}}
{: #migration-intro}

Learn about migrating {{site.data.keyword.la_full}} or {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

As of 28 March 2024, the {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} services are deprecated and will no longer be supported as of 30 March 2025. You will need to migrate to {{site.data.keyword.logs_full_notm}}, which replaces these two services, prior to 30 March 2025.
{: important}

## How does this announcement affect you?
{: #migration-intro-how}

You might need to:

- Migrate the {{site.data.keyword.at_full_notm}} architecture.

    If you use {{site.data.keyword.at_full_notm}} to collect and manage activity tracking events that are generated by {{site.data.keyword.cloud_notm}} services, you will need to configure {{site.data.keyword.atracker_full_notm}} to send your activity tracking events to another destination such as {{site.data.keyword.logs_full_notm}}.

- Migrate the {{site.data.keyword.la_full}} architecture.

    If you use {{site.data.keyword.la_full}} to collect and manage logs that run in {{site.data.keyword.cloud_notm}} or outide the {{site.data.keyword.cloud_notm}}, you will need to configure your hosts, services, or applications to send data to {{site.data.keyword.logs_full_notm}}. For example, you will have to deploy a new agent to send logs from your Kubernetes clusters.

- Migrate the platform logs architecture.

    If you use {{site.data.keyword.la_full}} to collect and manage platform logs that are generated by {{site.data.keyword.cloud_notm}} services, you will need to configure {{site.data.keyword.logs_routing_full_notm}} to send your platform logs to {{site.data.keyword.logs_full_notm}}.

- Migrate the {{site.data.keyword.atracker_full_notm}} configuration.

    If you use {{site.data.keyword.atracker_full_notm}} to configure the routing of activity tracking events to {{site.data.keyword.at_full_notm}} instances, you will need to configure the service to route the activity tracking events to {{site.data.keyword.logs_full_notm}} ddestinations.

- Reconfigure sources to send data to the new {{site.data.keyword.logs_full_notm}} instances. For example, you must deploy new agents to send logs from Kubernetes clusters.
- Update IAM permissions in the account.
- Modify run books.
- Update your disaster recovery process.
- Provision the {{site.data.keyword.en_full_notm}} service.

    In {{site.data.keyword.logs_full_notm}}, alerts are triggered through the {{site.data.keyword.en_full_notm}} service. If you do not currently use the service and have alerts configured in your {{site.data.keyword.at_full_notm}} instances, you must provision an instance of the {{site.data.keyword.en_full_notm}} service. For more information, see [Configuring an outbound integration for {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure).

The data format of activity tracking events and platform logs does not change.
{: important}


## Migrating your {{site.data.keyword.at_full_notm}} architecture
{: #migration-intro-at}

To migrate {{site.data.keyword.at_full_notm}} instances, you must provision 1 or more {{site.data.keyword.logs_full_notm}} instances to replace the existing {{site.data.keyword.at_full_notm}} instances, and configure {{site.data.keyword.atracker_full_notm}} to define the routing rules in the account that determine where the events that are generated are routed.

For more information, see:
- [Planning the migrating of your Activity Tracker instance](/docs/cloud-logs?topic=cloud-logs-template-migration-at).
- [Migrating 1 Activity Tracker instance in the account using the migration tool](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-at-option2).
- [Migrating 1 Activity Tracker instance in the account in steps](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-at-option1).
- [Configuring IBM Cloud Activity Tracker Event Routing in the account for an IBM Cloud Logs instance that was created without using the migration tool](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-at-option3).
- [Removing deprecated {{site.data.keyword.at_full_notm}} instances](/docs/cloud-logs?topic=cloud-logs-migration-remove-at).




## Migrating your {{site.data.keyword.la_full_notm}} architecture
{: #migration-intro-la}

To migrate {{site.data.keyword.la_full_notm}} instances that collect only operational and application logs, you must provision {{site.data.keyword.logs_full_notm}} instances in the account to replace the existing {{site.data.keyword.la_full_notm}} instances. You must also configure your data sources to send data to these {{site.data.keyword.logs_full_notm}} instances. Your data sources can be located in {{site.data.keyword.cloud_notm}}, on-prem, or running in another cloud. For example, you can configure an {{site.data.keyword.agent}} on supported platforms such as Kubernetes clusters, Red Hat OpenShift clusters, Linux and Windows servers, or send data directly to {{site.data.keyword.logs_full_notm}} by using the public or private ingress endpoint.

For more information, see:
- [Planning for the migration of Log Analysis instances collecting logs in the account](/docs/cloud-logs?topic=cloud-logs-template-migration-logs).
- [Migrating 1 Log Analysis instance in the account by using the migration tool](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-la).
- [Removing deprecated {{site.data.keyword.la_full_notm}} instances](/docs/cloud-logs?topic=cloud-logs-migration-remove-la)


To migrate {{site.data.keyword.la_full_notm}} instances that collect platform logs, you must configure {{site.data.keyword.logs_routing_full_notm}} and provision 1 or more {{site.data.keyword.logs_full_notm}} instances in the account to replace the existing {{site.data.keyword.la_full_notm}} instances that are configured to collect platform logs. For more information, see:
- [Planning for the migration of Analysis instances with platform logs flag enabled in the account](/docs/cloud-logs?topic=cloud-logs-template-migration-la).
- [Migrating 1 instance of Log Analysis with platforms log enabled by using the migration tool](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-la-plat).
- [Removing deprecated {{site.data.keyword.la_full_notm}} instances with platform logs enabled](/docs/cloud-logs?topic=cloud-logs-migration-remove-plat)
