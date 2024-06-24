---

copyright:
  years:  2024
lastupdated: "2024-06-20"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating the platform logs configuration
{: #migration-plat-logs}

You can use the migration tool to configure {{site.data.keyword.logs_full_notm}} to receive platform logs.
{: shortdesc}

Only one {{site.data.keyword.logs_full_notm}} instance can be configured in a region to receive platform logs.
{: note}

You must migrate all your {{site.data.keyword.la_full_notm}} instances before you use the migration tool to configure an {{site.data.keyword.logs_full_notm}} instance to receive platform logs.
{: important}


## What to expect
{: #plat-logs-migration-what}

When you run the migration tool to migrate your platform logs configuration in the region:

* The {{site.data.keyword.logs_full_notm}} instance that was created from the {{site.data.keyword.la_full_notm}} instance that was receiving platform logs is configured to receive platform logs in the region.

* If the region has an existing {{site.data.keyword.logs_full_notm}} instance configured to receive platform logs, the migration tool will issue an error.

* You can specify whether a public or private endpoint is used to receive platform logs by the {{site.data.keyword.logs_full_notm}} instance.

## Migration steps
{: #plat-logs-migration-steps}

To migrate your platform log configuration, complete the following steps:

1. Run the migration tool to [migrate your {{site.data.keyword.la_full_notm}} instances](/docs/cloud-logs?topic=cloud-logs-migration-la).

2. After you migrate the {{site.data.keyword.la_full_notm}} instances in the region, configure the {{site.data.keyword.logs_full_notm}} instance in the region that receives platform logs by running this command.

    ```text
    ibmcloud logging migrate create-resources --scope platform-logs -i private
    ```
    {: pre}

    The `-i` option indicates whether a `public` or `private` endpoint is used to receive platform logs by the {{site.data.keyword.logs_full_notm}} instance. The default is `public`.

    For more information about this command, see [`ibmcloud logging migrate create-resources`](/docs/cloud-logs?topic=cloud-logs-migration_cli#logging-migrate-create-resources)

3. Validate that the new configuration is working for your requirements.
