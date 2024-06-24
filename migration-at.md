---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating {{site.data.keyword.at_full_notm}} instances
{: #migration-at}

Migrating {{site.data.keyword.at_full}} instances to {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}} require the configuration of the {{site.data.keyword.atracker_full_notm}} service in the account and provisioning {{site.data.keyword.logs_full_notm}} instances. A migration tool is provided to help you migrate.
{: shortdesc}


## Overview
{: #at-overview}

You currently have two options to manage activity tracking events in an account. You can use {{site.data.keyword.atracker_full_notm}} (a platform service) to route auditing events in your account to a destination by configuring targets and routes that define where activity tracking events are sent. For more information, see [About IBM Cloud Activity Tracker Event Routing](/docs/atracker?topic=atracker-about). Alternatively, you can [provision {{site.data.keyword.at_full_notm}} instances](/docs/activity-tracker?topic=activity-tracker-provision) in regions to collect and monitor events in your account. You can also use {{site.data.keyword.atracker_full_notm}} to route events to your {{site.data.keyword.at_full_notm}} instances.

Migrating from {{site.data.keyword.at_full_notm}} instances to {{site.data.keyword.logs_full_notm}} requires that you configure {{site.data.keyword.atracker_full_notm}} and provision {{site.data.keyword.logs_full_notm}} instances to replace the existing {{site.data.keyword.at_full_notm}} instances. Any {{site.data.keyword.atracker_full_notm}} configuration routing to {{site.data.keyword.at_full_notm}} instances must also be migrated. Migration is done for each {{site.data.keyword.at_full_notm}} instance in an account.

The following image shows a high-level view of how {{site.data.keyword.atracker_full_notm}} and {{site.data.keyword.logs_full_notm}} are integrated so you can monitor and alert on activity tracking events.

![Account overview of handling activity tracking events.](/images/migration-at-1.png "Account overview of handling activity tracking events."){: caption="Figure 1. Overview of handling activity tracking events in an account" caption-side="bottom"}

## Checklist to plan for migration
{: #at-checklist}

Consider these items when you are planning your migration of {{site.data.keyword.at_full_notm}} instances in an account:

- [ ] Check whether you use {{site.data.keyword.atracker_full_notm}} to control and route where activity tracking events are sent. If you are using {{site.data.keyword.atracker_full_notm}}, [identify if you are routing events to {{site.data.keyword.at_full_notm}} instances.](/docs/atracker-cli-plugin?topic=atracker-cli-plugin-atracker-v2-cli#target-list-v2-cli-cos) Are those instances located in the same account or in a different account?

- [ ] Identify the regions where you operate and in which of those regions there are provisioned {{site.data.keyword.at_full_notm}} instances.

- [ ] Check your requirements for long-term storage. Do you have [archiving](/docs/activity-tracker?topic=activity-tracker-manage_events#manage_events_archive) configured for each {{site.data.keyword.at_full_notm}} instance? How long do you need to keep the data?

    In {{site.data.keyword.logs_full_notm}}, you can query all data that is stored in your configured {{site.data.keyword.cos_full_notm}} bucket. You own and maintain the bucket and the data stored in it. A separate archiving solution is not required.
    {: note}

- [ ] Are you streaming any data to other 3rd-party tools?

    The data format of activity tracking events is not changed with the deprecation of the {{site.data.keyword.at_full_notm}} service.
    {: important}

- [ ] Are you [excluding any data at ingestion](/docs/activity-tracker?topic=activity-tracker-exclusion_rules) to reduce costs that would be useful to keep for search or even for compliance? The {{site.data.keyword.logs_full_notm}} service offers a TCO feature to help you optimize costs based on data criticality and operational requirements.

- [ ] Are you controlling data usage by configuring {{site.data.keyword.at_full_notm}} [index rate alerts](/docs/activity-tracker?topic=activity-tracker-control_usage_index_rate&interface=ui)?

- [ ] Do you [control access](/docs/activity-tracker?topic=activity-tracker-iam) by using access groups? Do you use trusted profiles or service IDs? [Identify the policies](/docs/activity-tracker?topic=activity-tracker-iam#iam_accesspolicy) in the account that grant permissions to operate the {{site.data.keyword.at_full_notm}} instances in each account.

- [ ] What [notification channels](/docs/activity-tracker?topic=activity-tracker-channels) do you use for alerting? Email, Slack, PagerDuty, webhook, {{site.data.keyword.mon_full_notm}} (Sysdig).


## Migration steps
{: #at-migration-steps}

To migrate {{site.data.keyword.at_full_notm}} instances in the account, complete the following steps:

1. Run the migration tool to collect information about what instances need to be migrated and their resources.

    ```text
    ibmcloud logging migrate generate-terraform --scope account --service logdnaat
    ```
    {: pre}


2. Migrate each instance by running the one of these commands:

    * To generate Terraform scripts that you can modify, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --terraform
       ```
       {: pre}

       After you generate the Terraform scripts, modify them as required and apply by using Terraform.

    * To migrate an instance by applying Terraform, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --terraform -f
       ```
       {: pre}

    * To migrate an instance directly without Terraform, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --api
       ```
       {: pre}

3. Manually configure notification channels such as email and PagerDuty.

    If you use the terraform option, variables are provided for you to enter information on the slack URL and the webhook header apikey.

    {{site.data.keyword.logs_full_notm}} alerting is done by using the {{site.data.keyword.en_full_notm}} service.
    {: note}

4. After you migrate each of the {{site.data.keyword.at_full_notm}} instances in the account, configure {{site.data.keyword.atracker_full_notm}} by running this command.

    ```text
    ibmcloud logging migrate create-resources --scope atracker
    ```
    {: pre}

    If {{site.data.keyword.atracker_full_notm}} is already configured, the migration tool adds an extra target in each rule where an {{site.data.keyword.at_full_notm}} target is identified.

    If {{site.data.keyword.atracker_full_notm}} is not already configured, the tool configures the account to map your current {{site.data.keyword.at_full_notm}} routing to the new {{site.data.keyword.logs_full_notm}} instance. A new route is added to configure {{site.data.keyword.atracker_full_notm}} after migration to send events to an {{site.data.keyword.logs_full_notm}} instance.

5. Validate that the new configuration is working for your requirements.

6. After you validate that your migrated configuration is as required, remove {{site.data.keyword.at_full_notm}} from your current configuration.

   1. Clean up your {{site.data.keyword.atracker_full_notm}} configuration.

      1. Remove any {{site.data.keyword.at_full_notm}} targets from route rules.

      2. Delete any {{site.data.keyword.at_full_notm}} targets.

   2. Delete your {{site.data.keyword.at_full_notm}} instances.
