---

copyright:
  years:  2024
lastupdated: "2024-07-09"
keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating {{site.data.keyword.atracker_full_notm}} routes and targets in the account
{: #migration-atracker}

If {{site.data.keyword.atracker_full}} is configured in your environment to route activity tracking events to {{site.data.keyword.at_full_notm}} instances, the migration tool can be used to migrate the {{site.data.keyword.atracker_full_notm}} configuration as well. The Migration tool modifies your {{site.data.keyword.atracker_full_notm}} configuration to route events to {{site.data.keyword.logs_full_notm}} instances created when your {{site.data.keyword.at_full_notm}} instances were migrated.
{: shortdesc}

You must migrate your {{site.data.keyword.at_full_notm}} instances that are associated with {{site.data.keyword.atracker_full_notm}} routes and targets before you migrate your {{site.data.keyword.atracker_full_notm}} routes and targets. For information on migrating your {{site.data.keyword.at_full_notm}} instances, see [Migrating {{site.data.keyword.at_full_notm}} instances](/docs/cloud-logs?topic=cloud-logs-migration-at).
{: requirement}

## Scenario
{: #migration-atracker-scenario}

Consider the following scenario.

- {{site.data.keyword.atracker_full_notm}} is configured in the account.
- You have {{site.data.keyword.at_full_notm}} instances provisioned in multiple locations.
- You must migrate your {{site.data.keyword.at_full_notm}} instances to {{site.data.keyword.logs_full_notm}} instances.
- You must migrate your {{site.data.keyword.atracker_full_notm}} configuration that routes events to {{site.data.keyword.at_full_notm}} instances to route events to {{site.data.keyword.logs_full_notm}} instances.



## Before you begin
{: #migration-atracker-prereqs}

- Learn about migration. For more information, see [Migrating {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-migration-intro).

- Learn about the migration tool. For more information, see [Migrating tool](/docs/cloud-logs?topic=cloud-logs-migration-tool).

The migration tool only migrates existing rules that route events to {{site.data.keyword.at_full_notm}} instances. If you have {{site.data.keyword.at_full_notm}} instances that are not configured to route events using {{site.data.keyword.atracker_full_notm}}, and you want to use {{site.data.keyword.atracker_full_notm}} to route the events, you must manually [configure {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-overview).{: important}

## What to expect
{: #atracker-migration-what}

When you run the migration tool to migrate your {{site.data.keyword.atracker_full_notm}} configuration in the account:

- The migration tool adds an extra `cloud-logs` target for each {{site.data.keyword.at_full_notm}} instance that you have in the account.

    There is a limited number of targets per account. You can define up to 16 targets in total in an account.

    Make sure that your {{site.data.keyword.atracker_full_notm}} configuration has enough targets available so that the migration tool can create 1 target per {{site.data.keyword.at_full_notm}} instance in the account.
    {: requirement}

    If you do not have enough targets, the migration process cannot be completed. Delete any unused targets and try again.

    If you cannot delete any existing targets, you must manually migrate your {{site.data.keyword.atracker_full_notm}} configuration. Manually create 1 or more {{site.data.keyword.logs_full_notm}} instances so that you can route events from the account to these instances. For more information, see [Getting started](/docs/atracker?topic=atracker-getting-started).

- The migration tool adds a new route to send events to the migrated {{site.data.keyword.logs_full_notm}} instances.

    The rules defined for {{site.data.keyword.at_full_notm}} instances are used as reference to create new rules to the newly created {{site.data.keyword.logs_full_notm}} instances.

    For example, if you have a route with a rule that sends `us-south` events to {{site.data.keyword.at_full_notm}} instance `A`, the migration tool adds a rule to a new route to send `us-south` events to the `cloud-logs` ({{site.data.keyword.logs_full_notm}}) target created by the migration tool from the {{site.data.keyword.at_full_notm}} instance `A`.



## Migration steps
{: #atracker-migration-steps}

To migrate {{site.data.keyword.atracker_full_notm}} routes and targets in the account, complete the following steps:

1. Migrate each {{site.data.keyword.at_full_notm}} instance in the account for which you have a target associated to a routing rule by running one of these commands:

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

    * To migrate an instance without applying Terraform, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --api
       ```
       {: pre}

    Check the locations where {{site.data.keyword.logs_full_notm}} is available. You can only migrate instances in supported locations. For more information, see [Locations](/docs/cloud-logs?topic=cloud-logs-regions).

    When you migrate by using Terraform, you can modify the location where an instance is created before applying the Terraform script. You can check the migrated assets and prepare the migration for when other regions are supported.
    {: tip}

2. After you migrate each of the {{site.data.keyword.at_full_notm}} instances in the account, configure {{site.data.keyword.atracker_full_notm}}.

    Run the following command to generate Terraform scripts that you can customize:

    ```text
    ibmcloud logging migrate create-resources --scope atracker --terraform
    ```
    {: pre}

    Run the following command to generate and apply Terraform scripts that you can customize:

    ```text
    ibmcloud logging migrate create-resources --scope atracker --terraform -f
    ```
    {: pre}

    Run the following command to configure {{site.data.keyword.atracker_full_notm}} automatically after you create the route to send events to {{site.data.keyword.at_full_notm}} instances:

    ```text
    ibmcloud logging migrate create-resources --scope atracker --api
    ```
    {: pre}

    - The migration tool adds a `cloud-logs` target in {{site.data.keyword.atracker_full_notm}} for each {{site.data.keyword.logs_full_notm}} instance that is created as the result of migrating an {{site.data.keyword.at_full_notm}} instance, and has a target configured that is used in a routing rule.

        There is a limit of targets per account. You can define up to 16 targets in total in an account. Make sure that you have enough targets available so that the migration tool can create 1 target per {{site.data.keyword.at_full_notm}} migrated instance in the account. If you do not have enough targets, the migration process cannot be completed. Delete any unused targets and try again.
        {: requirement}

    - The migration tool adds a new route with rules that route events based on the current routing rules to {{site.data.keyword.at_full_notm}} instances.

5. Migrate IAM permissions. For more information, see [Migrating IAM permissions](/docs/cloud-logs?topic=cloud-logs-migration-iam).

6. Validate that the new configuration is working for your requirements.

7. After you validate that your migrated configuration is as required, delete {{site.data.keyword.at_full_notm}} instances.

    Before you delete your {{site.data.keyword.at_full_notm}} instances, check that the events that are generated by {{site.data.keyword.cloud_notm}} services that you use are managed through {{site.data.keyword.atracker_full_notm}}. For more information, see [{{site.data.keyword.cloud_notm}} services that generate events that are managed through {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-cloud_services_atracker).
