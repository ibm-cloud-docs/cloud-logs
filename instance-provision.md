---

copyright:
  years:  2024
lastupdated: "2024-07-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning an instance
{: #instance-provision}

You can provision an instance of the {{site.data.keyword.logs_full_notm}} service through the {{site.data.keyword.cloud_notm}} catalog, and programmatically by using a terraform script or the Resource Controller API.
{: shortdesc}

If you are creating an instance with [{{site.data.keyword.cos_full_notm}} buckets](/docs/cloud-logs?topic=cloud-logs-about-bucket#about-bucket-ov), make sure you create a [S2S authorization policy](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos&interface=ui) that grants {{site.data.keyword.logs_full_notm}} access to {{site.data.keyword.cos_full_notm}}, before proceeding. The policy should grant access to the {{site.data.keyword.cos_full_notm}} service as a whole, not just to the bucket. After creating the instance, the policy can be updated to restrict access to just the bucket. The [bucket details](/docs/cloud-logs?topic=cloud-logs-about-bucket&interface=ui) can also be configured any time after the service instance is created.
{: important}

There are limits for each provisioned instance. For more information, see [Limits per instance](/docs/cloud-logs?topic=cloud-logs-limits&interface=ui#limits-per-instance).
{: note}

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

   For more information about service plans, see [Service plans and pricing](/docs/cloud-logs?topic=cloud-logs-service_plans).-->

10. Optionally, add the [bucket details](/docs/cloud-logs?topic=cloud-logs-about-bucket#about-bucket-ov).

11. Click **Create**.

After you provision an instance, the UI opens.

Next, configure a log source by adding a logging agent. This agent is responsible for collecting and forwarding logs to your instance.



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

    By default, the standard plan is set.

    For more information about service plans, see [Service plans and pricing](/docs/cloud-logs?topic=cloud-logs-service_plans).

9. Optionally, add the [bucket details](/docs/cloud-logs?topic=cloud-logs-about-bucket#about-bucket-ov).

10. Click **Create**.

After you provision an instance, the UI opens.

Next, configure a log source by adding a logging agent. This agent is responsible for collecting and forwarding logs to your instance.



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

 
