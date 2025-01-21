---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-21"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Tutorial for migrating 1 Activity Tracker instance in the account end to end
{: #migration-tutorial-at-option2}

Use this tutorial to migrate 1 {{site.data.keyword.at_full}} instance and configure the {{site.data.keyword.atracker_full_notm}} service by running the migration tool.
{: shortdesc}


## Overview
{: #migration-tutorial-at-option2-ov}

Migrating {{site.data.keyword.at_full}} instances to {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}} requires the configuration of the {{site.data.keyword.atracker_full_notm}} service in the account to define where events are routed and the provisioning of {{site.data.keyword.logs_full_notm}} instances. A migration tool is provided to help you migrate.

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



## Prereqs
{: #migration-tutorial-at-option2-prereqs}

Complete these steps before you begin:

1. Make sure you use an ID that has permissions for migrating your instance.

    See [Required permissions for running the Migration tool](/docs/cloud-logs?topic=cloud-logs-migration-permissions).

    If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned.
    {: important}

    - [ ] IAM permissions to view Activity Tracker instances and resources

    - [ ] IAM permissions to read the DEK key name that is associated to a bucket if you have archiving configured on a bucket that has Key Protect enabled.

    - [ ] IAM permissions to manage the Activity Tracker Event Routing service

    - [ ] IAM permissions to create authorizations between services in the account

        - [ ] Activity Tracker Event Routing and Cloud Logs

        - [ ] Cloud Logs and Cloud Object Storage

        - [ ] Cloud Logs and IBM Cloud Event Notifications

        - [ ] Cloud Logs and IBM Cloud Event Streams

    - [ ] IAM permissions to create buckets

    - [ ] IAM permissions to configure sources, destinations, topics and subscriptions in IBM Cloud Event Notifications

2. Generate an API key to use when you apply your Terraform scripts to create resources. Must have these [permissions](/docs/cloud-logs?topic=cloud-logs-migration-permissions).

3. Install the Terraform CLI. Complete the steps in [Geting started with Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started).

4. To send alerts to your destinations, you must provision an instance of the Event Notifications service in the account.


## Migrating
{: #migration-tutorial-at-option2-migrate}

Complete the following steps:

1. Create a directory from where you plan to run the migration tool. Then, go to that directory and set the API key that you must configure to create resources for migration.

    Run `export IC_API_KEY=xxxxxx` in the command line where you plan to run the Terraform CLI commands.

    If running in Windows, use `set IC_API_KEY=xxxxxx` instead.
    {: note}

2. Run the migration tool to generate and apply the terraform files. Take time to review them and customize them before applying them if you need to make changes.

    ```sh
    ibmcloud logging migrate create-resources --scope instance --instance-crn CRN_VALUE --ecrn EVENT_NOTIFICATIONS_INSTANCE_CRN --platform --ingestion-key INGESTION_KEY [--instance-name INSTANCENAME] [--instance-resource-group-id RESOURCEGROUPID] [--cos-instance-crn cos-instance-crn] [--cos-kms-key-crn cos-kms-key-crn] [--data-bucket-name data-bucket-name] [--metrics-bucket-name metrics-bucket-name]  -t [-f]
    ```
    {: codeblock}

    You can configure the integration with the Event Notifications service with the option `--ecrn EVENT_NOTIFICATIONS_INSTANCE_CRN`.

    You can change the name of the instance that is created in Cloud Logs by adding the option `--instance-name INSTANCENAME`.

    You can change the resource group ID associated with the instance that is created in Cloud Logs by adding the option `--instance-resource-group-id RESOURCEGROUPID`.

    You can change the default values for the Cloud Object Storage resources by adding the options [--cos-instance-crn cos-instance-crn] [--cos-kms-key-crn cos-kms-key-crn] [--data-bucket-name data-bucket-name] [--metrics-bucket-name metrics-bucket-name].

    Run the migration tool with the option `-f` to apply the terraform files when you run the command. If you just want to generate terraform files, do not include this option.

3. Use the following checklist to verify that the following assets are created in your account when you migrate the instance:

    The Migration Tool only migrates configuration of selected resources.
    {: important}

    - Cloud Logs instance, including resources such as views, dashboards, screens, alerts and exclusion rules. The type of resources varies depending on your {{site.data.keyword.at_full}} instance resources.

        - [ ] Cloud Logs instance

        - [ ] Resources such as views, dashboards, screens, alerts, exclusion rules, and log groups.

        - [ ] Tags

    - Cloud Object Storage resources:

        - [ ] A data bucket

        - [ ] A metrics bucket

    - [ ] IAM authorizations:

        - [ ] IAM authorization between Cloud Logs and the data bucket.

        - [ ] IAM authorization between Cloud Logs and the metrics bucket.

        - [ ] IAM authorization between Cloud Logs and the Event Notifications service.

    - [ ] Add an external integration in Cloud Logs to the Event Notifications instance.

    - [ ] Activity Tracker Event Routing is configured to continue receiving auditing events in the Activity Tracker instance and the new Cloud Logs instance.

        - [ ]  Target with the details of the Activity Tracker instance.

        - [ ]  Target with the details of the Cloud Logs instance

        - [ ]  Route with a rule to route auditing events of the region being migrated to the Activity Tracker target.

        - [ ]  Route with a rule to route auditing events of the region being migrated to the Cloud Logs target.

4. Verify the Activity Tracker Event Routing configuration.

    - [ ] Check that you continue to see activity tracker events in tail mode in your Activity Tracker instance.

    - [ ] Check that you see activity tracking events in your Cloud Logs instance. Filter by applicationName `ibm-audit-event`.

5. Manually migrate parsing rules.

    If you have parsing rules configured in the Activity Tracker instance, you must manually recreate them in Cloud Logs.

    In Cloud Logs, you must use Regex to parse the data. For more information, see [Extracting specific values as JSON keys](/docs/cloud-logs?topic=cloud-logs-parse-extract-rule).

6. Verify your views and alert configurations in Cloud Logs.

    In Activity Tracker, a view and an alert are tightly coupled. You define the triggering condition (query) in the view and configure an alert to indicate when and to how many notification channels to send the event.

    In Cloud Logs, Views (known as Logs) and Alerts are resources that you manage separately. The migration tool creates a view and an alert as independent resources. The query is the same in both cases. Also adds an integration to the Event Notifications service so when is trigger, an event is sent to your destinations.

    When you verify the query of a view, if you make any changes to a view configuration such as changing the applicationName or the subsystemName, you must make the same changes to the alerts resource.

    You can check that alerts trigger in the Incidents page in your Cloud Logs instance. For more information, see [Managing triggered alerts in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-incidents).

7. Apply the Event Notification terraform files located in `migration-tool/cl/accountID/manual-tf-files/event-notifications-tf-files/activityTrackerInstanceID/`and verify that alerts are triggered.

    The migration tool generates the event notification resources files but does not apply them. After you verify your views and alerts, apply them to validate that events are generated and you are getting notifications in your destinations.

    The migration tool does not generate templates. You can manually configure templates for your resources. For more information, see [Creating an Event Notifications template](/docs/event-notifications?topic=event-notifications-en-create-en-template).

    The following Event Notification resources are required:

    - [ ] 1 Source that defines the integration between the Cloud Logs instance and the Event Notifications instance

    - [ ] Destination channels: You must have 1 destination per notification channel such as Slack, PagerDuty, WebHook

    - [ ] Topics: A topic is created for the alerts that send notifications through the same destination.

    - [ ] Subscriptions to correlate topics and destinations.

    Checklist of tasks:

    - [ ] Apply the Event notifications terraform files located in `migration-tool/cl/accountID/manual-tf-files/event-notifications-tf-files/activityTrackerInstanceID/`

    - [ ] Verify that alerts are triggered.

8. If you have log groups configured in your Activity Tracker instance, manually map the data access rule query to a Data Expression (DPXL).

    If you have log groups configured, the migration tool creates a data access rule for each log group and copies the Activity Tracker log group queries. You must manually migrate these queries to data access rules by using the Data Expression language. For more information, see [Create a rule in the IBM Cloud Logs service](/docs/cloud-logs?topic=cloud-logs-data-access-rules#data-access-rules-1).

9. Apply the IAM terraform files located in `migration-tool/cl/accountID/manual-tf-files/iam-policies/activityTrackerInstanceID/`and verify that permissions have been applied.

    - [ ] Verify the `migration-tool/cl/accountID/manual-tf-files/iam-policies/activityTrackerInstanceID/roles.tf` policies file

    - [ ] Apply the IAM terraform files located in `migration-tool/cl/accountID/manual-tf-files/iam-policies/activityTrackerInstanceID/`

    - [ ] Verify that permissions have been applied and your users and IDs have the correct access.

    The IAM policies that are defined in the roles.tf file are configured for the Cloud Logs instance ID. Why? Activity Tracker and Log Analysis are 2 different services that you must migrate. In the new architecture, the same service is used to manage the different types of data that Activity Tracker and Log Analysis monitor. Therefore, to avoid granting higher permissions than required when you give policies for both services in an access group or for a user, for example, the policies included are specific to the Cloud Logs Instance ID to which they apply. The roles are identified by running the access report that you can also run manually to verify who has access to your instance.
    {: important}

10. Add other IAM configurations manually

    - [ ] Grant permissions to work with the Activity Tracker Event Routing service to your admins/editors in the account

    - [ ] For each API keys (service ID / user ID) that you have with permissions to work with the Activity Tracker instance, you need to recreate them and modify the applications that use it so they include permissions to work with the new services and resources.

    Make sure that before you generate the API keys, the permissions to work with the Cloud Logs instance and Activity Tracker Event Routing are set.
    {: important}

11. If you have streaming configured, you must manually migrate the configuration. For more information, see [Streaming data](/docs/cloud-logs?topic=cloud-logs-streaming).

12. After you have completed the migration and verification process, remove your Activity Tracker instance and related resources.

    - [ ] Clean IAM by removing IAM policies that apply to the Activity Tracker instance.

    - [ ] Delete the Activity Tracker instance.
