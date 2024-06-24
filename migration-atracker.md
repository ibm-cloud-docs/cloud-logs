---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating {{site.data.keyword.atracker_full_notm}} routes and targets
{: #migration-atracker}

If {{site.data.keyword.atracker_full_notm}} is configured in your environment to route activity tracking events to {{site.data.keyword.at_full_notm}} instances, the migration tool can be used to migrate the configuration. Your {{site.data.keyword.atracker_full_notm}} configuration is modified to route events to {{site.data.keyword.logs_full_notm}} instances that were created by using the migration tool.
{: shortdesc}

You must migrate your {{site.data.keyword.at_full_notm}} instances that are associated with {{site.data.keyword.atracker_full_notm}} routes and targets before you migrate your routes and targets. For information on migrating your {{site.data.keyword.at_full_notm}} instances, see [Migrating {{site.data.keyword.at_full_notm}} instances](/docs/cloud-logs?topic=cloud-logs-migration-at).
{: important}


## What to expect
{: #atracker-migration-what}

When you run the migration tool to migrate your {{site.data.keyword.atracker_full_notm}} configuration in the account:

### {{site.data.keyword.atracker_full_notm}} is already configured
{: #atracker-migration-what-1}

- The migration tool adds an extra `cloud-logs` target for each {{site.data.keyword.at_full_notm}} instance that you have in the account.

    There is a limit of targets per account. You can define up to 16 targets in total in an account.

    Make sure that you have enough targets unconfigured so that the migration tool can create 1 target per {{site.data.keyword.at_full_notm}} instance in the account.

    If you do not have enough targets, the migration process cannot be completed. Delete any unused targets and try again.

    If you cannot delete any exiting targets, You must manually migrate your {{site.data.keyword.atracker_full_notm}} configuration. Create manually 1 or more {{site.data.keyword.logs_full_notm}} instances so that you can route events from the account to these instances. For more information, see [Getting started](/docs/atracker?topic=atracker-getting-started).

- The migration tool adds a new route. The rules defined for {{site.data.keyword.at_full_notm}} instances are used as reference to create new rules to the newly created {{site.data.keyword.logs_full_notm}} instances. For example, if you have a route with a rule that sends `us-south` events to {{site.data.keyword.at_full_notm}} instance `A`, the migration tool adds a rule to the new route that sends `us-south` events to the `cloud-logs` target that references the {{site.data.keyword.logs_full_notm}} instance `A` that is created using the migration tool.

### {{site.data.keyword.atracker_full_notm}} is not configured
{: #atracker-migration-what-2}

- The migration tool configures the account to map your current {{site.data.keyword.at_full_notm}} architecture to a similar one with the new {{site.data.keyword.logs_full_notm}} instances.

- A `clous-logs` target is created for each {{site.data.keyword.at_full_notm}} instance.

- A new route is added to configure {{site.data.keyword.atracker_full_notm}} after migration that routes events to {{site.data.keyword.logs_full_notm}} instances.

- The rules defined in the route are as follows:

    For `eu-de`, the rule routes events generated in the `eu-de` region and `global` events to the {{site.data.keyword.logs_full_notm}} instance created in the `eu-de` region.

    For other [supported regions](/docs/atracker?topic=atracker-regions), the rule routes events from that region only to the {{site.data.keyword.logs_full_notm}} instance created in that region. For example, for `us-south`, the rule routes events generated in the `us-south` region to the {{site.data.keyword.logs_full_notm}} instance created in the `us-south` region.


## Migration steps
{: #atracker-migration-steps}

To migrate {{site.data.keyword.atracker_full_notm}} routes and targets in the account, complete the following steps:

1. Run the migration tool to [migrate your {{site.data.keyword.at_full_notm}} instances](/docs/cloud-logs?topic=cloud-logs-migration-at).

2. After you migrate each of the {{site.data.keyword.at_full_notm}} instances in the account, configure {{site.data.keyword.atracker_full_notm}} by running this command.

    ```text
    ibmcloud logging migrate create-resources --scope atracker
    ```
    {: pre}

3. Validate that the new configuration is working for your requirements.
