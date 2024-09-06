---

copyright:
  years:  2024
lastupdated: "2024-09-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Template for tasks for migrating Log Analysis instances with platform logs flag enabled in the account
{: #template-migration-la}

Template to plan migration from {{site.data.keyword.la_full}} instances with the platform flag enabled to {{site.data.keyword.logs_full_notm}} instances.
{: shortdesc}

## List of services that you might need for migration
{: #template-migration-la-1}

- [ ] List of services that you might need for migration:

    - [ ] Cloud Object Storage (to store data and metrics)

    - [ ] Event Notifications (to trigger alerts thorugh Email, PD, Slack, webhook)

    - [ ] IBM Cloud Logs (the new logging service in IBM Cloud Observability)

## List of permissions that you might need for migration
{: #template-migration-la-2}

The following list outlines the IAM permissions that you need to migrate:

For more information on permissions, see [Required permissions](/docs/cloud-logs?topic=cloud-logs-migration-permissions).

- [ ] IAM permissions to view Log Analysis instances and resources

- [ ] IAM permissions to read the DEK key name that is associated to a bucket if you have archiving configured on a bucket that has Key Protect enabled.

- [ ] IAM permissions to manage the Logs Routing service

- [ ] IAM permissions to create authorizations between services in the account

    - [ ] Logs Routing and Cloud Logs

    - [ ] Cloud Logs and Cloud Object Storage

     - [ ] Cloud Logs and IBM Cloud Event Notifications

- [ ] IAM permissions to create buckets

- [ ]  IAM permissions to configure alert destinations in IBM Cloud Event Notifications

## Migration planning
{: #template-migration-la-3}

- [ ] Identify the regions where you have provisioned Log Analysis instances to collect platform logs.

For each instance,

- [ ] Run the migration tool (ibmcloud logging migrate create-resources --scope instance --instance-crn xxx --platform --ingestion-key xxxxx)

    This command will:

    - [ ] Migrate the instance, its resources such as views, dashboards, screens, alerts.

    - [ ] Check if archiving is enabled and migrate the archiving configuration. If it is, as part of the migration, 2 buckets are created to collect data and metrics.

    - [ ] Add IAM authroizations

        - [ ] Add an IAM authorization between Cloud Logs and the data bucket.

        - [ ] Add an IAM authorization between Cloud Logs and the metrics bucket.

        - [ ] Add an IAM authorization between Cloud Logs and the Event Notifications service.

        - [ ]  Add an external integration in Cloud Logs to the Event Notifications instance.

    - [ ] Migrate notification channels by creating the resources (topics, destinations, and subscriptions) to trigger alerts trough this channels in the IBM CLoud Events Notifications service.

    - [ ] Configure Logs Routing (to continue receiving platform logs in the Log Analysis instance and the new Cloud Logs instance.)

        - [ ]  Create a tenant in the region with 2 target destinations.

        - [ ]  Target 1 includes the details to route platform logs to the Cloud Logs instance

        - [ ]  Target 2 includes the details to route platform logs to the Log Analysis instance

- [ ] Generate the IAM report to identify the access groups, service IDs, users, and trusted profiles that have permissions configured on the instance that you are migrating.

- [ ] If you have parsing rules configured in the Log Analysis instance, you must manually recreate them in Cloud Logs. (In Cloud Logs, you must use Regex to parse the data.)

- [ ] Modify any runbooks for DevOps
