---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-30"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring {{site.data.keyword.atracker_full_notm}} in the account for an {{site.data.keyword.logs_full_notm}} instance that was created without using the migration tool
{: #migration-tutorial-at-option3}

Use this topic to configure the {{site.data.keyword.atracker_full_notm}} service to route activity tracking events to a Cloud Logs instance in the account without running the migration tool.
{: shortdesc}

Migrating {{site.data.keyword.at_full}} instances to {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}} requires the configuration of the {{site.data.keyword.atracker_full_notm}} service in the account to define where events are routed and the provisioning of 1 or more {{site.data.keyword.logs_full_notm}} instances. A migration tool is provided to help you migrate. However, you might find that you do not want to migrate and prefer to start fresh in Cloud Logs. If this is your scenario, complete these steps to create 1 Cloud Logs instance in the account where you collect activity tracking events that are generated in the account by configuring the Activity Tracker Event Routing service.


## Prereqs
{: #migration-tutorial-at-option3-prereqs}

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

2. If you plan to use terraform, generate an API key to use when you apply your Terraform scripts to create resources. Must have these [permissions](/docs/cloud-logs?topic=cloud-logs-migration-permissions).

3. If you plan to use terraform, install the Terraform CLI. Complete the steps in [Geting started with Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started).

4. To send alerts to your destinations, you must provision an instance of the Event Notifications service in the account.


## Provision a Cloud Logs instance
{: #migration-tutorial-at-option3-step1}
{: step}

1. [Provision a Cloud Logs instance](/docs/cloud-logs?topic=cloud-logs-instance-provision).
2. Configure two IBM Cloud Object Storage buckets for your IBM Cloud Logs instance. One is used for logs, the other is used for metrics. For mroe information, see [Creating buckets](/docs/cloud-logs?topic=cloud-logs-about-bucket&interface=ui#about-bucket-ov).

    [Review the bucket restrictions](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket#cos_databucket_restrictions).
    {: important}

3. Create a service to service (S2S) authorization between the Cloud Logs instance and the data bucket.
4. Create a service to service (S2S) authorization between the Cloud Logs instance and the metrics bucket.
5. Configure the buckets with your Cloud Logs instance. For more informations, see [Configuring buckets](/docs/cloud-logs?topic=cloud-logs-about-bucket).

## Configure Activity Tracker Event Routing
{: #migration-tutorial-at-option3-step2}
{: step}

Configure Activity Tracker Event Routing to continue receiving auditing events in the Activity Tracker instance and the new Cloud Logs instance. Then verify the Activity Tracker Event Routing configuration.

- [ ] [Create 1 `logdna` target for each Activity Tracker instance in the account](/docs/atracker?topic=atracker-target_v2_at&interface=ui)

- [ ]  [Create the routes with a rule that maps your current Activity Tracker instances location](/docs/atracker?topic=atracker-route_v2&interface=ui#route-create-ui):

    For eu-de: Select `eu-de` and `global` events and as the target destination, choose the target you have configured for the eu-de region.

    For the rest of the supported regions, choose the same region. For example, for `us-south` events, choose the target you have configured for the `us-south` region.

    For Chennai, select `in-che` events, and choose the target you have configured for the `in-che` region.

- [ ] [Define a service to service authorization between Activity Tracker Event Routing and Cloud Logs](/docs/atracker?topic=atracker-iam-service-auth-logs)

- [ ] [Create a `cloud_logs` target with the details of the Cloud Logs instance](/docs/atracker?topic=atracker-target_v2_icl)

- [ ] [Create a route with a wildcard rule to route all auditing events to the Cloud Logs target](/docs/atracker?topic=atracker-route_v2&interface=ui#route-create-ui).

    Choose `wildcard(*)` events and the Cloud Logs target that you have created.

Checklist to verify the Activity Tracker Event Routing configuration.

- [ ] Check that you continue to see activity tracking events in tail mode in your Activity Tracker instances.

- [ ] Check that you see activity tracking events, from all the regions where you have Activity Tracker instances, in your Cloud Logs instance. Filter by applicationName `ibm-audit-event`.

## Configure the Event Notifications service for alerting
{: #migration-tutorial-at-option3-step3}
{: step}

Cloud Logs integrates with the Event Notifications service to send events to your destinations.

In Activity Tracker, a view and an alert are tightly coupled. You define the triggering condition (query) in the view and configure an alert to indicate when and to how many notification channels to send the event.

In Cloud Logs, Views (known as Logs) and Alerts are resources that you manage separately. You create a view and an alert as independent resources. The query is the same in both cases if the view and the alert are related. You can also add an integration to the Event Notifications service when you configure an alert so when the alert triggers in Cloud Logs, an event is sent to your destinations through the Event Notifications service.

1. Provision an instance of Event notifications.

2. [Define a service to service authorization between Cloud Logs and the Event Notifications service](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-step1)

3. [Define an outbound integration in your Cloud Logs instance to integrate both services](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-step2).

3. [Verify you integration](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-next).


## Configure IAM policies
{: #migration-tutorial-at-option3-step4}
{: step}

You must configure IAM policies to grant access to work with the Cloud Logs service. For more information, see [Geting started with IAM](/docs/cloud-logs?topic=cloud-logs-iam).

## Create resources in Cloud Logs
{: #migration-tutorial-at-option3-step5}
{: step}

You might want to configure some views and alerts that you currently have in your Activity Tracker instances.

- To create views, see [Managing custom views](/docs/cloud-logs?topic=cloud-logs-custom_views).
- To create dashboards, see [Managing dashboards](/docs/cloud-logs?topic=cloud-logs-create_dashboards).
- Deploy an extension. Extensions are pre-defined resources that you can easily deploy to start monitoring your data. See [Managing extensions](/docs/cloud-logs?topic=cloud-logs-extensions).

## Remove Activity Tracker instances in the account
{: #migration-tutorial-at-option3-step6}
{: step}

After you have completed the verification process, remove your Activity Tracker instances and related resources.

- [ ] Clean up IAM by removing IAM policies that apply to the Activity Tracker instances.

- [ ] Remove Activity Tracker Event Routing target and route for the legacy Activity Tracker instances.

- [ ] Delete the Activity Tracker instances in the account.
