---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-21"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Template for tasks for migrating Log Analysis instances collecting logs in the account
{: #template-migration-logs}

Template to plan migration from {{site.data.keyword.la_full}} instances to {{site.data.keyword.logs_full_notm}} instances.
{: shortdesc}


Migrating {{site.data.keyword.la_full_notm}} instances to {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}} requires:
- Migration of the {{site.data.keyword.la_full_notm}} instance
- Configuration of the logging agent to send data to the Cloud Logs instance


Always run the Migration Tool in a development or staging environment to test and validate the migration command and steps.
{: important}


The following list outlines the services that you need access for migration an {{site.data.keyword.la_full_notm}} instance:

- Cloud Object Storage (to store data and metrics)

- Event Notifications (to trigger alerts through Email, PD, Slack, webhook)

- {{site.data.keyword.logs_full_notm}} (the new logging service in IBM Cloud Observability)

- Event Streams for managing streaming of data through a topic in Event Streams



## Migration planning
{: #template-migration-logs-3}

- [ ] Identify the regions where you have provisioned Log Analysis instances to collect platform logs.
- [ ] [Tutorial for migrating 1 Log Analysis instance in the account by using the migration tool](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-la).
