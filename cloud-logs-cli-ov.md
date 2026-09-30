---

copyright:
  years:  2024, 2026
lastupdated: "2026-09-30"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Working with the {{site.data.keyword.logs_full_notm}} CLI
{: #cloud-logs-cli-ov}

You can use the {{site.data.keyword.logs_full}} command-line interface (CLI) to manage your {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

Both `ibmcloud cloud-logs` and `ibmcloud logs` can be used to run {{site.data.keyword.logs_full_notm}} CLI commands.
{: tip}

Use `ibmcloud cloud-logs COMMAND --help` for more information about a command.
{: tip}

## Prerequisites
{: #cloud-logs-cli-ov-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

## Installing the {{site.data.keyword.logs_full_notm}} CLI Plugin
{: #cloud-logs-cli-ov-install}

Install the {{site.data.keyword.logs_full_notm}} CLI plug-in by running the following command:

```text
ibmcloud plugin install logs
```
{: pre}

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

## Setting the {{site.data.keyword.logs_full_notm}} instance
{: #cloud-logs-cli-ov-context}

To target the {{site.data.keyword.logs_full_notm}} instance every time you run a CLI command, use one of the following options:

- Option 1: Run the `ibmcloud logs config set` command to configure the service URL and persist the value in the terminal that you use to run the commands.

    ```text
    ibmcloud logs config set service-url https://{API_endpoint}
    ```
    {: pre}

    Global parameters can be stored in a persistent configuration so that you do not need to manually specify each time the plug-in is invoked. Each parameter can be managed with the `ibmcloud logs config` commands.
    {: tip}

- Option 2: Set the service endpoint in each command that you run.

    Export an environment variable with your {{site.data.keyword.logs_full_notm}} service endpoint URL.

    ```text
    export LOGS_URL=https://{API_endpoint}
    ```
    {: pre}

    Add the `--service-url` to each command.

    ```text
    ibmcloud logs --service-url https://$LOGS_URL
    ```
    {: pre}

    Replace `{API_endpoint}` with the API endpoint that is specific to your instance. The API endpoint information can be copied from the service details page in the {{site.data.keyword.logs_full_notm}} UI.



## Commands to manage alerts
{: #cloud-logs-cli-ov-cl-cmd-alerts}

The following table lists the commands that you can use to manage alerts:

| Command | Description |
|---------|-------------|
| `alert-definition` | Get an alert definition by ID. |
| `alert-definition-create` | Create an alert definition. |
| `alert-definition-delete` | Delete an alert definition by ID. |
| `alert-definition-update` | Update an alert definition by ID. |
| `alert-definitions` | List alert definitions. |
{: caption="{{site.data.keyword.logs_full_notm}} V3 alert definition CLI commands" caption-side="bottom"}


## Commands to manage queries
{: #cloud-logs-cli-ov-cl-cmd-query}

The following table lists the command that you can use to manage queries:

| Command | Description |
|---------|-------------|
| `query` | Run a query to search the logs. |
{: caption="{{site.data.keyword.logs_full_notm}} query CLI commands" caption-side="bottom"}

The following table lists the commands that you can use to manage background queries:

| Command | Description |
|---------|-------------|
| `background-query-cancel`, `bgq-cancel` | Cancel a background query. |
| `background-query-create`, `bgq-create` | Submit a background query to be processed asynchronously. |
| `background-query-data`, `bgq-data` | Data of the background query to search the logs. |
| `background-query-status`, `bgq-status` | Get the status of a background query. |
{: caption="{{site.data.keyword.logs_full_notm}} background query (asynchronous archive query) CLI commands" caption-side="bottom"}

## Commands to manage data access rules
{: #cloud-logs-cli-ov-cl-cmd-bck}

The following table lists the commands that you can use to manage data access rules:

| Command | Description |
|---------|-------------|
| `data-access-rule-create` | Create a data access rule. |
| `data-access-rule-delete` | Delete a data access rule. |
| `data-access-rule-update` | Update a data access rule. |
| `data-access-rules` | Get a service instance's data access rules by ID. |
{: caption="{{site.data.keyword.logs_full_notm}} data access rule CLI commands" caption-side="bottom"}

## Commands to manage data usage
{: #cloud-logs-cli-ov-cl-cmd-data-usage}

The following table lists the commands that you can use to manage data usage:

| Command | Description |
|---------|-------------|
| `data-usage` | Get the daily and detailed data usage. |
| `data-usage-metrics-export-status` | Get the data usage metrics export status. |
| `data-usage-metrics-export-status-update` | Update the data usage metrics export status. |
{: caption="{{site.data.keyword.logs_full_notm}} data usage CLI commands" caption-side="bottom"}


## Commands to manage enrichments
{: #cloud-logs-cli-ov-cl-cmd-enrich}

The following table lists the commands that you can use to manage enrichments:

| Command | Description |
|---------|-------------|
| `enrichment-create` | Create an enrichment. |
| `enrichment-delete` | Delete enrichments. |
| `enrichments` | List all enrichments. |
{: caption="{{site.data.keyword.logs_full_notm}} enrichment CLI commands" caption-side="bottom"}


## Commands to manage streaming
{: #cloud-logs-cli-ov-cl-cmd-stream}

The following table lists the commands that you can use to manage streaming:

| Command | Description |
|---------|-------------|
| `event-stream-target-create` | Create an {{site.data.keyword.messagehub_full_notm}} integration. |
| `event-stream-target-delete` | Delete an {{site.data.keyword.messagehub}} integration by ID. |
| `event-stream-target-update` | Update an {{site.data.keyword.messagehub}} integration. |
| `event-stream-targets` | List all {{site.data.keyword.messagehub}} integrations.
{: caption="{{site.data.keyword.logs_full_notm}} {{site.data.keyword.messagehub}} integration CLI commands" caption-side="bottom"}


## Commands to manage events2metrics
{: #cloud-logs-cli-ov-cl-cmd-e2m}

The following table lists the commands that you can use to manage events2metrics:

| Command | Description |
|---------|-------------|
| `events2metrics`, `e2m` | Gets the events to metrics definitions by ID. |
| `events2metrics-create`, `e2m-create` | Creates the events to metrics definitions. |
| `events2metrics-delete`, `e2m-delete` | Deletes the events to metrics definitions by ID. |
| `events2metrics-list`, `e2m-list` | Lists the events to metrics definitions. |
| `events2metrics-update`, `e2m-update` | Updates the events to metrics definitions. |
{: caption="{{site.data.keyword.logs_full_notm}} events to metrics CLI commands" caption-side="bottom"}

## Commands to manage webhooks
{: #cloud-logs-cli-ov-cl-cmd-wh}

The following table lists the commands that you can use to manage webhooks:

| Command | Description |
|---------|-------------|
| `outgoing-webhook` | Gets an outbound integration by ID. |
| `outgoing-webhook-create` | Create an outbound integration. |
| `outgoing-webhook-delete` | Delete an outbound integration. |
| `outgoing-webhook-update` | Update an outbound integration. |
| `outgoing-webhooks` | List outbound integrations. |
{: caption="{{site.data.keyword.logs_full_notm}} outbound integration CLI commands" caption-side="bottom"}

## Commands to manage policies
{: #cloud-logs-cli-ov-cl-cmd-pol}

The following table lists the commands that you can use to manage policies:

| Command | Description |
|---------|-------------|
| `policies` | Gets policies. |
| `policy` | Gets policy by ID. |
| `policy-create` | Creates a new policy. |
| `policy-delete` | Deletes an existing policy. |
| `policy-update` | Updates an existing policy. |
{: caption="{{site.data.keyword.logs_full_notm}} policy CLI commands" caption-side="bottom"}



## Commands to manage rule groups
{: #cloud-logs-cli-ov-cl-cmd-rg}

The following table lists the commands that you can use to manage rule groups:

| Command | Description |
|---------|-------------|
| `rule-group` | Gets a rule group by groupid. |
| `rule-group-create` | Creates a rule group. |
| `rule-group-delete` | Deletes a rule group by groupid. |
| `rule-group-update` | Updates a rule group by groupid. |
| `rule-groups` | Gets all rule groups. |
{: caption="{{site.data.keyword.logs_full_notm}} rules CLI commands" caption-side="bottom"}


## Commands to manage views
{: #cloud-logs-cli-ov-cl-cmd-view}

The following table lists the commands that you can use to manage views:

| Command | Description |
|---------|-------------|
| `view` | Gets a view by ID. |
| `view-create` | Creates a new view. |
| `view-delete` | Deletes a view by ID. |
| `view-update` | Replaces an existing view. |
| `views` | Lists all company public views. |
{: caption="{{site.data.keyword.logs_full_notm}} view CLI commands" caption-side="bottom"}

## Commands to manage view folders
{: #cloud-logs-cli-ov-cl-cmd-view-folder}

The following table lists the commands that you can use to manage view folders:

| Command | Description |
|---------|-------------|
| `view-folder` | Get view folder. |
| `view-folder-create` | Create view folder. |
| `view-folder-delete` | Deletes a view folder by ID. |
| `view-folder-update` | Replaces an existing view folder. |
| `view-folders` | List view's folders. |
{: caption="{{site.data.keyword.logs_full_notm}} view folder CLI commands" caption-side="bottom"}

## Commands to manage extensions
{: #cloud-logs-cli-ov-cl-cmd-ext}

The following table lists the commands that you can use to manage extensions:

| Command | Description |
|---------|-------------|
| `extensions` | Gets an extension by ID. |
| `extension-deployment` | Get deplayment details by an extension. |
| `extension-deployment-delete` | Delete deployment of an extension. |
| `extension-deployment-managep` | Deploy or update deployment of an extension. |
| `extensions` | Get list of extensions. |
{: caption="{{site.data.keyword.logs_full_notm}} extensions CLI commands" caption-side="bottom"}
