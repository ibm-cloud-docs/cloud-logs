---

copyright:
  years:  2024
lastupdated: "2024-10-09"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Migrating {{site.data.keyword.at_full_notm}} instances into N {{site.data.keyword.logs_full_notm}} instances for data locality
{: #migration-atracker-n-cl}

You can use the Migration tool to migrate {{site.data.keyword.at_full_notm}} instances into N {{site.data.keyword.logs_full_notm}} instances, replicating the current {{site.data.keyword.at_full_notm}} architecture. Then, after you have migrated all instances, you can use the Migration tool to configure {{site.data.keyword.atracker_full_notm}} in the account.
{: shortdesc}

The following image shows a high-level view of the account after {{site.data.keyword.at_full_notm}} instances from multiple regions in the account are migrated into multiple instances of {{site.data.keyword.logs_full_notm}}:

![High-level view of the account after {{site.data.keyword.at_full_notm}} instances from multiple regions in the account are migrated into multiple instances of {{site.data.keyword.logs_full_notm}}](/images/migration-atracker-many.svg "Account overview of handling activity tracking events."){: caption="High-level view of the account after {{site.data.keyword.at_full_notm}} instances from multiple regions in the account are migrated into multiple instances of {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}

## Scenario
{: #migration-atracker-n-cl-scenario}

- {{site.data.keyword.atracker_full_notm}} is not configured in the account.
- You have {{site.data.keyword.at_full_notm}} instances provisioned in multiple locations.
- You must migrate your {{site.data.keyword.at_full_notm}} instances to {{site.data.keyword.logs_full_notm}} instances.
- You have a requirement to maintain data locality in the account.

## Before you begin
{: #migration-atracker-n-cl-prereqs}

- Learn about migration. For more information, see [Migrating {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-migration-intro).

- Learn about the migration tool. For more information, see [Migrating tool](/docs/cloud-logs?topic=cloud-logs-migration-tool).

- Check the locations where {{site.data.keyword.logs_full_notm}} is available. You can only provision {{site.data.keyword.logs_full_notm}} instances in supported locations. For more information, see [Locations](/docs/cloud-logs?topic=cloud-logs-regions).

## Migration steps
{: #migration-atracker-n-cl-steps}

Complete the following steps to migrate {{site.data.keyword.at_full_notm}} instances in the account:

1. Run the migration tool to collect information about what instances need to be migrated and their resources.

    ```text
    ibmcloud logging migrate generate-terraform --scope account --service logdnaat
    ```
    {: pre}

    When you run this command, you get information in the `tmp` directory about the resources that you currently have configured. You also get terraform scripts to recreate these resources in {{site.data.keyword.logs_full_notm}} in the `cl` directory.

2. Migrate each {{site.data.keyword.at_full_notm}} instance by running one of these commands:

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

    When you migrate by using Terraform, you can modify the location where an instance is created before applying the terraform script so you can check the migrated assets and get it ready for when the region is supported.{: note}

3. Manually configure notification channels such as email and PagerDuty.

    If you use the terraform option, variables are provided for you to enter information on the slack URL and the webhook header apikey.

    {{site.data.keyword.logs_full_notm}} alerting is done by using the {{site.data.keyword.en_full_notm}} service.
    {: note}

4. After you migrate each of the {{site.data.keyword.at_full_notm}} instances in the account, manually configure a route in {{site.data.keyword.atracker_full_notm}} that routes events to your current {{site.data.keyword.at_full_notm}} instances.

    Before you configure {{site.data.keyword.atracker_full_notm}} to route activity Tracking events to your {{site.data.keyword.logs_full_notm}} instance, you MUST configure targets for each {{site.data.keyword.at_full_notm}} and a route with rules to route events that are generated in each region to be routed to the {{site.data.keyword.at_full_notm}} instance that is available in the same region where the events are generated. Why? Until you have validated the new architecture, you must continue managing the account through the deprecated services. If you fail to configure this route, activity tracking events will stop being routed to your current {{site.data.keyword.at_full_notm}} instances. {: important}

    You must define rules in the route as follows:

    - For `eu-de`, the rule routes events generated in the `eu-de` region and `global` events to the {{site.data.keyword.logs_full_notm}} instance created in the `eu-de` region.

    - For other [supported regions](/docs/atracker?topic=atracker-regions), the rule routes events from that region only to the {{site.data.keyword.logs_full_notm}} instance created in that region. For example, for `us-south`, the rule routes events generated in the `us-south` region to the {{site.data.keyword.logs_full_notm}} instance created in the `us-south` region.

    The Migration tool cannot automatically create this route as it requires an ingestion key that you must get and configure. For more information on how to configure the targets and routes, see [Getting started with {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-getting-started). {: important}

5. After you migrate each of the {{site.data.keyword.at_full_notm}} instances in the account, configure {{site.data.keyword.atracker_full_notm}}.

    Run the following command to generate Terraform scripts that you can customize:

    ```text
    ibmcloud logging migrate create-resources --scope atracker --terraform
    ```
    {: pre}

    Run the following command to generate and apply Terraform scripts:

    ```text
    ibmcloud logging migrate create-resources --scope atracker --terraform -f
    ```
    {: pre}

    Run the following command to configure {{site.data.keyword.atracker_full_notm}} automatically after you create the route to send events to {{site.data.keyword.at_full_notm}} instances:

    ```text
    ibmcloud logging migrate create-resources --scope atracker --api
    ```
    {: pre}

    - The migration tool adds a `cloud-logs` target in {{site.data.keyword.atracker_full_notm}} for each {{site.data.keyword.logs_full_notm}} instance that is created as the result of migrating an {{site.data.keyword.at_full_notm}} instance.

        There is a limit of targets per account. You can define up to 16 targets in total in an account. Make sure that you have enough targets unconfigured so that the migration tool can create 1 target per {{site.data.keyword.at_full_notm}} migrated instance in the account. If you do not have enough targets, the migration process cannot be completed. Delete any unused targets and try again.

    - The migration tool adds a new route with rules to route events to the {{site.data.keyword.logs_full_notm}} instance that is available in the region where the events are generated. The rules defined in the route are as follows:

        - For `eu-de`, the rule routes events generated in the `eu-de` region and `global` events to the {{site.data.keyword.logs_full_notm}} instance created in the `eu-de` region.

        - For other [supported regions](/docs/atracker?topic=atracker-regions), the rule routes events from that region only to the {{site.data.keyword.logs_full_notm}} instance created in that region. For example, for `us-south`, the rule routes events generated in the `us-south` region to the {{site.data.keyword.logs_full_notm}} instance created in the `us-south` region.

6. Migrate IAM permissions. For more information, see [Migrating IAM permissions](/docs/cloud-logs?topic=cloud-logs-migration-iam).

7. Validate that the new configuration is working for your requirements.

8. After you validate that your migrated configuration is as required, delete {{site.data.keyword.at_full_notm}} instances.

    Before you delete your {{site.data.keyword.at_full_notm}} instances, check that the events that are generated by {{site.data.keyword.cloud_notm}} services that you use are managed through {{site.data.keyword.atracker_full_notm}}. For more information, see [{{site.data.keyword.cloud_notm}} services that generate events that are managed through {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-cloud_services_atracker).
