---

copyright:
  years:  2024
lastupdated: "2024-07-23"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_full_notm}} CLI
{: #cloud-logs-cli}

You can use the {{site.data.keyword.logs_full}} command-line interface (CLI) to manage your {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

## Prerequisites
{: #logs-cli-prereq-temp}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the {{site.data.keyword.logs_full_notm}} CLI plug-in by running the following command:

    ```text
    ibmcloud plugin install logs
    ```
    {: pre}

    You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
    {: tip}

* To target the {{site.data.keyword.logs_full_notm}} instance, use one of the following options.

    Option 1: Run the `ibmcloud logs config set` command.

      ```text
       ibmcloud logs config set service-url https://{instance_ID}.api.{region}.logs.cloud.ibm.com
      ```
      {: pre}


    Option 2: Export an environment variable with your {{site.data.keyword.logs_full_notm}} service endpoint URL.

      ```text
      export LOGS_URL=https://{instance_ID}.api.{region}.logs.cloud.ibm.com
      ```
      {: pre}

    Option 3: Set the service endpoint in the command.

      ```text
      ibmcloud logs --service-url https://{instance_ID}.api.{region}.logs.cloud.ibm.com
      ```
      {: pre}

    Replace `{instance_ID}` and `{region}` with the values that apply to your {{site.data.keyword.logs_full_notm}} service instance. The endpoint URL that is specific to your instance can be copied from the service details page in the {{site.data.keyword.logs_full_notm}} UI.

## Commands
{: #cl-commands}

The current supported version of the {{site.data.keyword.logs_full_notm}} CLI is 0.1.0. If any other version is installed, uninstall the plug-in that is installed and install the current {{site.data.keyword.logs_full_notm}} CLI plug-in.
{: important}

| Command | Description |
|---------|-------------|
| `ibmcloud logs alert` | Get an alert by ID. |
| `ibmcloud logs alert-create` | Create an alert. |
| `ibmcloud logs alert-delete` | Delete an alert. |
| `ibmcloud logs alert-update` | Update an alert. |
| `ibmcloud logs alerts` | List alerts. |
| `ibmcloud logs config` | Control persistent configuration. |
| `ibmcloud logs data-access-rule-create` | Create a data access rule. |
| `ibmcloud logs data-access-rule-delete` | Delete a data access rule. |
| `ibmcloud logs data-access-rule-update` | Update a data access rule. |
| `ibmcloud logs data-access-rules` | List the service instance's data access rules with the provided IDs. |
| `ibmcloud logs data-usage-metrics-export-status` | Get the data usage metrics export status. |
| `ibmcloud logs data-usage-metrics-export-status-update` | Update the data usage metrics export status. |
| `ibmcloud logs enrichment-create` | Create an enrichment. |
| `ibmcloud logs enrichment-delete` | Delete enrichments. |
| `ibmcloud enrichments` | List all enrichments. |
| `ibmcloud logs events2metrics, e2m` | Gets event to metrics definitions by ID. |
| `ibmcloud logs events2metrics-create`  \n `ibmcloud e2m-create` | Creates event to metrics definitions. |
| `ibmcloud logs events2metrics-delete`  \n `ibmcloud e2m-delete` | Deletes event to metrics definitions by ID. |
| `ibmcloud logs events2metrics-list`  \n `ibmcloud e2m-list` | Lists event to metrics definitions. |
| `ibmcloud logs events2metrics-update`  \n `ibmcloud e2m-update` | Updates event to metrics definitions. |
| `ibmcloud logs outgoing-webhook` | Gets an outbound integration by ID. |
| `ibmcloud logs outgoing-webhook-create` | Create an outbound integration. |
| `ibmcloud logs outgoing-webhook-delete` | Delete an outbound integration. |
| `ibmcloud logs outgoing-webhook-update` | Update an outbound integration. |
| `ibmcloud logs outgoing-webhooks` | Lists outbound integrations. |
| `ibmcloud logs policies` | Gets policies. |
| `ibmcloud logs policy` | Get a policy by ID. |
| `ibmcloud logs policy-create` | Create a policy. |
| `ibmcloud logs policy-delete` | Delete an existing policy. |
| `ibmcloud logs policy-update` | Update an existing policy. |
| `ibmcloud logs query` | Run a query to search the logs. |
| `ibmcloud logs rule-group` | Gets rule group by group ID. |
| `ibmcloud logs rule-group-create` | Create a rule group. |
| `ibmcloud logs rule-group-delete` | Delete a rule group by group ID. |
| `ibmcloud logs rule-group-update` | Update a rule group by group ID. |
| `ibmcloud logs rule-groups` | Get all rule groups. |
| `ibmcloud logs view` | Get a view by ID. |
| `ibmcloud logs view-create` | Create a view. |
| `ibmcloud logs view-delete` | Delete a view by ID. |
| `ibmcloud logs view-folder-create` | Create a view folder. |
| `ibmcloud logs view-folder-update` | Replace an existing view folder. |
| `ibmcloud logs view-folders` | List a view's folders. |
| `ibmcloud logs view-update` | Replace an existing view. |
| `ibmcloud logs views` | List all public views. |
{: caption="{{site.data.keyword.logs_full_notm}} CLI commands" caption-side="bottom"}

For more information about using these commands, log in to the {{site.data.keyword.cloud_notm}} and run `ibmcloud logs command_name -h`. For example, `ibmcloud logs views -h`.

