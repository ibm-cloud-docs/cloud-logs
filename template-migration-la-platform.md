---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-21"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Planning for the migration of Analysis instances with platform logs flag enabled in the account
{: #template-migration-la}

Plan for your migration of {{site.data.keyword.la_full}} instances with the platform flag enabled to {{site.data.keyword.logs_full_notm}} instances.
{: shortdesc}

Migrating {{site.data.keyword.la_full_notm}} instances to {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}} requires:
- Migration of the {{site.data.keyword.la_full_notm}} instance
- Configuration of the logging agent to send data to the Cloud Logs instance
- Configuration of IBM Cloud Logs Routing to define to which Cloud Logs instance platforms logs generated in a region are routed


![High-level view of the migration tool](/images/migration-la-12.png "High-level view of the migration tool"){: caption="High-level view of the migration tool" caption-side="bottom"}


When you configure the IBM Cloud Logs Routing service, you are controlling where platform logs are routed in the account. For migration, it is very important that you first configure IBM Cloud Logs Routing and define a `Log Analysis` target to configure the current default behavior in the account. Afterwards, you can define a `Cloud Logs` target to send the same data to the migrated {{site.data.keyword.logs_full_notm}} instance. If you do not define a Log Analysis target first, platform logs will stop being routed to your current {{site.data.keyword.la_full}} instance.
{: important}

Always run the migration tool in a development or staging environment to test and validate the migration command and steps.
{: important}


The following list outlines the services that you need access to to migrate an {{site.data.keyword.la_full_notm}} instance:

- Cloud Object Storage (to store data and metrics)

- Event Notifications (to trigger alerts through Email, PagerDuty, Slack, webhook)

- {{site.data.keyword.logs_full_notm}} (the new logging service in IBM Cloud Observability)

- Event Streams for managing streaming of data through a topic

- IBM Cloud Logs Routing



## Migration steps
{: #template-migration-la-3}

- [ ] Identify the regions where you have provisioned Log Analysis instances to collect platform logs.

- [ ] [Migrate 1 instance of Log Analysis with platforms log enabled by using the migration tool](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-la-plat).
