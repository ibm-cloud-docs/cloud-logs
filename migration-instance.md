---

copyright:
  years:  2024
lastupdated: "2024-08-19"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Migrating 1 instance with the migration tool
{: #migration-instance}

You can use the Migration tool, a command line tool, to migrate 1 {{site.data.keyword.la_full_notm}} instance or 1 {{site.data.keyword.at_full_notm}} instance and its configuration to a {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

## Before you begin
{: #migration-instance-prereqs}

- Learn about migration. For more information, see [Migrating {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-migration-intro).

- Learn about the migration tool. For more information, see [Migrating tool](/docs/cloud-logs?topic=cloud-logs-migration-tool).

- To apply the Terraform scripts, you must export `IC_API_KEY` with an API key that has permissions to create and manage an instance of {{site.data.keyword.logs_full_notm}}.

    ```text
    export IC_API_KEY=xxxxxx
    ```
    {: pre}

    If running the tool in Windows, use `set IC_API_KEY=xxxxxx` instead.
    {: note}

    The API key must have permissions to create instances, create buckets, and manage {{site.data.keyword.logs_full_notm}} instances.{: note}


## Options migrating instances
{: #migration-instance-options}

- Option 1: You can automatically migrate an instance by using the Migration tool. Run the following command:

    ```text
    ibmcloud logging migrate create-resources --scope instance --instance-crn CRN --api
    ```
    {: codeblock}

- Option 2: You can migrate an instance by using the Migration tool to generate Terraform scripts that you can customize and apply at a later time. Run the following command:

    ```text
    ibmcloud logging migrate create-resources --scope instance --instance-crn CRN --terraform
    ```
    {: codeblock}

    Use this option to plan and prepare the migration of an instance that is provisioned in a region where the {{site.data.keyword.logs_full_notm}} service is not available. {: tip}

- Option 3: You can migrate an instance by using the Migration tool to generate and apply Terraform scripts. Run the following command:

    ```text
    ibmcloud logging migrate create-resources --scope instance --instance-crn CRN --terraform -f
    ```
    {: codeblock}

    When you are asked if you want to apply the Terraform scripts, make any changes that you need to the Terraform files that are located in `/migration-tool/cl/accountID/instanceID/service-type/terraform/tf-directory/`. Save the changes. Then, enter `yes` to apply the Terraform scripts.


For information about the files that are generated by the Migration tool, see [Files that are generated by the Migration tool](/docs/cloud-logs?topic=cloud-logs-migration-tool-files).


## What happens when an instance is migrated
{: #migration-instance-what}

When you provision an {{site.data.keyword.la_full_notm}} instance or an {{site.data.keyword.at_full_notm}} instance in {{site.data.keyword.cloud_notm}}, you can:
- Attach tags to the instance
- Integrate with the {{site.data.keyword.cos_full_notm}} service to configure archiving of the data for long term storage. Authorization is done by using service credentials.

When you provision an {{site.data.keyword.logs_full_notm}} instance, you can:
- Attach tags to the instance
- Integrate with the {{site.data.keyword.cos_full_notm}} service to attach a data bucket and a metrics bucket to the instance so that you can store data and metrics for long term storage and querying. Authorization between services is done by using a service to service authorization.
- Integrate with the {{site.data.keyword.en_full_notm}} service to configure notification channels and trigger alerts. Authorization between services is done by using a service to service authorization.

When you run the Migration tool to migrate an instance,
- A new {{site.data.keyword.logs_full_notm}} instance is created for the {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance that you migrate by using the Migration tool.

    - The name of the {{site.data.keyword.la_full_notm}} instance or {{site.data.keyword.at_full_notm}} instance is used to name the new {{site.data.keyword.logs_full_notm}} instance.

- Tags attached to your instance are added to the new {{site.data.keyword.logs_full_notm}} instance.

- Two {{site.data.keyword.cos_full_notm}} buckets are created and associated with the {{site.data.keyword.logs_full_notm}} instance if your instance has archiving configured. One bucket is used to store data. The other bucket is used to store metrics that are generated from logs.

    - If Activity Tracker, Monitoring, or Associated key management services are configured, the same configuration is applied to the new buckets.



    - You cannot use as your metrics bucket a bucket with lifecycle policies where data is retained and cannot be deleted.

    - Service to service authorizations are created between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.cos_full_notm}} buckets.

- Public views are created. For each view, the Migration tool created a view.

- Alerts are configured. For each view with an alert, a public view definition is created and alert definition is created.

- A dashboard is created for each dashboard or screen.

- Block rules are created. For each exclusion rule, a block rule is created.

- If you have alerts configured in your instance, and you have an instance of the {{site.data.keyword.en_full_notm}} provisioned in the account, an outbound integration is configured between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance.

    - A service to service authorization is created between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance.



## Known issues
{: #mig1instance-known}

- If you have a `/migration-tool/` directory with assets that are generated from a previous run of the command for migrate 1 instance, you must provide a different directory. If you do not provide a different directory, your migration reports errors.
