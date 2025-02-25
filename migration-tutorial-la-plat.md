---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-25"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Migrating 1 instance of Log Analysis with platform log enabled by using the migration tool
{: #migration-tutorial-la-plat}

Use this topic to migrate 1 {{site.data.keyword.la_full_notm}} instance with platform log enabled by using the migration tool.
{: shortdesc}


Migrating {{site.data.keyword.la_full_notm}} instances to {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}} requires:
- Migration of the {{site.data.keyword.la_full_notm}} instance
- Configuration of the logging agent to send data to the Cloud Logs instance
- Configuration of IBM Cloud Logs Routing to define to which Cloud Logs instance platform logs generated in a region are routed


When you configure the IBM Cloud Logs Routing service, you are controlling where platform logs are routed in the account. For migration, it is very important that you first configure IBM Cloud Logs Routing and define a `Log Analysis` target to configure the current default behavior in the account. Afterwards, you can define a `Cloud Logs` target to send the same data to the migrated {{site.data.keyword.logs_full_notm}} instance. If you do not define a Log Analysis target first, platform logs will stop being routed to your current {{site.data.keyword.la_full}} instance.
{: important}

Always run the migration tool in a development or staging environment to test and validate the migration command and steps.
{: important}


{{/_include-segments/data-not-migrated.md}}


The following list outlines the services that you need access to migrate an {{site.data.keyword.la_full_notm}} instance:

- Cloud Object Storage (to store data and metrics)

- Event Notifications (to trigger alerts through Email, PagerDuty, Slack, webhook)

- {{site.data.keyword.logs_full_notm}} (the new logging service in IBM Cloud Observability)

- Event Streams for managing streaming of data through a topic

- IBM Cloud Logs Routing

The migration tool helps you migrate the following configuration:
- 1 Log Analysis instance and resources such as views, alerts, data usage, dashboards (limited), log groups (limited), exclusion rules (limited). Limited means that to complete you must take manual action as the technologies are very different.
- Archiving configuration, if the Log Analysis instance has archiving enabled. The migration tool also creates the IAM authorizations between the Cloud Logs instance and the Cloud Object Storage buckets.
- Alerting configuration, including the configuration required in Event Notification to trigger alerts to your notification channels (destinations).
- IAM policies to grant permissions to work with the Cloud Logs instance based on the access report of the Log Analysis instance.
- Creates the IBM Cloud Logs Routing configuration to keep data going to your deprecated instance and to the migrated instance.

## Prereqs
{: #migration-tutorial-la-plat-prereqs}

Complete these steps before you begin:

1. Make sure you use an ID that has permissions for migrating your instance.

    See [Required permissions for running the migration tool](/docs/cloud-logs?topic=cloud-logs-migration-permissions).

    If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned.
    {: important}

    - [ ] IAM permissions to view Log Analysis instances and resources

    - [ ] IAM permissions to read the DEK key name that is associated to a bucket if you have archiving configured on a bucket that has Key Protect enabled.

    - [ ] IAM permissions to manage the Logs Routing service

    - [ ] IAM permissions to create authorizations between services in the account

        - [ ] Logs Routing and Cloud Logs

        - [ ] Cloud Logs and Cloud Object Storage

        - [ ] Cloud Logs and IBM Cloud Event Notifications

        - [ ] Cloud Logs and IBM Cloud Event Streams

    - [ ] IAM permissions to create buckets

    - [ ] IAM permissions to configure sources, destinations, topics and subscriptions in IBM Cloud Event Notifications

2. Generate an API key to use when you apply your Terraform scripts to create resources. You must have these [permissions](/docs/cloud-logs?topic=cloud-logs-migration-permissions).

3. Install the Terraform CLI. Complete the steps in [Geting started with Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started).

4. To send alerts to your destinations, you must provision an instance of the Event Notifications service in the account.

### Configuring permissions using the UI
{: #at2-perm-cli}


{{/_include-segments/atla-permissions.md}}

## Migrating
{: #migration-tutorial-la-plat-migrate}


{{/_include-segments/clean-directory.md}}


{{/_include-segments/find-ecrn.md}}


{{/_include-segments/verify-queries.md}}

Complete the following steps:

1. Create a directory from where you plan to run the migration tool. Then, go to that directory and set the API key to create resources for migration.

    Run `export IC_API_KEY=xxxxxx` in the command line where you plan to run the Terraform CLI commands.

    If running in Windows, use `set IC_API_KEY=xxxxxx` instead.
    {: note}

2. Run the migration tool to generate and apply the terraform files. Take time to review the files and customize them before applying them if you need to make changes.

    ```sh
    ibmcloud logging migrate create-resources --scope instance --instance-crn CRN_VALUE --ecrn EVENT_NOTIFICATIONS_INSTANCE_CRN --platform --ingestion-key INGESTION_KEY [--instance-name INSTANCENAME] [--instance-resource-group-id RESOURCEGROUPID] [--cos-instance-crn cos-instance-crn] [--cos-kms-key-crn cos-kms-key-crn] [--data-bucket-name data-bucket-name] [--metrics-bucket-name metrics-bucket-name] [--ingress-endpoint-type ingress-endpoint-type] -t [-f]
    ```
    {: codeblock}

    You can configure the integration with the Event Notifications service with the option `--ecrn EVENT_NOTIFICATIONS_INSTANCE_CRN`.

    You can change the name of the instance that is created in Cloud Logs by adding the option `--instance-name INSTANCENAME`.

    You can change the resource group ID associated with the instance that is created in Cloud Logs by adding the option `--instance-resource-group-id RESOURCEGROUPID`.

    You can change the default values for the Cloud Object Storage resources by adding the options `[--cos-instance-crn cos-instance-crn] [--cos-kms-key-crn cos-kms-key-crn] [--data-bucket-name data-bucket-name] [--metrics-bucket-name metrics-bucket-name]`.

    You can configure `--ingress-endpoint-type`  to define the ingress endpoint type to use to send platform logs to the Cloud Logs instance. Valid values are `private` and `public`. If not specified the default is `public`.

    The `-f` option will run the migration tool without any additional prompts. Run the migration tool with the option `-f` to apply the Terraform files when you run the command. If you just want to generate Terraform files so you can review and modify them, do not include this option. Once reviewed or modified you can apply the Terraform files by running `terraform apply` from the directory containing the Terraform files.

3. Use the following checklist to verify that the following assets are created in your account when you migrate the instance:

    The migration tool only migrates the configuration of selected resources.
    {: important}

    - Cloud Logs instance, including resources such as views, dashboards, screens, alerts and exclusion rules. The type of resources varies depending on your {{site.data.keyword.la_full_notm}} instance resources.

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

    - [ ] IBM Cloud Logs Routing is configured to continue receiving platform logs in the Log Analysis instance and in the new Cloud Logs instance.

        - [ ]  Target with the details of the Log Analysis instance.

        - [ ]  Target with the details of the Cloud Logs instance

4. Manually migrate parsing and exclusion rules.

    If you have parsing rules and exclusion rules configured in the Log Analysis instance, you must manually recreate them in Cloud Logs.

    In Cloud Logs, you must use Regex to parse the data. For more information, see [Extracting specific values as JSON keys](/docs/cloud-logs?topic=cloud-logs-parse-extract-rule).

5. Deploy and configure the Logging agent to collect and route logs to the Cloud Logs instance.

    You can use a service ID or a trusted profile as the identity that is used by the agent to authenticate with the IBM Cloud Logs service. Choose a supported authorization method for the environment where you plan to deploy the agent: For more information, see [Authorization methods](/docs/cloud-logs?topic=cloud-logs-agent-about#agent-auth-methods).
    {: important}


    - [ ] [Deploy the agent for Kubernetes clusters](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy)

    - [ ] [Deploy the agent for OpenShift clusters](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy)

    - [ ] [Deploy the agent for Linux servers](/docs/cloud-logs?topic=cloud-logs-agent-linux)

    - [ ] [Deploy the agent for Windows servers](/docs/cloud-logs?topic=cloud-logs-agent-windows)

    - [ ] [Deploy the agent to collect and route rSyslog data](/docs/cloud-logs?topic=cloud-logs-agent-rsyslog)

6. Verify your views and alert configurations in Cloud Logs.

    In Log Analysis, a view and an alert are tightly coupled. You define the triggering condition (query) in the view and configure an alert to indicate when and to how many notification channels to send the event.

    In Cloud Logs, Views (known as Logs) and Alerts are resources that you manage separately. The migration tool creates a view and an alert as independent resources. The query is the same in both cases. Also adds an integration to the Event Notifications service so when is trigger, an event is sent to your destinations.

    When you verify the query of a view, if you make any changes to a view configuration such as changing the `applicationName` or the `subsystemName`, you must make the same changes to the alerts resource.

    You can check that alerts trigger in the Incidents page in your Cloud Logs instance. For more information, see [Managing triggered alerts in IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-incidents).



7. Apply the Event Notification terraform files located in `migration-tool/cl/accountID/manual-tf-files/event-notifications-tf-files/logAnalysisInstanceID/`and verify that alerts are triggered.

    The migration tool generates the event notification resources files but does not apply them. After you verify your views and alerts, apply them to validate that platform logs are generated and you are getting notifications in your destinations.

    The migration tool does not generate templates. You can manually configure templates for your resources. For more information, see [Creating an Event Notifications template](/docs/event-notifications?topic=event-notifications-en-create-en-template).

    The following Event Notification resources are required:

    - [ ] 1 Source that defines the integration between the Cloud Logs instance and the Event Notifications instance

    - [ ] Destination channels: You must have 1 destination per notification channel such as Slack, PagerDuty, WebHook

    - [ ] Topics: A topic is created for the alerts that send notifications through the same destination.

    - [ ] Subscriptions to correlate topics and destinations.

    Checklist of tasks:

    - [ ] Apply the Event notifications terraform files located in `migration-tool/cl/accountID/manual-tf-files/event-notifications-tf-files/logAnalysisInstanceID/`

    - [ ] Verify that alerts are triggered.

8. If you have log groups configured in your Log Analysis instance, manually map the data access rule query to a Data Expression (DPXL).

    If you have log groups configured, the migration tool creates a data access rule for each log group and copies the Log Analysis log group queries. You must manually migrate these queries to data access rules by using the Data Expression language. For more information, see [Create a rule in the IBM Cloud Logs service](/docs/cloud-logs?topic=cloud-logs-data-access-rules#data-access-rules-1).

9. Apply the IAM terraform files located in `migration-tool/cl/accountID/manual-tf-files/iam-policies/logAnalysisInstanceID/`and verify that permissions have been applied.

    - [ ] Verify the `migration-tool/cl/accountID/manual-tf-files/iam-policies/logAnalysisInstanceID/roles.tf` policies file

    - [ ] Apply the IAM terraform files located in `migration-tool/cl/accountID/manual-tf-files/iam-policies/logAnalysisInstanceID/`

    - [ ] Verify that permissions have been applied and your users and IDs have the correct access.

    The IAM policies that are defined in the `roles.tf` file are configured for the Cloud Logs instance ID. Why? Activity Tracker and Log Analysis are 2 different services that you must migrate. In the new architecture, the same service is used to manage the different types of data that Activity Tracker and Log Analysis monitor. Therefore, to avoid granting higher permissions than required when you give policies for both services in an access group or for a user, for example, the policies included are specific to the Cloud Logs Instance ID to which they apply. The roles are identified by running the access report that you can also run manually to verify who has access to your instance.
    {: important}

10. Add other IAM configurations manually

    - [ ] Grant permissions to work with the IBM Cloud Logs Routing service to your admins/editors in the account

    - [ ] For each API key (service ID / user ID) that you have with permissions to work with the Log Analysis instance, you need to recreate them and modify the applications that use it so they include permissions to work with the new services and resources.

    Make sure that before you generate the API keys, the permissions to work with the Cloud Logs instance are set.
    {: important}

11. If you have streaming configured, you must manually migrate the configuration. For more information, see [Streaming data](/docs/cloud-logs?topic=cloud-logs-streaming).

12. After you have completed the migration and verification process, remove your Log Analysis instance and related resources by following the instructions in [Removing deprecated {{site.data.keyword.la_full_notm}} instances with platform logs enabled](/docs/cloud-logs?topic=cloud-logs-migration-remove-plat).
