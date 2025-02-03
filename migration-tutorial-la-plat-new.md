---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring {{site.data.keyword.logs_routing_full_notm}} in the account for an {{site.data.keyword.logs_full_notm}} instance that was created without using the migration tool
{: #migration-tutorial-la-plat-new}

Use this topic to configure the {{site.data.keyword.logs_routing_full}} service to route logs to an {{site.data.keyword.logs_full_notm}} instance in the account without running the migration tool.
{: shortdesc}

Migrating {{site.data.keyword.la_full_notm}} instances to {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}} requires:
- Migration of the {{site.data.keyword.la_full_notm}} instance or the creation of a new {{site.data.keyword.logs_full_notm}} instance.

   Use this topic when you created a new {{site.data.keyword.logs_full_notm}} instance. See [Migrating 1 instance of Log Analysis with platform log enabled by using the migration tool](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-la-plat) for steps to migrate an existing {{site.data.keyword.la_full_notm}} instance with platform logs enabled and configure sending platform logs to the migrated instance.
   {: tip}

- Configuration of the logging agent to send data to the Cloud Logs instance.
- Configuration of IBM Cloud Logs Routing to define to which Cloud Logs instance platform logs generated in a region are routed.

## Considerations
{: #migration-tutorial-la-plat-new-considerations}

Depending on your organization's needs, you can configure your routing in different ways:

* You can route platform logs generated in a region to an {{site.data.keyword.logs_full_notm}} instance in the same region. This will be the same behavior you are used to when using {{site.data.keyword.la_full_notm}}.

* You can route platform logs generated in a region to an {{site.data.keyword.logs_full_notm}} instance in a different region. You can use this method to consolidate platform logs in a single {{site.data.keyword.logs_full_notm}} instance.

You need to complete these steps for each region where you are generating platform logs. You only need to create {{site.data.keyword.logs_full_notm}} instances where you need them.

## Prereqs
{: #migration-tutorial-la-plat-new-prereqs}

Complete these steps before you begin:

1. Make sure you use an ID that has required permisions.

   If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned.
   {: important}

    - [ ] IAM permissions to view {{site.data.keyword.la_full_notm}} instances and resources

    - [ ] IAM permissions to manage the {{site.data.keyword.logs_routing_full_notm}} service

    - [ ] IAM permissions to create authorizations between services in the account

        - [ ] {{site.data.keyword.logs_routing_full_notm}} and {{site.data.keyword.logs_full_notm}}

        - [ ] {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}}

        - [ ] {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.en_full_notm}}

        - [ ] {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.messagehub_full_notm}}

    - [ ] IAM permissions to create buckets

    - [ ] IAM permissions to configure sources, destinations, topics and subscriptions in {{site.data.keyword.en_full_notm}}

2. To send alerts to your destinations, you must provision an instance of the {{site.data.keyword.en_full_notm}} service in the account.

## Set the {{site.data.keyword.logs_routing_full_notm}} target to your existing {{site.data.keyword.la_full_notm}} instance
{: #migration-tutorial-la-plat-new-step1}
{: step}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click the **Menu** icon ![Navigation Menu icon](/icons/icon_hamburger.svg "Menu") &gt; **Observability** &gt; **Logging** &gt; **Routing** &gt; **Log Analysis targets**. 

3. Set the target for each location so that the existing logs will continue to be sent to your current {{site.data.keyword.la_full_notm}} instance.

## Provision a {{site.data.keyword.logs_full_notm}} instance
{: #migration-tutorial-la-plat-new-step2}
{: step}

1. [Provision a {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-provision).
2. Configure two IBM Cloud Object Storage buckets for your IBM Cloud Logs instance. One is used for logs, the other is used for metrics. For mroe information, see [Creating buckets](/docs/cloud-logs?topic=cloud-logs-about-bucket&interface=ui#about-bucket-ov).

    [Review the bucket restrictions](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket#cos_databucket_restrictions).
    {: important}

3. Create a service to service (S2S) authorization between the Cloud Logs instance and the data bucket.
4. Create a service to service (S2S) authorization between the Cloud Logs instance and the metrics bucket.
5. Configure the buckets with your Cloud Logs instance. For more informations, see [Configuring buckets](/docs/cloud-logs?topic=cloud-logs-about-bucket).


## Configure the Event Notifications service for alerting
{: #migration-tutorial-la-plat-new-step3}
{: step}

Cloud Logs integrates with the {{site.data.keyword.en_full_notm}} service to send events to your destinations.

In {{site.data.keyword.la_full_notm}}, a view and an alert are tightly coupled. You define the triggering condition (query) in the view and configure an alert to indicate when and to how many notification channels to send the event.

In {{site.data.keyword.logs_full_notm}}, Views (known as Logs) and Alerts are resources that you manage separately. You create a view and an alert as independent resources. The query is the same in both cases if the view and the alert are related. You can also add an integration to the {{site.data.keyword.en_full_notm}} service when you configure an alert so when the alert triggers in {{site.data.keyword.logs_full_notm}}, an event is sent to your destinations through the {{site.data.keyword.en_full_notm}} service.

1. Provision an instance of {{site.data.keyword.en_full_notm}}.

2. [Define a service to service authorization between Cloud Logs and the Event Notifications service](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-step1)

3. [Define an outbound integration in your Cloud Logs instance to integrate both services](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-step2).

3. [Verify you integration](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-next).

## Set the {{site.data.keyword.logs_routing_full_notm}} target to your new {{site.data.keyword.logs_full_notm}} instance
{: #migration-tutorial-la-plat-new-step4}
{: step}

1. [Set up service to service (S2S) authorization](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-logs-routing&interface=ui) between {{site.data.keyword.logs_routing_full_notm}} and {{site.data.keyword.logs_full_notm}} so {{site.data.keyword.logs_routing_full_notm}} can send logs to {{site.data.keyword.logs_full_notm}}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click the **Menu** icon ![Navigation Menu icon](/icons/icon_hamburger.svg "Menu") &gt; **Observability** &gt; **Logging** &gt; **Routing** &gt; **Cloud Logs targets**. 

3. Set the {{site.data.keyword.logs_full_notm}} target to reference the {{site.data.keyword.logs_full_notm}} instance you created.

## Deploy logging agents to send data to the {{site.data.keyword.logs_full_notm}} instance
{: #migration-tutorial-la-plat-new-step5}
{: step}

IBM Cloud platform logs associated with resources in your account are automatically sent to your {{site.data.keyword.logs_full_notm}} instance. If you want infrastructure and application logs to be sent to your {{site.data.keyword.logs_full_notm}} instance, you will need to deploy a [logging agent](/docs/cloud-logs?topic=cloud-logs-agent-about) in those environments.

You can use a service ID or a trusted profile as the identity that is used by the agent to authenticate with the IBM Cloud Logs service. Choose a supported authorization method for the environment where you plan to deploy the agent: For more information, see [Authorization methods](/docs/cloud-logs?topic=cloud-logs-agent-about#agent-auth-methods).
{: important}

- [ ] [Deploy the agent for Kubernetes clusters](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy)

- [ ] [Deploy the agent for OpenShift clusters](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy)

- [ ] [Deploy the agent for Linux servers](/docs/cloud-logs?topic=cloud-logs-agent-linux)

- [ ] [Deploy the agent for Windows servers](/docs/cloud-logs?topic=cloud-logs-agent-windows)

- [ ] [Deploy the agent to collect and route rSyslog data](/docs/cloud-logs?topic=cloud-logs-agent-rsyslog)

## Configure IAM policies
{: #migration-tutorial-la-plat-new-step6}
{: step}

You must configure IAM policies to grant access to work with the {{site.data.keyword.logs_full_notm}} service. For more information, see [Geting started with IAM](/docs/cloud-logs?topic=cloud-logs-iam).

## Create resources in {{site.data.keyword.logs_full_notm}}
{: #migration-tutorial-la-plat-new-step7}
{: step}

You might want to configure some views and alerts that you currently have in your {{site.data.keyword.la_full_notm}} instances.

- To create views, see [Managing custom views](/docs/cloud-logs?topic=cloud-logs-custom_views).
- To create dashboards, see [Managing dashboards](/docs/cloud-logs?topic=cloud-logs-create_dashboards).
- Deploy an extension. Extensions are pre-defined resources that you can easily deploy to start monitoring your data. See [Managing extensions](/docs/cloud-logs?topic=cloud-logs-extensions).

## Remove {{site.data.keyword.la_full_notm}} instances in the account
{: #migration-tutorial-la-plat-new-step8}
{: step}

After you have completed the migration and verification process, remove your Log Analysis instance and related resources by following the instructions in [Removing deprecated {{site.data.keyword.la_full_notm}} instances with platform logs enabled](/docs/cloud-logs?topic=cloud-logs-migration-remove-plat).
