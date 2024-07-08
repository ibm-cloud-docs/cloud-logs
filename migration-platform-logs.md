---

copyright:
  years:  2024
lastupdated: "2024-07-04"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating instances that collect platform logs
{: #migration-platform-logs}

Migrating {{site.data.keyword.la_full}} instances that collect platform logs into {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}} require the configuration of the {{site.data.keyword.logs_routing_full_notm}} service in the account and provisioning {{site.data.keyword.logs_full_notm}} instances. A migration tool is provided to help you migrate.
{: shortdesc}


## {{site.data.keyword.la_full_notm}} platform logs architecture
{: #migration-platform-logs-ov}

Before the release of the {{site.data.keyword.logs_routing_full_notm}} service and the {{site.data.keyword.logs_full_notm}} service, you could only collect platform logs through the {{site.data.keyword.la_full_notm}} instance that is configured with the platform flag in the same region where the logs are generated.

Only one {{site.data.keyword.la_full_notm}} instance can be configured in a region to receive platform logs.



## Options for migration
{: #migration-platform-logs-options}

With the release of the {{site.data.keyword.logs_routing_full_notm}} service and the {{site.data.keyword.logs_full_notm}} service, you have different options on how to configure management of platform logs in the account. You can keep the current {{site.data.keyword.la_full_notm}} architecture and maintain data locality or if you prefer, you can move to a centralize model where all logs are collected in a single {{site.data.keyword.logs_full_notm}} instance.


The following image shows the high-level view of how {{site.data.keyword.logs_routing_full_notm}} and {{site.data.keyword.logs_full_notm}} are integrated so you can monitor and alert on platform logs.

![Account overview of handling platform logs.](/images/migration-la-1.png "Account overview of handling platform logs."){: caption="Figure 1. Overview of handling platform logs." caption-side="bottom"}



Common to both options is that to migrate the {{site.data.keyword.la_full_notm}} instances that collect platform logs into {{site.data.keyword.logs_full_notm}} in {{site.data.keyword.cloud_notm}}, you must configure the {{site.data.keyword.logs_routing_full_notm}} service in the account and provision 1 or more {{site.data.keyword.logs_full_notm}} instances depending on the option that you choose.

Choose based on your requirements from any of the following options:

| Requirement                        | Migration scenario |
|------------------------------------|--------------------|
| Centralize platform logs           | Migrate {{site.data.keyword.la_full_notm}} instances into 1 {{site.data.keyword.logs_full_notm}} instance |
| Data locality required             | Migrate {{site.data.keyword.la_full_notm}} instances into N {{site.data.keyword.logs_full_notm}} instances, replicating the current {{site.data.keyword.la_full_notm}} architecture |
{: caption="Table 1. Migration scenarios"}

Check the list of services that are supported in {{site.data.keyword.logs_routing_full_notm}} and generate platform logs. If you use {{site.data.keyword.cloud_notm}} services that generate platform logs that are not in that list, continue to use your {{site.data.keyword.la_full_notm}} instance until you verify you receive them in the {{site.data.keyword.logs_full_notm}} instance. For more information, see [Supported services](/docs/logs-router?topic=logs-router-cloud_services).{: important}


## Migrating to a central model
{: #migration-platform-logs-options-1}

The following image shows a high-level view of the account after you migrate {{site.data.keyword.la_full_notm}} instances from multiple regions in the account into 1 instance of {{site.data.keyword.logs_full_notm}}:

![High-level view of the account after {{site.data.keyword.la_full_notm}} instances from multiple regions in the account are migrated into 1 instance of {{site.data.keyword.logs_full_notm}}](/images/migration-plat-logs-central.svg "Account overview of handling logs."){: caption="Figure 1. High-level view of the account after {{site.data.keyword.la_full_notm}} instances from multiple regions in the account are migrated into 1 instance of {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}

## Migrating maintaing data locality
{: #migration-platform-logs-options-2}

You can use the migration tool to migrate {{site.data.keyword.la_full_notm}} instances into N {{site.data.keyword.logs_full_notm}} instances, replicating the current {{site.data.keyword.la_full_notm}} architecture. Then, after you have migrated all instances, you can use the migration tool to configure {{site.data.keyword.logs_routing_full_notm}} in the account. For more information, see [Migrating {{site.data.keyword.la_full_notm}} instances into N {{site.data.keyword.logs_full_notm}} instances for data locality](/docs/cloud-logs?topic=cloud-logs-migration-la-n-cl).

The following image shows a high-level view of the account after {{site.data.keyword.la_full_notm}} instances from multiple regions in the account are migrated into multiple instances of {{site.data.keyword.logs_full_notm}}:

![High-level view of the account after {{site.data.keyword.la_full_notm}} instances from multiple regions in the account are migrated into multiple instances of {{site.data.keyword.logs_full_notm}}](/images/migration-plat-logs-many.svg "Account overview of handling logs."){: caption="Figure 1. High-level view of the account after {{site.data.keyword.la_full_notm}} instances from multiple regions in the account are migrated into multiple instances of {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}


## Migration steps
{: #la-migration-steps}

To migrate {{site.data.keyword.la_full_notm}} instances that collect platform logs in the account, complete the following steps:

The Migration tool migrates instances replicating the current account architecture, that is, applying a data locality model.

1. Run the migration tool to collect information about what instances need to be migrated and their resources.

    ```text
    ibmcloud logging migrate generate-terraform --scope account --service logdna
    ```
    {: pre}


2. Migrate each instance by running one of these commands:

    * To generate terraform scripts that you can modify, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --terraform
       ```
       {: pre}

    * To migrate an instance by applying Terraform, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --terraform -f
       ```
       {: pre}

    * To migrate an instance directly without Terraform, run:

       ```text
       ibmcloud logging migrate create-resources --scope instance --instance-crn CRNvalue --api
       ```
       {: pre}

    You must migrate all your {{site.data.keyword.la_full_notm}} instances that collect platform logs before you use the Migration tool to configure {{site.data.keyword.logs_routing_full_notm}} in the account.{: important}

3. Manually configure notification channels such as email, and PagerDuty.

    If you use the terraform option, variables are provided for you to enter information on the slack URL and the webhook header apikey.

   {{site.data.keyword.logs_full_notm}} alerting is done by using the {{site.data.keyword.en_full_notm}} service.
   {: note}

4. After you migrate each of the instances in the account, configure {{site.data.keyword.logs_routing_full_notm}}.

    ```text
    ibmcloud logging migrate create-resources --scope platform-logs -i [private|public]
    ```
    {: pre}

    The `-i` option indicates whether a `public` or `private` endpoint is used to receive platform logs by the {{site.data.keyword.logs_full_notm}} instance. The default is `public`.

    For more information about this command, see [`ibmcloud logging migrate create-resources`](/docs/cloud-logs?topic=cloud-logs-migration_cli#logging-migrate-create-resources)

    The tool configures the account to map your current {{site.data.keyword.la_full_notm}} architecture for managing platform logs through {{site.data.keyword.logs_routing_full_notm}}.

5. Validate that the new configuration is working for your requirements.

6. After you validate your configuration is operating as required, delete your {{site.data.keyword.la_full_notm}} instances and your legacy configurations to send data.


## Validating the new architecture
{: #migration-platform-logs-options-validate}

While you migrate and validate the new architecture, you must collect platform logs in your {{site.data.keyword.la_full_notm}} instances, same as you currently do now. You must configure {{site.data.keyword.logs_routing_full_notm}} to send logs to your {{site.data.keyword.la_full_notm}} instances with rules that map your current {{site.data.keyword.la_full_notm}} architecture in the account. If you fail to configure this route, logs will stop being routed to your current {{site.data.keyword.la_full_notm}} instances. For more information on how to configure a double target in a region, see [Configuring two targets of different types](/docs/logs-router?topic=logs-router-config-2-targets&interface=api).
{: important}


What {{site.data.keyword.logs_routing_full_notm}} configuration do you need?

- 1 tenant per region
- 1 target configured for the {{site.data.keyword.la_full_notm}} instance in the region
- 1 target for the {{site.data.keyword.logs_full_notm}} instance that is the result of migrating an {{site.data.keyword.la_full_notm}} instance in the region


Until you have validated the new architecture and you can remove the {{site.data.keyword.la_full_notm}} instances from the account, you must continue managing data through the deprecated services.
{: important}


For example, your validation configuration in the account should look like the following if you choose a central architecture:

![High-level view of the account during validation of a centralize architecture."](/images/migration-platform-central-validation.svg "Account overview of handling logs."){: caption="Figure 1. High-level view of the account during validation of a centralize architecture" caption-side="bottom"}


For example, your validation configuration in the account should look like the following if you chose a data locality architecture:

![High-level view of the account during validation of a centralize architecture."](/images/migration-platform-many-validation.svg "Account overview of handling logs."){: caption="Figure 1. High-level view of the account during validation of a centralize architecture" caption-side="bottom"}
