---

copyright:
  years:  2024, 2026
lastupdated: "2026-03-25"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning an instance
{: #instance-provision}

You can provision an instance of the {{site.data.keyword.logs_full_notm}} service through the {{site.data.keyword.cloud_notm}} catalog, and programmatically by using a terraform script or the Resource Controller API.
{: shortdesc}

{{site.data.keyword.logs_full_notm}} integrates with IBM Cloud Object Storage for long term storage of the data and for collection of metrics, and with IBM Cloud Event Notifications for triggering of alerts. Authorization between services is done by configuring IAM service to service authorizations in the account.

You can run Cloud Logs without a data bucket or a metrics bucket. However, features like TCO Optimizer to manage data thorugh different data pipelines at different costs, long term data querying or metrics related features would not be available.

There are limits for each provisioned instance. For more information, see [Limits per instance](/docs/cloud-logs?topic=cloud-logs-limits&interface=ui#limits-per-instance).
{: note}


{{_include-segments/instance-naming-limits.md}}

## Provisioning an instance through the Observability dashboard
{: #instance-provision-ui}
{: ui}

To provision an instance from the Observability dashboard in the {{site.data.keyword.cloud_notm}}, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click the **Menu** icon ![Navigation Menu icon](/icons/icon_hamburger.svg "Menu") &gt; **Observability** to access the *Observability* dashboard.

3. Click **Logging** &gt; **Instances**. You might need to click the **Cloud Logs** tab to see your {{site.data.keyword.logs_full_notm}} instances.

4. Click **Create**.

5. Select the required service for your instance.

6. Select the [location](/docs/cloud-logs?topic=cloud-logs-regions&interface=ui) where you plan to provision the instance.

7. Enter a name for the service instance.

8. Select a resource group.

    By default, the **default** resource group is set.

    **Note:** If you are not able to select a resource group, check that you have editing permissions on the resource group where you want to provision the instance.

9. Select the `Standard` service plan.

    By default, the Standard plan is set.

   For more information about service plans, see [Service plans and pricing](/docs/cloud-logs?topic=cloud-logs-service_plans).

10. Choose a retention plan. Valid values are `7 days`, `14 days`, `30 days`, `60 days` or `90 days`.

11. Click **Create**.

After you provision an instance, the UI opens.



## Provisioning an instance through the catalog
{: #instance-provision-catalog}
{: ui}

To provision an instance of {{site.data.keyword.logs_full_notm}} through the {{site.data.keyword.cloud_notm}} catalog, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Logging and Monitoring** category.

4. Click the **{{site.data.keyword.logs_full_notm}}** tile.

5. Select the [location](/docs/cloud-logs?topic=cloud-logs-regions) where you plan to provision the instance.

6. Enter a name for the service instance.

7. Select a resource group.

    By default, the **Default** resource group is set.

    **Note:** If you are not able to select a resource group, check that you have editing permissions on the resource group where you want to provision the instance.

8. Select the `Standard` service plan.

    By default, the standard plan is set. For more information about service plans, see [Service plans and pricing](/docs/cloud-logs?topic=cloud-logs-service_plans).

9. Choose a retention plan. Valid values are `7 days`, `14 days`, `30 days`, `60 days` or `90 days`.

10. Click **Create**.

After you provision an instance, the UI opens.




## Provisioning an instance through the CLI
{: #instance-provision-cli}
{: cli}

To provision an instance of {{site.data.keyword.logs_full_notm}} through the command line, complete the following steps:

1. [Pre-requisite] Installation of the {{site.data.keyword.cloud_notm}} CLI.

   For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

   If the CLI is installed, continue with the next step.

2. Log in to the region in the {{site.data.keyword.cloud_notm}} where you want to provision the instance. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

3. Set the resource group where you want to provision the instance. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. Create the instance. Run the [ibmcloud resource service-instance-create](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command:

    ```text
    ibmcloud resource service-instance-create NAME logs SERVICE_PLAN_NAME LOCATION -p '{"private_endpoints_only": PRIVATE_ENDPOINT}'
    ```
    {: codeblock}

    Where

    `NAME` is the name of the instance

    `SERVICE_PLAN_NAME` is the type of plan. Valid value is *standard*.

    `LOCATION` is the region where the logging instance is created. To get the latest list of locations that are available for the {{site.data.keyword.logs_full_notm}} service, see [Locations](/docs/cloud-logs?topic=cloud-logs-regions).

    * `PRIVATE_ENDPOINT` is either `true` or `false`.  If `true` only [private endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api) can be used to access the instance.

       Unless otherwise specified when provisioning an instance, the default is for the instance to be accessible by both public and private endpoints.
       {: note}

    For example, to provision an instance with the standard plan that can be accessed only by private endpoints, run the following command:

    ```text
    ibmcloud resource service-instance-create my-instance logs standard us-south -p '{"private_endpoints_only": true}'
    ```
    {: codeblock}



## Next steps
{: #instance-provision-next}

{{site.data.keyword.logs_full_notm}} integrates with{{site.data.keyword.cos_full_notm}} for long term storage of the data and for collection of metrics, and with {{site.data.keyword.en_full_notm}} for triggering of alerts. Authorization between services is done by configuring IAM service to service (S2S) authorizations in the account.

After you provision the instance, complete the following steps:

1. Attach a data bucket and a metrics bucket to store data for long term storage and for search. For more information, see [Configuring buckets](/docs/cloud-logs?topic=cloud-logs-about-bucket).

2. Configure an outbound integration to an {{site.data.keyword.en_full_notm}} instance to send notifications to destinations of your choice such as email, or slack. For more information, see [Configuring an outbound integration to connect {{site.data.keyword.logs_full_notm}} with {{site.data.keyword.en_full_notm}}](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure) and [Working with notification channels](/docs/cloud-logs?topic=cloud-logs-destinations).

3. Configure one or more log sources. Choose any of the following options:

    - Configure the logging agent. This agent is responsible for collecting and forwarding logs to your instance. For more information, see [The logging agent](/docs/cloud-logs?topic=cloud-logs-agent-about).

    - Configure {{site.data.keyword.atracker_full_notm}} to route auditing events, both [global](/docs/atracker?topic=atracker-event_types#event_types_global) and [location-based](/docs/atracker?topic=atracker-event_types#event_types_location) event data, in your {{site.data.keyword.cloud_notm}} to the {{site.data.keyword.logs_full_notm}} instance. For more information, see [Getting started with {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-getting-started).

    - Configure {{site.data.keyword.logs_routing_full}} to route platform logs from your {{site.data.keyword.cloud_notm}} account to the {{site.data.keyword.logs_full_notm}} instance. For more information, see [Getting started with {{site.data.keyword.logs_routing_full}}](/docs/logs-router?topic=logs-router-getting-started).
