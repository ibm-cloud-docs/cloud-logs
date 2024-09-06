---

copyright:
  years:  2024
lastupdated: "2024-09-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Template for tasks for migrating Log Analysis instances collecting logs in the account
{: #template-migration-logs}

- [ ] List of services that you might need for migration:

    - [ ] Cloud Object Storage (to store data and metrics)

    - [ ] Event Notifications (to trigger alerts thorugh Email, PD, Slack, webhook)

    - [ ] IBM Cloud Logs (the new logging service in IBM Cloud Observability)

- [ ] IAM permissions to migrate

    - [ ] IAM permissions to view Log Analysis instances and resources

    - [ ] IAM permissions to read the DEK key name that is associated to a bucket if you have archiving configured on a bucket that has Key Protect enabled.

    - [ ] IAM permissions to manage the Logs Routing service

    - [ ] IAM permissions to create authorizations between services in the account

        - [ ] Logs Routing and Cloud Logs

        - [ ] Cloud Logs and Cloud Object Storage

        - [ ] Cloud Logs and IBM Cloud Event Notifications

    - [ ] IAM permissions to create buckets

    - [ ]  IAM permissions to configure alert destinations in IBM Cloud Event Notifications

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

- [ ] Deploy/ Configure the Logging agent to collect and route logs to the Cloud Logs instance.

    - [ ] Deploy agent for Kubernetes clusters

    - [ ] Deploy agent for OpenShift clusters

    - [ ] Deploy agent for Linux servers

    - [ ] Deploy agent to collect and route rSyslog data

- [ ] Generate the IAM report to identify the access groups, service IDs, users, and trusted profiles that have permissions configured on the instance that you are migrating.

- [ ] If you have parsing rules configured in the Log Analysis instance, you must manually recreate them in Cloud Logs. (In Cloud Logs, you must use Regex to parse the data.)

- [ ] Modify any runbooks for DevOps
