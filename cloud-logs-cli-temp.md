---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-31"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_full_notm}} CLI
{: #cloud-logs-cli-temp}

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
   ibmcloud logs config set service-url https://{API_endpoint}
   ```
   {: pre}


   Option 2: Export an environment variable with your {{site.data.keyword.logs_full_notm}} service endpoint URL.

   ```text
   export LOGS_URL=https://{API_endpoint}
   ```
   {: pre}

   Option 3: Set the service endpoint in the command.

   ```text
   ibmcloud logs --service-url https://{API_endpoint}
   ```
   {: pre}

   Replace `{API_endpoint}` with the API endpoint that is specific to your instance. The API endpoint information can be copied from the service details page in the {{site.data.keyword.logs_full_notm}} UI.

## Commands
{: #cl-commands}

The currently supported version of the {{site.data.keyword.logs_full_notm}} CLI is 0.3.0. If any other version is installed, uninstall the plug-in that is installed and install the current {{site.data.keyword.logs_full_notm}} CLI plug-in.
{: important}

Both `ibmcloud cloud-logs` and `ibmcloud logs` can be used to run {{site.data.keyword.logs_full_notm}} CLI commands.
{: tip}

| Command | Description |
|---------|-------------|
| `alert` | Get an alert by ID. |
| `alert-create` | Create an alert. |
| `alert-delete` | Delete an alert. |
| `alert-update` | Update an alert. |
| `alerts` | List alerts. |
{: caption="{{site.data.keyword.logs_full_notm}} alert CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `alert-definition` | Get an alert definition by ID. |
| `alert-definition-create` | Create an alert definition. |
| `alert-definition-delete` | Delete an alert definition by ID. |
| `alert-definition-update` | Update an alert definition by ID. |
| `alert-definitions` | List alert definitions. |
{: caption="{{site.data.keyword.logs_full_notm}} alert definition CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `background-query-cancel`, `bgq-cancel` | Cancel a background query. |
| `background-query-create`, `bgq-create` | Submit a background query to be processed asynchronously. |
| `background-query-data`, `bgq-data` | Data of the background query to search the logs. |
| `background-query-status`, `bgq-status` | Get the status of a background query. |
{: caption="{{site.data.keyword.logs_full_notm}} background query (asynchronous archive query) CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `data-access-rule-create` | Create a data access rule. |
| `data-access-rule-delete` | Delete a data access rule. |
| `data-access-rule-update` | Update a data access rule. |
| `data-access-rules` | Get a service instance's data access rules by ID. |
{: caption="{{site.data.keyword.logs_full_notm}} data access rule CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `data-usage` | Get the daily and detailed data usage. |
| `data-usage-metrics-export-status` | Get the data usage metrics export status. |
| `data-usage-metrics-export-status-update` | Update the data usage metrics export status. |
{: caption="{{site.data.keyword.logs_full_notm}} data usage CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `enrichment-create` | Create an enrichment. |
| `enrichment-delete` | Delete enrichments. |
| `enrichments` | List all enrichments. |
{: caption="{{site.data.keyword.logs_full_notm}} enrichment CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `event-stream-target-create` | Create an {{site.data.keyword.messagehub_full_notm}} integration. |
| `event-stream-target-delete` | Delete an {{site.data.keyword.messagehub}} integration by ID. |
| `event-stream-target-update` | Update an {{site.data.keyword.messagehub}} integration. |
| `event-stream-targets` | List all {{site.data.keyword.messagehub}} integrations.
{: caption="{{site.data.keyword.logs_full_notm}} {{site.data.keyword.messagehub}} integration CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `events2metrics`, `e2m` | Gets the events to metrics definitions by ID. |
| `events2metrics-create`, `e2m-create` | Creates the events to metrics definitions. |
| `events2metrics-delete`, `e2m-delete` | Deletes the events to metrics definitions by ID. |
| `events2metrics-list`, `e2m-list` | Lists the events to metrics definitions. |
| `events2metrics-update`, `e2m-update` | Updates the events to metrics definitions. |
{: caption="{{site.data.keyword.logs_full_notm}} events to metrics CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `outgoing-webhook` | Gets an outbound integration by ID. |
| `outgoing-webhook-create` | Create an outbound integration. |
| `outgoing-webhook-delete` | Delete an outbound integration. |
| `outgoing-webhook-update` | Update an outbound integration. |
| `outgoing-webhooks` | List outbound integrations. |
{: caption="{{site.data.keyword.logs_full_notm}} outbound integration CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `policies` | Gets policies. |
| `policy` | Gets a policy by ID. |
| `policy-create` | Creates a new policy. |
| `policy-delete` | Deletes an existing policy. |
| `policy-update` | Updates an existing policy. |
{: caption="{{site.data.keyword.logs_full_notm}} policy CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `query` | Run a query to search the logs. |
{: caption="{{site.data.keyword.logs_full_notm}} query CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `rule-group` | Gets a rule group by groupid. |
| `rule-group-create` | Creates a rule group. |
| `rule-group-delete` | Deletes a rule group by groupid. |
| `rule-group-update` | Updates a rule group by groupid. |
| `rule-groups` | Gets all rule groups. |
{: caption="{{site.data.keyword.logs_full_notm}} rules CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `view` | Gets a view by ID. |
| `view-create` | Creates a new view. |
| `view-delete` | Deletes a view by ID. |
| `view-update` | Replaces an existing view. |
| `views` | Lists all public views. |
{: caption="{{site.data.keyword.logs_full_notm}} view CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `view-folder` | Get a view folder. |
| `view-folder-create` | Create a view folder. |
| `view-folder-delete` | Deletes a view folder by ID. |
| `view-folder-update` | Replaces an existing view folder. |
| `view-folders` | List a view's folders. |
{: caption="{{site.data.keyword.logs_full_notm}} view folder CLI commands" caption-side="bottom"}

| Command | Description |
|---------|-------------|
| `config` | Control the persistent configuration. | 
| `help` | Show help information. |
{: caption="{{site.data.keyword.logs_full_notm}} additional CLI commands" caption-side="bottom"}

For more information about using these commands, log in to the {{site.data.keyword.cloud_notm}} and run `ibmcloud logs command_name -h`. For example, `ibmcloud logs views -h`.
