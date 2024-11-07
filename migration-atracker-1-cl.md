---

copyright:
  years:  2024
lastupdated: "2024-11-07"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating {{site.data.keyword.at_full_notm}} instances into a single {{site.data.keyword.logs_full_notm}} instance for centralize auditing events
{: #migration-atracker-1-cl}

You can use the migration tool to help you migrate {{site.data.keyword.at_full_notm}} instances into a single {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

The following image shows a high-level view of the account after {{site.data.keyword.at_full_notm}} instances from multiple regions in the account are migrated into 1 instance of {{site.data.keyword.logs_full_notm}}.

![High-level view of the account after {{site.data.keyword.at_full_notm}} instances from multiple regions in the account are migrated into 1 instance of {{site.data.keyword.logs_full_notm}}](/images/migration-atracker-central.svg "Account overview of activity tracking event hanlding."){: caption="High-level view of the account after {{site.data.keyword.at_full_notm}} instances from multiple regions in the account are migrated into 1 instance of {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}

## Scenario
{: #migration-atracker-1-cl-scenario}

- {{site.data.keyword.atracker_full_notm}} is not configured in the account.
- You have {{site.data.keyword.at_full_notm}} instances provisioned in multiple locations.
- You must migrate your {{site.data.keyword.at_full_notm}} instances into 1 {{site.data.keyword.logs_full_notm}} instance.
- You have a requirement to centralize activity tracking events that are generated in the account.

## Before you begin
{: #migration-atracker-1-cl-prereqs}

- Learn about migration. For more information, see [Migrating {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-migration-intro).

- Learn about the migration tool. For more information, see [Migrating tool](/docs/cloud-logs?topic=cloud-logs-migration-tool).

- Check the locations where {{site.data.keyword.logs_full_notm}} is available. You can only provision {{site.data.keyword.logs_full_notm}} instances in supported locations. For more information, see [Locations](/docs/cloud-logs?topic=cloud-logs-regions).

## Migration steps
{: #migration-atracker-1-cl-steps}

Complete the following steps to migrate {{site.data.keyword.at_full_notm}} instances in the account:

1. Run the migration tool to collect information about what instances need to be migrated and their resources.

    ```text
    ibmcloud logging migrate generate-terraform --scope account --service logdnaat
    ```
    {: pre}

    When you run this command, you get information in the `tmp` directory about the resources that you currently have configured. You also get terraform scripts to recreate these resources in {{site.data.keyword.logs_full_notm}} in the `cl` directory.

2. Manually configure a route in {{site.data.keyword.atracker_full_notm}} that routes events to your current {{site.data.keyword.at_full_notm}} instances.

    Before you configure {{site.data.keyword.atracker_full_notm}} to route activity tracking events to your {{site.data.keyword.logs_full_notm}} instance, you must configure targets for each {{site.data.keyword.at_full_notm}} instance and a route with rules to route events that are generated in each region to be routed to the {{site.data.keyword.at_full_notm}} instance that is available in the same region where the events are generated. Until you have validated the new architecture, you must continue managing the account through the deprecated services. If you fail to configure this route, activity tracking events will stop being routed to your current {{site.data.keyword.at_full_notm}} instances. {: important}

    Define rules in the route as follows:

    - For `eu-de`, the rule routes events generated in the `eu-de` region and `global` events to the {{site.data.keyword.logs_full_notm}} instance created in the `eu-de` region.

    - For other [supported regions](/docs/atracker?topic=atracker-regions), the rule routes events from that region only to the {{site.data.keyword.logs_full_notm}} instance created in that region. For example, for `eu-es`, the rule routes events generated in the `eu-es` region to the {{site.data.keyword.logs_full_notm}} instance created in the `eu-es` region.

    The migration tool cannot automatically create this route since it requires an ingestion key that you must get and configure. For more information on how to configure the targets and routes, see [Getting started with {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-getting-started).
    {: important}

3. Run the migration tool to create the {{site.data.keyword.logs_full_notm}} instance, data bucket, metrics bucket, and configure {{site.data.keyword.atracker_full_notm}} in the account.

    Run the following command to generate Terraform scripts:

    ```text
    ibmcloud logging migrate create-resources --scope atracker --terraform --single --instance-name INSTANCE_NAME --data-bucket-name DATA_BUCKET_NAME --metrics-bucket-name METRICS_BUCKET_NAME --region REGION --instance-resource-group-id RESOURCE_GROUP_ID --cos-instance-crn COS_INSTANCE_CRN [--cos-kms-key-crn KEY_CRN]
    ```
    {: pre}

    Run the following command to generate Terraform scripts:

    ```text
    ibmcloud logging migrate create-resources --scope atracker --terraform --single --instance-name INSTANCE_NAME --data-bucket-name DATA_BUCKET_NAME --metrics-bucket-name METRICS_BUCKET_NAME --region REGION --instance-resource-group-id RESOURCE_GROUP_ID --cos-instance-crn COS_INSTANCE_CRN [--cos-kms-key-crn KEY_CRN] -f
    ```
    {: pre}

    Run the following command to automatically create the instance by using the API:

    ```text
    ibmcloud logging migrate create-resources --scope atracker --api --single --instance-name INSTANCE_NAME --data-bucket-name DATA_BUCKET_NAME --metrics-bucket-name METRICS_BUCKET_NAME --instance-region REGION --instance-resource-group-id RESOURCE_GROUP_ID --cos-instance-crn COS_INSTANCE_CRN [--cos-kms-key-crn KEY_CRN]
    ```
    {: pre}

    - The migration tool creates the {{site.data.keyword.logs_full_notm}} instance and buckets for data and metrics.

    - The migration tool creates the service to service authorizations between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.atracker_full_notm}}, and {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}}.

    - The migration tool creates an {{site.data.keyword.atracker_full_notm}} target with information about the {{site.data.keyword.logs_full_notm}} instance using the endpoint that is specified by the `region` parameter.

    - The migration tool adds a new route with a wildcard rule to route all events, including global ones, to the {{site.data.keyword.logs_full_notm}} instance.

4. If you have alerts configured in your {{site.data.keyword.at_full_notm}} instances, you must define an outbound integration to the {{site.data.keyword.en_full_notm}} service in your {{site.data.keyword.logs_full_notm}} instance. In addition, you might need to provision an instance of the {{site.data.keyword.en_full_notm}} service, and do some manual tasks to enable notification channels that might, for example, require credentials.

    In {{site.data.keyword.logs_full_notm}}, alerts are triggered through the {{site.data.keyword.en_full_notm}} service. If you do not currently use the {{site.data.keyword.en_full_notm}} service, and have alerts configured in your {{site.data.keyword.at_full_notm}} instances, you must provision an instance of the {{site.data.keyword.en_full_notm}} service for alerting. For more information, see [Enabling event notifications for {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-event-notifications-events).
    {: note}

    You must manually configure notification channels such as email and PagerDuty. For example, every user that is configured to receive a mail notification when an alert is triggered receives an email that requires them to accept before they get email notifications that might be generated by the alert.

    Sysdig alerts are not migrated. You can use the *Incidents* page to see which alerts have been triggered. You can use the {{site.data.keyword.en_full_notm}} service to configure other notification channels.

    You must manually configure the Slack URL and the webhook header apikey when you configure Slack notification channels or webhooks to other applications.

    The migration tool provides Terraform scripts that you can customize to configure the {{site.data.keyword.en_full_notm}} service.

5. Migrate IAM permissions. For more information, see [Migrating IAM permissions](/docs/cloud-logs?topic=cloud-logs-migration-iam).

6. Validate that the new configuration is working for your requirements.

7. After you validate that your migrated configuration is as required, delete your {{site.data.keyword.at_full_notm}} instances.

    Before you delete your {{site.data.keyword.at_full_notm}} instances, check that the events that are generated by {{site.data.keyword.cloud_notm}} services that you use are managed through {{site.data.keyword.atracker_full_notm}}. For more information, see [{{site.data.keyword.cloud_notm}} services that generate events that are managed through {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-cloud_services_atracker).
