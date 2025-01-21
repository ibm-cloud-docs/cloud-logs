---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-21"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Template for migrating Activity Tracker instances in the account
{: #template-migration-at}

Template to plan migration from 1 {{site.data.keyword.at_full}} instance to 1 {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}


## Overview
{: #template-migration-at-ov}

Migrating {{site.data.keyword.at_full}} instances to {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}} requires the configuration of the {{site.data.keyword.atracker_full_notm}} service in the account to define where events are routed and the provisioning of {{site.data.keyword.logs_full_notm}} instances. A migration tool is provided to help you migrate.

![High-level view of the migration tool](/images/migration-at-1.png "High-level view of the migration tool"){: caption="High-level view of the migration tool" caption-side="bottom"}

Options to migrate:
- Option 1: Migrate the {{site.data.keyword.at_full}} instance by using the migration tool, and then, configure manually the {{site.data.keyword.atracker_full_notm}} service afterwards.
- Option 2: Migrate the {{site.data.keyword.at_full}} instance and configure the {{site.data.keyword.atracker_full_notm}} service by running the migration tool.

When you configure the {{site.data.keyword.atracker_full_notm}} service, you are taking the control in the account where events are routed. For migration, it is very important that when you configure {{site.data.keyword.atracker_full_notm}}, you define first a `logdna` target and a route for the region where the {{site.data.keyword.at_full}} instance is available so you configure the current default behavior in the account. Afterwards, you can define a `cloud_logs` target and route to send the same data to the migrated {{site.data.keyword.logs_full_notm}} instance. If you do not define a logdna target first, events will stop being routed to your current {{site.data.keyword.at_full}} instance.
{: important}


Always run the Migration Tool in a development or staging environment to test and validate the migration command and steps.
{: important}

The following list outlines the services that you need access for migration an {{site.data.keyword.at_full}} instance:

- Cloud Object Storage (to store data and metrics)

- Event Notifications (to trigger alerts through Email, PD, Slack, webhook)

- {{site.data.keyword.logs_full_notm}} (the new logging service in IBM Cloud Observability)

- {{site.data.keyword.atracker_full_notm}} for managing how events are routed in the account

- Event Streams for managing streaming of data through a topic in Event Streams


## Migration
{: #template-migration-at-3}

- [ ] Identify the regions where you have provisioned Activity Tracker instances.

For each instance, choose one of the following options:
- [Tutorial for migrating 1 Activity Tracker instance in the account end to end](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-at-option2).
- [Tutorial for migrating 1 Activity Tracker instance in the account in steps](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-at-option1).
- [Tutorial for configuring Activity Tracker in the account for a new setup that does not require migration](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-at-option3).
