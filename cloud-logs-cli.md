---

copyright:
  years: 2026
lastupdated: "2026-04-28"

keywords: cloud logs api, cli, plugin

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_full_notm}} CLI
{: #cloud-logs-cli}

You can use the {{site.data.keyword.cloud_notm}} command-line interface (CLI) to manage your {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

## Prerequisites
{: #logs-cli-prereq}

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
2. [Install the {{site.data.keyword.logs_full_notm}} CLI Plugin](/docs/cloud-logs?topic=cloud-logs-cloud-logs-cli-ov#cloud-logs-cli-ov-install).
3. [Set the IBM Cloud Logs instance](/docs/cloud-logs?topic=cloud-logs-cloud-logs-cli-ov#cloud-logs-cli-ov-context) that you want to target with the CLI commands.



## Config
{: #cloud-logs-cli-config-command}

Global parameters can also be stored in persistent configuration so that they do not need to be manually specified each time the plug-in is invoked. Each parameter can be configured with the `config` command and its subcommands.

```sh
ibmcloud cloud-logs config
```

### `ibmcloud cloud-logs config set`
{: #cloud-logs-cli-config-set-command}

Set a new config value for a specific option. Each subcommand of the `set` command maps to a global option. Each subcommand accepts a single argument, the string representation of the value to store for the option.

```sh
ibmcloud cloud-logs config set <option> <value>
```

#### Examples
{: #cloud-logs-config-set-command-examples}

```sh
ibmcloud cloud-logs config set service-url \
    'https://cloud.ibm.com/my-api'
```
{: pre}

### `ibmcloud cloud-logs config get`
{: #cloud-logs-cli-config-get-command}

Print out the currently set value for a specific option. Each subcommand of the `get` command maps to a global option.

```sh
ibmcloud cloud-logs config get <option>
```

#### Examples
{: #cloud-logs-config-get-command-examples}

```sh
ibmcloud cloud-logs config get service-url
```
{: pre}

### `ibmcloud cloud-logs config unset`
{: #cloud-logs-cli-config-unset-command}

Unset the currently set value for a specific option. Each subcommand of the `unset` command maps to a global option.

The subcommands available for this service are: `service-url`, .

```sh
ibmcloud cloud-logs config unset <option>
```

#### Examples
{: #cloud-logs-config-unset-command-examples}

```sh
ibmcloud cloud-logs config unset service-url
```
{: pre}

### `ibmcloud cloud-logs config list`
{: #cloud-logs-cli-config-list-command}

List out all of the currently set config values.

```sh
ibmcloud cloud-logs config list
```

#### Examples
{: #cloud-logs-config-list-command-examples}

```sh
ibmcloud cloud-logs config list
```
{: pre}

## Alert Definitions
{: #cloud-logs-alert-definitions-cli}

Create and manage alert definitions.

### `ibmcloud cloud-logs alert-definition`
{: #cloud-logs-cli-command}

Get details of an existing alert by using the alert ID.

```sh
ibmcloud cloud-logs alert-definition --id ID
```


#### Command options
{: #cloud-logs-cli-options}

`--id` (strfmt.UUID)
:   Alert definition ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-examples}

```sh
ibmcloud cloud-logs alert-definition \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

#### Default JMESPath
{: #cloud-logs-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,Created_Time:created_time}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,Created_Time:created_time}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,Created_Time:created_time}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs alert-definition-update`
{: #cloud-logs-cli-alert-definition-update-command}

Update an alert definition.

```sh
ibmcloud cloud-logs alert-definition-update --id ID [--prototype PROTOTYPE | --name NAME --description DESCRIPTION --enabled=ENABLED --priority PRIORITY --active-on ACTIVE-ON --type TYPE --group-by-keys GROUP-BY-KEYS --incidents-settings INCIDENTS-SETTINGS --notification-group NOTIFICATION-GROUP --entity-labels ENTITY-LABELS --phantom-mode=PHANTOM-MODE --deleted=DELETED --logs-immediate LOGS-IMMEDIATE --logs-threshold LOGS-THRESHOLD --logs-ratio-threshold LOGS-RATIO-THRESHOLD --logs-time-relative-threshold LOGS-TIME-RELATIVE-THRESHOLD --metric-threshold METRIC-THRESHOLD --flow FLOW --logs-anomaly LOGS-ANOMALY --metric-anomaly METRIC-ANOMALY --logs-new-value LOGS-NEW-VALUE --logs-unique-count LOGS-UNIQUE-COUNT]
```


#### Command options
{: #cloud-logs-alert-definition-update-cli-options}

`--id` (strfmt.UUID)
:   Alert definition ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--prototype` ([`AlertDefinitionPrototype`](#cli-prototype-example-schema))
:   Request model to create or update an alert. Only one alert type configuration is allowed and must be the same as in `type` field. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--name` (string)
:   The name of the alert definition. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--description` (string)
:   A detailed description of what the alert monitors and when it triggers. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--enabled` (bool)
:   Whether the alert is currently active and monitoring. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

`--priority` (string)
:   The priority of the alert definition. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `p5_or_unspecified`, `p4`, `p3`, `p2`, `p1`.

`--active-on` ([`ApisAlertDefinitionActivitySchedule`](#cli-apis-activity-schedule-example-schema))
:   Defining when the alert is active. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-on=@path/to/file.json`.

`--type` (string)
:   Alert type. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `logs_immediate_or_unspecified`, `logs_threshold`, `logs_anomaly`, `logs_ratio_threshold`, `logs_new_value`, `logs_unique_count`, `logs_time_relative_threshold`, `metric_threshold`, `metric_anomaly`, `flow`.

`--group-by-keys` ([]string)
:   Keys used to group and aggregate alert data. Not supported for `logs_new_value` alert type. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The list items must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`. The maximum length is `2` items. The minimum length is `0` items.

`--incidents-settings` ([`ApisAlertDefinitionAlertDefIncidentSettings`](#cli-apis-alert-def-incident-settings-example-schema))
:   Incident creation and management settings. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--incidents-settings=@path/to/file.json`.

`--notification-group` ([`ApisAlertDefinitionAlertDefNotificationGroup`](#cli-apis-alert-def-notification-group-example-schema))
:   Primary notification group for alert events. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--notification-group=@path/to/file.json`.

`--entity-labels` (map[string]string)
:   Labels used to identify and categorize the alert entity. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--entity-labels=@path/to/file.json`.

`--phantom-mode` (bool)
:   Whether the alert is in phantom mode (creating incidents or not) Phantom alerts serve as building blocks for flow alerts without triggering independent notifications.  Enabling this will remove the 'Notifications' section from the alert definition. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

`--deleted` (bool)
:   Whether the alert has been marked as deleted. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

`--logs-immediate` ([`ApisAlertDefinitionLogsImmediateType`](#cli-apis-logs-immediate-type-example-schema))
:   Configuration for immediate log-based alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-immediate=@path/to/file.json`.

`--logs-threshold` ([`ApisAlertDefinitionLogsThresholdType`](#cli-apis-logs-threshold-type-example-schema))
:   Configuration for the log-based threshold alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-threshold=@path/to/file.json`.

`--logs-ratio-threshold` ([`ApisAlertDefinitionLogsRatioThresholdType`](#cli-apis-logs-ratio-threshold-type-example-schema))
:   Configuration for the log-based ratio threshold alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-ratio-threshold=@path/to/file.json`.

`--logs-time-relative-threshold` ([`ApisAlertDefinitionLogsTimeRelativeThresholdType`](#cli-apis-logs-time-relative-threshold-type-example-schema))
:   Configuration for time-relative log threshold alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-time-relative-threshold=@path/to/file.json`.

`--metric-threshold` ([`ApisAlertDefinitionMetricThresholdType`](#cli-apis-metric-threshold-type-example-schema))
:   Configuration for metric-based threshold alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--metric-threshold=@path/to/file.json`.

`--flow` ([`ApisAlertDefinitionFlowType`](#cli-apis-flow-type-example-schema))
:   Configuration for flow alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--flow=@path/to/file.json`.

`--logs-anomaly` ([`ApisAlertDefinitionLogsAnomalyType`](#cli-apis-logs-anomaly-type-example-schema))
:   Configuration for the log-based anomaly detection alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-anomaly=@path/to/file.json`.

`--metric-anomaly` ([`ApisAlertDefinitionMetricAnomalyType`](#cli-apis-metric-anomaly-type-example-schema))
:   Configuration for metric-based anomaly detection alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--metric-anomaly=@path/to/file.json`.

`--logs-new-value` ([`ApisAlertDefinitionLogsNewValueType`](#cli-apis-logs-new-value-type-example-schema))
:   Configuration for alerts triggered by new log values. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-new-value=@path/to/file.json`.

`--logs-unique-count` ([`ApisAlertDefinitionLogsUniqueCountType`](#cli-apis-logs-unique-count-type-example-schema))
:   Configuration for alerts based on unique log value counts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-unique-count=@path/to/file.json`.

#### Examples
{: #cloud-logs-alert-definition-update-examples}

```sh
ibmcloud cloud-logs alert-definition-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --prototype '{"name": "Alert 1738141279354", "description": "Example Alert definition", "enabled": true, "priority": "p5_or_unspecified", "active_on": {"day_of_week": ["monday_or_unspecified","tuesday","wednesday","thursday","friday","saturday","sunday"], "start_time": {"hours": 22, "minutes": 30}, "end_time": {"hours": 22, "minutes": 30}}, "type": "logs_threshold", "group_by_keys": [], "incidents_settings": {"notify_on": "triggered_only_unspecified", "minutes": 10}, "notification_group": {"group_by_keys": [], "webhooks": [{"notify_on": "triggered_and_resolved", "integration": {"integration_id": 123}, "minutes": 15}]}, "entity_labels": {}, "phantom_mode": false, "deleted": false, "logs_threshold": {"logs_filter": {"simple_filter": {"lucene_query": "text:\"error\"", "label_filters": {"application_name": [{"value": "my-app", "operation": "starts_with"}], "subsystem_name": [{"value": "my-app", "operation": "starts_with"}], "severities": ["verbose_unspecified","debug","info","warning","error","critical"]}}}, "undetected_values_management": {"trigger_undetected_values": true, "auto_retire_timeframe": "hours_24"}, "rules": [{"condition": {"threshold": 1, "time_window": {"logs_time_window_specific_value": "minutes_10"}}, "override": {"priority": "p5_or_unspecified"}}], "condition_type": "more_than_or_unspecified", "notification_payload_filter": [], "evaluation_delay_ms": 60000}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs alert-definition-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'Unique count alert' \
    --description 'Example of unique count alert from terraform' \
    --enabled=true \
    --priority p1 \
    --active-on apisAlertDefinitionActivitySchedule \
    --type flow \
    --group-by-keys key1,key2 \
    --incidents-settings apisAlertDefinitionAlertDefIncidentSettings \
    --notification-group apisAlertDefinitionAlertDefNotificationGroup \
    --entity-labels '{}' \
    --phantom-mode=false \
    --deleted=false \
    --logs-threshold apisAlertDefinitionLogsThresholdType
```
{: pre}

#### Default JMESPath
{: #cloud-logs-alert-definition-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,UpdatedTime:updated_time}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,UpdatedTime:updated_time}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,UpdatedTime:updated_time}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs alert-definition-delete`
{: #cloud-logs-cli-alert-definition-delete-command}

Delete an alert definition.

```sh
ibmcloud cloud-logs alert-definition-delete --id ID
```


#### Command options
{: #cloud-logs-alert-definition-delete-cli-options}

`--id` (strfmt.UUID)
:   Alert definition ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-alert-definition-delete-examples}

```sh
ibmcloud cloud-logs alert-definition-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs alert-definitions`
{: #cloud-logs-cli-alert-definitions-command}

List alert definitions.

```sh
ibmcloud cloud-logs alert-definitions
```


#### Example
{: #cloud-logs-alert-definitions-examples}

```sh
ibmcloud cloud-logs alert-definitions
```
{: pre}

#### Default JMESPath
{: #cloud-logs-alert-definitions-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `alert_definitions[*].{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,Created_Time:created_time}` |
| Error | Default | - |
|  | Table | `alert_definitions[*].{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,Created_Time:created_time}` |
| All pages | Default | - |
|  | Table | `alert_definitions[*].{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,Created_Time:created_time}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs alert-definition-create`
{: #cloud-logs-cli-alert-definition-create-command}

Create an alert definition.

```sh
ibmcloud cloud-logs alert-definition-create [--prototype PROTOTYPE | --name NAME --description DESCRIPTION --enabled=ENABLED --priority PRIORITY --active-on ACTIVE-ON --type TYPE --group-by-keys GROUP-BY-KEYS --incidents-settings INCIDENTS-SETTINGS --notification-group NOTIFICATION-GROUP --entity-labels ENTITY-LABELS --phantom-mode=PHANTOM-MODE --deleted=DELETED --logs-immediate LOGS-IMMEDIATE --logs-threshold LOGS-THRESHOLD --logs-ratio-threshold LOGS-RATIO-THRESHOLD --logs-time-relative-threshold LOGS-TIME-RELATIVE-THRESHOLD --metric-threshold METRIC-THRESHOLD --flow FLOW --logs-anomaly LOGS-ANOMALY --metric-anomaly METRIC-ANOMALY --logs-new-value LOGS-NEW-VALUE --logs-unique-count LOGS-UNIQUE-COUNT]
```


#### Command options
{: #cloud-logs-alert-definition-create-cli-options}

`--prototype` ([`AlertDefinitionPrototype`](#cli-prototype-example-schema))
:   Request model to create or update an alert. Only one alert type configuration is allowed and must be the same as in `type` field. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--name` (string)
:   The name of the alert definition. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--description` (string)
:   A detailed description of what the alert monitors and when it triggers. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--enabled` (bool)
:   Whether the alert is currently active and monitoring. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

`--priority` (string)
:   The priority of the alert definition. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `p5_or_unspecified`, `p4`, `p3`, `p2`, `p1`.

`--active-on` ([`ApisAlertDefinitionActivitySchedule`](#cli-apis-activity-schedule-example-schema))
:   Defining when the alert is active. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-on=@path/to/file.json`.

`--type` (string)
:   Alert type. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `logs_immediate_or_unspecified`, `logs_threshold`, `logs_anomaly`, `logs_ratio_threshold`, `logs_new_value`, `logs_unique_count`, `logs_time_relative_threshold`, `metric_threshold`, `metric_anomaly`, `flow`.

`--group-by-keys` ([]string)
:   Keys used to group and aggregate alert data. Not supported for `logs_new_value` alert type. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The list items must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`. The maximum length is `2` items. The minimum length is `0` items.

`--incidents-settings` ([`ApisAlertDefinitionAlertDefIncidentSettings`](#cli-apis-alert-def-incident-settings-example-schema))
:   Incident creation and management settings. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--incidents-settings=@path/to/file.json`.

`--notification-group` ([`ApisAlertDefinitionAlertDefNotificationGroup`](#cli-apis-alert-def-notification-group-example-schema))
:   Primary notification group for alert events. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--notification-group=@path/to/file.json`.

`--entity-labels` (map[string]string)
:   Labels used to identify and categorize the alert entity. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--entity-labels=@path/to/file.json`.

`--phantom-mode` (bool)
:   Whether the alert is in phantom mode (creating incidents or not) Phantom alerts serve as building blocks for flow alerts without triggering independent notifications.  Enabling this will remove the 'Notifications' section from the alert definition. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

`--deleted` (bool)
:   Whether the alert has been marked as deleted. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

`--logs-immediate` ([`ApisAlertDefinitionLogsImmediateType`](#cli-apis-logs-immediate-type-example-schema))
:   Configuration for immediate log-based alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-immediate=@path/to/file.json`.

`--logs-threshold` ([`ApisAlertDefinitionLogsThresholdType`](#cli-apis-logs-threshold-type-example-schema))
:   Configuration for the log-based threshold alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-threshold=@path/to/file.json`.

`--logs-ratio-threshold` ([`ApisAlertDefinitionLogsRatioThresholdType`](#cli-apis-logs-ratio-threshold-type-example-schema))
:   Configuration for the log-based ratio threshold alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-ratio-threshold=@path/to/file.json`.

`--logs-time-relative-threshold` ([`ApisAlertDefinitionLogsTimeRelativeThresholdType`](#cli-apis-logs-time-relative-threshold-type-example-schema))
:   Configuration for time-relative log threshold alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-time-relative-threshold=@path/to/file.json`.

`--metric-threshold` ([`ApisAlertDefinitionMetricThresholdType`](#cli-apis-metric-threshold-type-example-schema))
:   Configuration for metric-based threshold alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--metric-threshold=@path/to/file.json`.

`--flow` ([`ApisAlertDefinitionFlowType`](#cli-apis-flow-type-example-schema))
:   Configuration for flow alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--flow=@path/to/file.json`.

`--logs-anomaly` ([`ApisAlertDefinitionLogsAnomalyType`](#cli-apis-logs-anomaly-type-example-schema))
:   Configuration for the log-based anomaly detection alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-anomaly=@path/to/file.json`.

`--metric-anomaly` ([`ApisAlertDefinitionMetricAnomalyType`](#cli-apis-metric-anomaly-type-example-schema))
:   Configuration for metric-based anomaly detection alerts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--metric-anomaly=@path/to/file.json`.

`--logs-new-value` ([`ApisAlertDefinitionLogsNewValueType`](#cli-apis-logs-new-value-type-example-schema))
:   Configuration for alerts triggered by new log values. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-new-value=@path/to/file.json`.

`--logs-unique-count` ([`ApisAlertDefinitionLogsUniqueCountType`](#cli-apis-logs-unique-count-type-example-schema))
:   Configuration for alerts based on unique log value counts. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--logs-unique-count=@path/to/file.json`.

#### Examples
{: #cloud-logs-alert-definition-create-examples}

```sh
ibmcloud cloud-logs alert-definition-create \
    --prototype '{"name": "Alert 1738141279354", "description": "Example Alert definition", "enabled": true, "priority": "p5_or_unspecified", "active_on": {"day_of_week": ["monday_or_unspecified","tuesday","wednesday","thursday","friday","saturday","sunday"], "start_time": {"hours": 22, "minutes": 30}, "end_time": {"hours": 22, "minutes": 30}}, "type": "logs_threshold", "group_by_keys": [], "incidents_settings": {"notify_on": "triggered_only_unspecified", "minutes": 10}, "notification_group": {"group_by_keys": [], "webhooks": [{"notify_on": "triggered_and_resolved", "integration": {"integration_id": 123}, "minutes": 15}]}, "entity_labels": {}, "phantom_mode": false, "deleted": false, "logs_threshold": {"logs_filter": {"simple_filter": {"lucene_query": "text:\"error\"", "label_filters": {"application_name": [{"value": "my-app", "operation": "starts_with"}], "subsystem_name": [{"value": "my-app", "operation": "starts_with"}], "severities": ["verbose_unspecified","debug","info","warning","error","critical"]}}}, "undetected_values_management": {"trigger_undetected_values": true, "auto_retire_timeframe": "hours_24"}, "rules": [{"condition": {"threshold": 1, "time_window": {"logs_time_window_specific_value": "minutes_10"}}, "override": {"priority": "p5_or_unspecified"}}], "condition_type": "more_than_or_unspecified", "notification_payload_filter": [], "evaluation_delay_ms": 60000}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs alert-definition-create \
    --name 'Unique count alert' \
    --description 'Example of unique count alert from terraform' \
    --enabled=true \
    --priority p1 \
    --active-on apisAlertDefinitionActivitySchedule \
    --type flow \
    --group-by-keys key1,key2 \
    --incidents-settings apisAlertDefinitionAlertDefIncidentSettings \
    --notification-group apisAlertDefinitionAlertDefNotificationGroup \
    --entity-labels '{}' \
    --phantom-mode=false \
    --deleted=false \
    --logs-threshold apisAlertDefinitionLogsThresholdType
```
{: pre}

#### Default JMESPath
{: #cloud-logs-alert-definition-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,Created_Time:created_time}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,Created_Time:created_time}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Priority:priority,Type:type,Created_Time:created_time}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

## Alerts
{: #cloud-logs-alerts-cli}

Create and manage alerts.

### `ibmcloud cloud-logs alert`
{: #cloud-logs-cli-alert-command}

Get an alert by ID.

```sh
ibmcloud cloud-logs alert --id ID
```


#### Command options
{: #cloud-logs-alert-cli-options}

`--id` (strfmt.UUID)
:   Alert ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-alert-examples}

```sh
ibmcloud cloud-logs alert \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

#### Default JMESPath
{: #cloud-logs-alert-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs alert-update`
{: #cloud-logs-cli-alert-update-command}

Update an alert.

```sh
ibmcloud cloud-logs alert-update --id ID --name NAME --is-active=IS-ACTIVE --severity SEVERITY [--condition CONDITION | --condition-immediate CONDITION-IMMEDIATE --condition-less-than CONDITION-LESS-THAN --condition-more-than CONDITION-MORE-THAN --condition-more-than-usual CONDITION-MORE-THAN-USUAL --condition-new-value CONDITION-NEW-VALUE --condition-flow CONDITION-FLOW --condition-unique-count CONDITION-UNIQUE-COUNT --condition-less-than-usual CONDITION-LESS-THAN-USUAL] [--description DESCRIPTION] [--expiration EXPIRATION | --expiration-year EXPIRATION-YEAR --expiration-month EXPIRATION-MONTH --expiration-day EXPIRATION-DAY] [--notification-groups NOTIFICATION-GROUPS] [--filters FILTERS | --filters-severities FILTERS-SEVERITIES --filters-metadata FILTERS-METADATA --filters-alias FILTERS-ALIAS --filters-text FILTERS-TEXT --filters-ratio-alerts FILTERS-RATIO-ALERTS --filters-filter-type FILTERS-FILTER-TYPE] [--active-when ACTIVE-WHEN | --active-when-timeframes ACTIVE-WHEN-TIMEFRAMES] [--notification-payload-filters NOTIFICATION-PAYLOAD-FILTERS] [--meta-labels META-LABELS] [--meta-labels-strings META-LABELS-STRINGS] [--incident-settings INCIDENT-SETTINGS | --incident-settings-retriggering-period-seconds INCIDENT-SETTINGS-RETRIGGERING-PERIOD-SECONDS --incident-settings-notify-on INCIDENT-SETTINGS-NOTIFY-ON --incident-settings-use-as-notification-settings=INCIDENT-SETTINGS-USE-AS-NOTIFICATION-SETTINGS]
```


#### Command options
{: #cloud-logs-alert-update-cli-options}

`--id` (strfmt.UUID)
:   Alert ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--name` (string)
:   Alert name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--is-active` (bool)
:   Alert is active. Required.

`--severity` (string)
:   Alert severity. Required.

    Allowable values are: `info_or_unspecified`, `warning`, `critical`, `error`.

`--condition` ([`AlertsV2AlertCondition`](#cli-alerts-v2-alert-condition-example-schema))
:   Alert condition. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition=@path/to/file.json`.

`--description` (string)
:   Alert description.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}0-9_\\-\\s]+$/`.

`--expiration` ([`AlertsV1Date`](#cli-alerts-v1-date-example-schema))
:   Alert expiration date. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--expiration=@path/to/file.json`.

`--notification-groups` ([`AlertsV2AlertNotificationGroups[]`](#cli-alerts-v2-alert-notification-groups-example-schema))
:   Alert notification groups.

    The maximum length is `10` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--notification-groups=@path/to/file.json`.

`--filters` ([`AlertsV1AlertFilters`](#cli-alerts-v1-alert-filters-example-schema))
:   Alert filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--active-when` ([`AlertsV1AlertActiveWhen`](#cli-alerts-v1-alert-active-when-example-schema))
:   When will the alert be active. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when=@path/to/file.json`.

`--notification-payload-filters` ([]string)
:   The JSON keys to be included in the alert notification. If unspecified, the full log text will be included in the alert notification.

    The list items must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`. The maximum length is `100` items. The minimum length is `0` items.

`--meta-labels` ([`AlertsV1MetaLabel[]`](#cli-alerts-v1-meta-label-example-schema))
:   The Meta labels to add to the alert.

    The maximum length is `200` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--meta-labels=@path/to/file.json`.

`--meta-labels-strings` ([]string)
:   The meta data added to the alert as a string separated by a ":" character.

    The list items must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`. The maximum length is `4096` items. The minimum length is `0` items.

`--incident-settings` ([`AlertsV2AlertIncidentSettings`](#cli-alerts-v2-alert-incident-settings-example-schema))
:   Incident settings, will create the incident based on this configuration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--incident-settings=@path/to/file.json`.

`--condition-immediate` ([`AlertsV2ImmediateConditionEmpty`](#cli-alerts-v2-immediate-condition-empty-example-schema))
:   Condition for immediate standard alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-immediate=@path/to/file.json`.

`--condition-less-than` ([`AlertsV2LessThanCondition`](#cli-alerts-v2-less-than-condition-example-schema))
:   Condition for less than alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-less-than=@path/to/file.json`.

`--condition-more-than` ([`AlertsV2MoreThanCondition`](#cli-alerts-v2-more-than-condition-example-schema))
:   Condition for more than alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-more-than=@path/to/file.json`.

`--condition-more-than-usual` ([`AlertsV2MoreThanUsualCondition`](#cli-alerts-v2-more-than-usual-condition-example-schema))
:   Condition for more than usual alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-more-than-usual=@path/to/file.json`.

`--condition-new-value` ([`AlertsV2NewValueCondition`](#cli-alerts-v2-new-value-condition-example-schema))
:   Condition for new value alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-new-value=@path/to/file.json`.

`--condition-flow` ([`AlertsV2FlowCondition`](#cli-alerts-v2-flow-condition-example-schema))
:   Condition for flow alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-flow=@path/to/file.json`.

`--condition-unique-count` ([`AlertsV2UniqueCountCondition`](#cli-alerts-v2-unique-count-condition-example-schema))
:   Condition for unique count alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-unique-count=@path/to/file.json`.

`--condition-less-than-usual` ([`AlertsV2LessThanUsualCondition`](#cli-alerts-v2-less-than-usual-condition-example-schema))
:   Condition for less than usual alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-less-than-usual=@path/to/file.json`.

`--expiration-year` (int64)
:   Year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

    The maximum value is `2147483647`. The minimum value is `0`.

`--expiration-month` (int64)
:   Month of the year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

    The maximum value is `12`. The minimum value is `1`.

`--expiration-day` (int64)
:   Day of the month. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

    The maximum value is `31`. The minimum value is `1`.

`--filters-severities` ([]string)
:   The severity of the logs to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable list items are: `debug_or_unspecified`, `verbose`, `info`, `warning`, `error`, `critical`. The maximum length is `4096` items. The minimum length is `0` items.

`--filters-metadata` ([`AlertsV1AlertFiltersMetadataFilters`](#cli-alerts-v1-alert-filters-metadata-filters-example-schema))
:   The metadata filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-metadata=@path/to/file.json`.

`--filters-alias` (string)
:   The alias of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--filters-text` (string)
:   The text to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--filters-ratio-alerts` ([`AlertsV1AlertFiltersRatioAlert[]`](#cli-alerts-v1-alert-filters-ratio-alert-example-schema))
:   The ratio alerts. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-ratio-alerts=@path/to/file.json`.

`--filters-filter-type` (string)
:   The type of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable values are: `text_or_unspecified`, `template`, `ratio`, `unique_count`, `time_relative`, `metric`, `flow`.

`--active-when-timeframes` ([`AlertsV1AlertActiveTimeframe[]`](#cli-alerts-v1-alert-active-timeframe-example-schema))
:   Activity timeframes of the alert. This option provides a value for a sub-field of the JSON option 'active-when'. It is mutually exclusive with that option.

    The maximum length is `30` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when-timeframes=@path/to/file.json`.

`--incident-settings-retriggering-period-seconds` (int64)
:   The retriggering period of the alert in seconds. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

    The maximum value is `4294967295`. The minimum value is `0`.

`--incident-settings-notify-on` (string)
:   Notify on setting. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

    Allowable values are: `triggered_only`, `triggered_and_resolved`.

`--incident-settings-use-as-notification-settings` (bool)
:   Use these settings for all notificaion webhook. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

#### Examples
{: #cloud-logs-alert-update-examples}

```sh
ibmcloud cloud-logs alert-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'Test alert' \
    --is-active=true \
    --severity info_or_unspecified \
    --condition '{"more_than": {"parameters": {"threshold": 1, "timeframe": "timeframe_10_min", "group_by": ["coralogix.metadata.applicationName"], "metric_alert_parameters": {"metric_field": "cpu_usage", "metric_source": "prometheus", "arithmetic_operator": "percentile", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "metric_alert_promql_parameters": {"promql_text": "sum(rate(container_cpu_usage_seconds_total{container_name=\"my-container\"}[5m])) by (pod_name)", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "ignore_infinity": true, "relative_timeframe": "hour_or_unspecified", "cardinality_fields": [], "related_extended_data": {"cleanup_deadman_duration": "cleanup_deadman_duration_24h", "should_trigger_deadman": true}}, "evaluation_window": "rolling_or_unspecified"}}' \
    --description 'Alert when the number of logs reaches a threshold.' \
    --expiration '{"year": 2012, "month": 12, "day": 24}' \
    --notification-groups '[{"group_by_fields": ["coralogix.metadata.applicationName"], "notifications": [{"retriggering_period_seconds": 60, "notify_on": "triggered_and_resolved", "integration_id": 123}]}]' \
    --filters '{"severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "metadata": {"applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"]}, "alias": "monitorQuery", "text": "initiator.id.keyword:iam-ServiceId-10820fd6-c3fe-414e-8fd5-44ce95f7d34d AND action.keyword:cloud-object-storage.object.create", "ratio_alerts": [{"alias": "TopLevelAlert", "text": "_exists_:\"container_name\"", "severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"], "group_by": ["Host","Thread"]}], "filter_type": "text_or_unspecified"}' \
    --active-when '{"timeframes": [{"days_of_week": ["monday_or_unspecified","tuesday","wednesday","thursday","friday","saturday","sunday"], "range": {"start": {"hours": 18, "minutes": 30, "seconds": 0}, "end": {"hours": 18, "minutes": 30, "seconds": 0}}}]}' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[{"key": "env", "value": "dev"}]' \
    --meta-labels-strings '[]' \
    --incident-settings '{"retriggering_period_seconds": 300, "notify_on": "triggered_only", "use_as_notification_settings": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:

```sh
ibmcloud cloud-logs alert-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'Test alert' \
    --is-active=true \
    --severity info_or_unspecified \
    --description 'Alert when the number of logs reaches a threshold.' \
    --notification-groups '[alertsV2AlertNotificationGroups]' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[alertsV1MetaLabel]' \
    --meta-labels-strings '[]' \
    --condition-more-than alertsV2MoreThanCondition \
    --expiration-year 2012 \
    --expiration-month 12 \
    --expiration-day 24 \
    --filters-severities debug_or_unspecified,verbose,info,warning,error,critical \
    --filters-metadata alertsV1AlertFiltersMetadataFilters \
    --filters-alias monitorQuery \
    --filters-text _exists_:"container_name" \
    --filters-ratio-alerts '[alertsV1AlertFiltersRatioAlert]' \
    --filters-filter-type flow \
    --active-when-timeframes '[alertsV1AlertActiveTimeframe]' \
    --incident-settings-retriggering-period-seconds 60 \
    --incident-settings-notify-on triggered_and_resolved \
    --incident-settings-use-as-notification-settings=true
```
{: pre}

#### Default JMESPath
{: #cloud-logs-alert-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs alert-delete`
{: #cloud-logs-cli-alert-delete-command}

Delete an alert.

```sh
ibmcloud cloud-logs alert-delete --id ID
```


#### Command options
{: #cloud-logs-alert-delete-cli-options}

`--id` (strfmt.UUID)
:   Alert ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-alert-delete-examples}

```sh
ibmcloud cloud-logs alert-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs alerts`
{: #cloud-logs-cli-alerts-command}

List alerts.

```sh
ibmcloud cloud-logs alerts
```


#### Example
{: #cloud-logs-alerts-examples}

```sh
ibmcloud cloud-logs alerts
```
{: pre}

#### Default JMESPath
{: #cloud-logs-alerts-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `alerts[*].{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
| Error | Default | - |
|  | Table | `alerts[*].{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
| All pages | Default | - |
|  | Table | `alerts[*].{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs alert-create`
{: #cloud-logs-cli-alert-create-command}

Create an alert.

```sh
ibmcloud cloud-logs alert-create --name NAME --is-active=IS-ACTIVE --severity SEVERITY [--condition CONDITION | --condition-immediate CONDITION-IMMEDIATE --condition-less-than CONDITION-LESS-THAN --condition-more-than CONDITION-MORE-THAN --condition-more-than-usual CONDITION-MORE-THAN-USUAL --condition-new-value CONDITION-NEW-VALUE --condition-flow CONDITION-FLOW --condition-unique-count CONDITION-UNIQUE-COUNT --condition-less-than-usual CONDITION-LESS-THAN-USUAL] [--description DESCRIPTION] [--expiration EXPIRATION | --expiration-year EXPIRATION-YEAR --expiration-month EXPIRATION-MONTH --expiration-day EXPIRATION-DAY] [--notification-groups NOTIFICATION-GROUPS] [--filters FILTERS | --filters-severities FILTERS-SEVERITIES --filters-metadata FILTERS-METADATA --filters-alias FILTERS-ALIAS --filters-text FILTERS-TEXT --filters-ratio-alerts FILTERS-RATIO-ALERTS --filters-filter-type FILTERS-FILTER-TYPE] [--active-when ACTIVE-WHEN | --active-when-timeframes ACTIVE-WHEN-TIMEFRAMES] [--notification-payload-filters NOTIFICATION-PAYLOAD-FILTERS] [--meta-labels META-LABELS] [--meta-labels-strings META-LABELS-STRINGS] [--incident-settings INCIDENT-SETTINGS | --incident-settings-retriggering-period-seconds INCIDENT-SETTINGS-RETRIGGERING-PERIOD-SECONDS --incident-settings-notify-on INCIDENT-SETTINGS-NOTIFY-ON --incident-settings-use-as-notification-settings=INCIDENT-SETTINGS-USE-AS-NOTIFICATION-SETTINGS]
```


#### Command options
{: #cloud-logs-alert-create-cli-options}

`--name` (string)
:   Alert name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--is-active` (bool)
:   Alert is active. Required.

`--severity` (string)
:   Alert severity. Required.

    Allowable values are: `info_or_unspecified`, `warning`, `critical`, `error`.

`--condition` ([`AlertsV2AlertCondition`](#cli-alerts-v2-alert-condition-example-schema))
:   Alert condition. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition=@path/to/file.json`.

`--description` (string)
:   Alert description.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}0-9_\\-\\s]+$/`.

`--expiration` ([`AlertsV1Date`](#cli-alerts-v1-date-example-schema))
:   Alert expiration date. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--expiration=@path/to/file.json`.

`--notification-groups` ([`AlertsV2AlertNotificationGroups[]`](#cli-alerts-v2-alert-notification-groups-example-schema))
:   Alert notification groups.

    The maximum length is `10` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--notification-groups=@path/to/file.json`.

`--filters` ([`AlertsV1AlertFilters`](#cli-alerts-v1-alert-filters-example-schema))
:   Alert filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--active-when` ([`AlertsV1AlertActiveWhen`](#cli-alerts-v1-alert-active-when-example-schema))
:   When will the alert be active. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when=@path/to/file.json`.

`--notification-payload-filters` ([]string)
:   The JSON keys to be included in the alert notification. If unspecified, the full log text will be included in the alert notification.

    The list items must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`. The maximum length is `100` items. The minimum length is `0` items.

`--meta-labels` ([`AlertsV1MetaLabel[]`](#cli-alerts-v1-meta-label-example-schema))
:   The Meta labels to add to the alert.

    The maximum length is `200` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--meta-labels=@path/to/file.json`.

`--meta-labels-strings` ([]string)
:   The meta data added to the alert as a string separated by a ":" character.

    The list items must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`. The maximum length is `4096` items. The minimum length is `0` items.

`--incident-settings` ([`AlertsV2AlertIncidentSettings`](#cli-alerts-v2-alert-incident-settings-example-schema))
:   Incident settings, will create the incident based on this configuration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--incident-settings=@path/to/file.json`.

`--condition-immediate` ([`AlertsV2ImmediateConditionEmpty`](#cli-alerts-v2-immediate-condition-empty-example-schema))
:   Condition for immediate standard alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-immediate=@path/to/file.json`.

`--condition-less-than` ([`AlertsV2LessThanCondition`](#cli-alerts-v2-less-than-condition-example-schema))
:   Condition for less than alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-less-than=@path/to/file.json`.

`--condition-more-than` ([`AlertsV2MoreThanCondition`](#cli-alerts-v2-more-than-condition-example-schema))
:   Condition for more than alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-more-than=@path/to/file.json`.

`--condition-more-than-usual` ([`AlertsV2MoreThanUsualCondition`](#cli-alerts-v2-more-than-usual-condition-example-schema))
:   Condition for more than usual alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-more-than-usual=@path/to/file.json`.

`--condition-new-value` ([`AlertsV2NewValueCondition`](#cli-alerts-v2-new-value-condition-example-schema))
:   Condition for new value alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-new-value=@path/to/file.json`.

`--condition-flow` ([`AlertsV2FlowCondition`](#cli-alerts-v2-flow-condition-example-schema))
:   Condition for flow alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-flow=@path/to/file.json`.

`--condition-unique-count` ([`AlertsV2UniqueCountCondition`](#cli-alerts-v2-unique-count-condition-example-schema))
:   Condition for unique count alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-unique-count=@path/to/file.json`.

`--condition-less-than-usual` ([`AlertsV2LessThanUsualCondition`](#cli-alerts-v2-less-than-usual-condition-example-schema))
:   Condition for less than usual alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-less-than-usual=@path/to/file.json`.

`--expiration-year` (int64)
:   Year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

    The maximum value is `2147483647`. The minimum value is `0`.

`--expiration-month` (int64)
:   Month of the year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

    The maximum value is `12`. The minimum value is `1`.

`--expiration-day` (int64)
:   Day of the month. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

    The maximum value is `31`. The minimum value is `1`.

`--filters-severities` ([]string)
:   The severity of the logs to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable list items are: `debug_or_unspecified`, `verbose`, `info`, `warning`, `error`, `critical`. The maximum length is `4096` items. The minimum length is `0` items.

`--filters-metadata` ([`AlertsV1AlertFiltersMetadataFilters`](#cli-alerts-v1-alert-filters-metadata-filters-example-schema))
:   The metadata filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-metadata=@path/to/file.json`.

`--filters-alias` (string)
:   The alias of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--filters-text` (string)
:   The text to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--filters-ratio-alerts` ([`AlertsV1AlertFiltersRatioAlert[]`](#cli-alerts-v1-alert-filters-ratio-alert-example-schema))
:   The ratio alerts. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-ratio-alerts=@path/to/file.json`.

`--filters-filter-type` (string)
:   The type of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable values are: `text_or_unspecified`, `template`, `ratio`, `unique_count`, `time_relative`, `metric`, `flow`.

`--active-when-timeframes` ([`AlertsV1AlertActiveTimeframe[]`](#cli-alerts-v1-alert-active-timeframe-example-schema))
:   Activity timeframes of the alert. This option provides a value for a sub-field of the JSON option 'active-when'. It is mutually exclusive with that option.

    The maximum length is `30` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when-timeframes=@path/to/file.json`.

`--incident-settings-retriggering-period-seconds` (int64)
:   The retriggering period of the alert in seconds. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

    The maximum value is `4294967295`. The minimum value is `0`.

`--incident-settings-notify-on` (string)
:   Notify on setting. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

    Allowable values are: `triggered_only`, `triggered_and_resolved`.

`--incident-settings-use-as-notification-settings` (bool)
:   Use these settings for all notificaion webhook. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

#### Examples
{: #cloud-logs-alert-create-examples}

```sh
ibmcloud cloud-logs alert-create \
    --name 'Test alert' \
    --is-active=true \
    --severity info_or_unspecified \
    --condition '{"more_than": {"parameters": {"threshold": 1, "timeframe": "timeframe_10_min", "group_by": ["coralogix.metadata.applicationName"], "metric_alert_parameters": {"metric_field": "cpu_usage", "metric_source": "prometheus", "arithmetic_operator": "percentile", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "metric_alert_promql_parameters": {"promql_text": "sum(rate(container_cpu_usage_seconds_total{container_name=\"my-container\"}[5m])) by (pod_name)", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "ignore_infinity": true, "relative_timeframe": "hour_or_unspecified", "cardinality_fields": [], "related_extended_data": {"cleanup_deadman_duration": "cleanup_deadman_duration_24h", "should_trigger_deadman": true}}, "evaluation_window": "rolling_or_unspecified"}}' \
    --description 'Alert when the number of logs reaches a threshold' \
    --expiration '{"year": 2012, "month": 12, "day": 24}' \
    --notification-groups '[{"group_by_fields": ["coralogix.metadata.applicationName"], "notifications": [{"retriggering_period_seconds": 60, "notify_on": "triggered_and_resolved", "integration_id": 123}]}]' \
    --filters '{"severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "metadata": {"applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"]}, "alias": "monitorQuery", "text": "initiator.id.keyword:iam-ServiceId-10820fd6-c3fe-414e-8fd5-44ce95f7d34d AND action.keyword:cloud-object-storage.object.create", "ratio_alerts": [{"alias": "TopLevelAlert", "text": "_exists_:\"container_name\"", "severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"], "group_by": ["Host","Thread"]}], "filter_type": "text_or_unspecified"}' \
    --active-when '{"timeframes": [{"days_of_week": ["monday_or_unspecified","tuesday","wednesday","thursday","friday","saturday","sunday"], "range": {"start": {"hours": 18, "minutes": 30, "seconds": 0}, "end": {"hours": 18, "minutes": 30, "seconds": 0}}}]}' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[{"key": "env", "value": "dev"}]' \
    --meta-labels-strings '[]' \
    --incident-settings '{"retriggering_period_seconds": 300, "notify_on": "triggered_only", "use_as_notification_settings": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs alert-create \
    --name 'Test alert' \
    --is-active=true \
    --severity info_or_unspecified \
    --description 'Alert when the number of logs reaches a threshold' \
    --notification-groups '[alertsV2AlertNotificationGroups]' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[alertsV1MetaLabel]' \
    --meta-labels-strings '[]' \
    --condition-more-than alertsV2MoreThanCondition \
    --expiration-year 2012 \
    --expiration-month 12 \
    --expiration-day 24 \
    --filters-severities debug_or_unspecified,verbose,info,warning,error,critical \
    --filters-metadata alertsV1AlertFiltersMetadataFilters \
    --filters-alias monitorQuery \
    --filters-text _exists_:"container_name" \
    --filters-ratio-alerts '[alertsV1AlertFiltersRatioAlert]' \
    --filters-filter-type flow \
    --active-when-timeframes '[alertsV1AlertActiveTimeframe]' \
    --incident-settings-retriggering-period-seconds 60 \
    --incident-settings-notify-on triggered_and_resolved \
    --incident-settings-use-as-notification-settings=true
```
{: pre}

#### Default JMESPath
{: #cloud-logs-alert-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Is_Active:is_active,Severity:severity}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

## Background Query Asynchronous Archive Query
{: #cloud-logs-background-query-asynchronous-archive-query-cli}

Submit a background query and fetch your archive logs.

### `ibmcloud cloud-logs background-query-create`
{: #cloud-logs-cli-background-query-create-command}

Submits a query that runs in the background, allowing the client to continue without waiting for the results immediately.

```sh
ibmcloud cloud-logs background-query-create --query QUERY --syntax SYNTAX [--start-date START-DATE] [--end-date END-DATE] [--now-date NOW-DATE]
```

#### Aliases
{: #cloud-logs-cli-background-query-create-command-aliases}

`background-query-create`, `bgq-create`

#### Command options
{: #cloud-logs-background-query-create-cli-options}

`--query` (string)
:   The background query to be run. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--syntax` (string)
:   The query syntax. Required.

    Allowable values are: `unspecified`, `lucene`, `dataprime`, `lucene_utf8_base64`, `dataprime_utf8_base64`.

`--start-date` (strfmt.DateTime)
:   Beginning of the time range for the query, default: end - 15 minutes or current
 time - 15 minutes if end is not defined.

`--end-date` (strfmt.DateTime)
:   End of the time range for the query. Default: start + 15 minutes or current
 time if start is not defined.

`--now-date` (strfmt.DateTime)
:   Contextual `now` for the query, default: current time. Used by functions
 like now() in DataPrime.

#### Example
{: #cloud-logs-background-query-create-examples}

```sh
ibmcloud cloud-logs background-query-create \
    --query 'source logs | filter $d.apiVersion == 42' \
    --syntax dataprime_utf8_base64 \
    --start-date 2023-11-05T13:15:30.000Z \
    --end-date 2023-11-05T13:15:30.000Z \
    --now-date 2023-11-05T13:15:30.000Z
```
{: pre}

### `ibmcloud cloud-logs background-query-status`
{: #cloud-logs-cli-background-query-status-command}

Get the status of a background query.

```sh
ibmcloud cloud-logs background-query-status --query-id QUERY-ID
```

#### Aliases
{: #cloud-logs-cli-background-query-status-command-aliases}

`background-query-status`, `bgq-status`

#### Command options
{: #cloud-logs-background-query-status-cli-options}

`--query-id` (strfmt.UUID)
:   Generated query ID that can be used to obtain the status and results of a background query. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-background-query-status-examples}

```sh
ibmcloud cloud-logs background-query-status \
    --query-id 412036c3-04be-431a-b1e2-9ebf971be6c6
```
{: pre}

#### Default JMESPath
{: #cloud-logs-background-query-status-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{SubmittedAt:submitted_at, Warnings:warnings, RunningSince:terminated.running_since, TerminatedAt:terminated.terminated_at}` |
| Error | Default | - |
|  | Table | `{SubmittedAt:submitted_at, Warnings:warnings, RunningSince:terminated.running_since, TerminatedAt:terminated.terminated_at}` |
| All pages | Default | - |
|  | Table | `{SubmittedAt:submitted_at, Warnings:warnings, RunningSince:terminated.running_since, TerminatedAt:terminated.terminated_at}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs background-query-cancel`
{: #cloud-logs-cli-background-query-cancel-command}

Cancel a background query.

```sh
ibmcloud cloud-logs background-query-cancel --query-id QUERY-ID
```

#### Aliases
{: #cloud-logs-cli-background-query-cancel-command-aliases}

`background-query-cancel`, `bgq-cancel`

#### Command options
{: #cloud-logs-background-query-cancel-cli-options}

`--query-id` (strfmt.UUID)
:   Generated query ID that can be used to obtain the status and results of a background query. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-background-query-cancel-examples}

```sh
ibmcloud cloud-logs background-query-cancel \
    --query-id 412036c3-04be-431a-b1e2-9ebf971be6c6
```
{: pre}

## Data Access Rules
{: #cloud-logs-data-access-rules-cli}

Create and manage Data Access Rules.

### `ibmcloud cloud-logs data-access-rules`
{: #cloud-logs-cli-data-access-rules-command}

Get service instance's Data Access Rules by ids.

```sh
ibmcloud cloud-logs data-access-rules [--id ID]
```


#### Command options
{: #cloud-logs-data-access-rules-cli-options}

`--id` ([]strfmt.UUID)
:   Array of data access rule IDs.

    The list items must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`. The maximum length is `4096` items. The minimum length is `0` items.

#### Example
{: #cloud-logs-data-access-rules-examples}

```sh
ibmcloud cloud-logs data-access-rules \
    --id 4f966911-4bda-407e-b069-477394effa59
```
{: pre}

#### Default JMESPath
{: #cloud-logs-data-access-rules-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `data_access_rules[*].{ID:id,Display_Name:display_name,Description:description}` |
| Error | Default | - |
|  | Table | `data_access_rules[*].{ID:id,Display_Name:display_name,Description:description}` |
| All pages | Default | - |
|  | Table | `data_access_rules[*].{ID:id,Display_Name:display_name,Description:description}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs data-access-rule-create`
{: #cloud-logs-cli-data-access-rule-create-command}

Create a data access rule.

```sh
ibmcloud cloud-logs data-access-rule-create --display-name DISPLAY-NAME --filters FILTERS --default-expression DEFAULT-EXPRESSION [--description DESCRIPTION]
```


#### Command options
{: #cloud-logs-data-access-rule-create-cli-options}

`--display-name` (string)
:   Display Name for the data access rule. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--filters` ([`DataAccessRuleFilter[]`](#cli-data-access-rule-filter-example-schema))
:   Filters for the data access rule. Required.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--default-expression` (string)
:   Default Expression for the data access rule. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--description` (string)
:   Description for the data access rule.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Example
{: #cloud-logs-data-access-rule-create-examples}

```sh
ibmcloud cloud-logs data-access-rule-create \
    --display-name 'Test data access rule' \
    --filters '[{"entity_type": "logs", "expression": "<v1> foo == \'bar\'"}]' \
    --default-expression <v1>true \
    --description 'Data access rule intended for testing'
```
{: pre}

#### Default JMESPath
{: #cloud-logs-data-access-rule-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{ID:id,Description:description}` |
| Error | Default | - |
|  | Table | `{ID:id,Description:description}` |
| All pages | Default | - |
|  | Table | `{ID:id,Description:description}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs data-access-rule-update`
{: #cloud-logs-cli-data-access-rule-update-command}

Update a data access rule.

```sh
ibmcloud cloud-logs data-access-rule-update --id ID --display-name DISPLAY-NAME --filters FILTERS --default-expression DEFAULT-EXPRESSION [--description DESCRIPTION]
```


#### Command options
{: #cloud-logs-data-access-rule-update-cli-options}

`--id` (strfmt.UUID)
:   ID of the data access rule to be deleted. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--display-name` (string)
:   Display Name for the data access rule. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--filters` ([`DataAccessRuleFilter[]`](#cli-data-access-rule-filter-example-schema))
:   Filters for the data access rule. Required.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--default-expression` (string)
:   Default Expression for the data access rule. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--description` (string)
:   Description for the data access rule.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Example
{: #cloud-logs-data-access-rule-update-examples}

```sh
ibmcloud cloud-logs data-access-rule-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --display-name 'Test data access rule' \
    --filters '[{"entity_type": "logs", "expression": "<v1> foo == \'bar\'"}]' \
    --default-expression <v1>true \
    --description 'Data access rule intended for testing'
```
{: pre}

#### Default JMESPath
{: #cloud-logs-data-access-rule-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{ID:id,Description:description}` |
| Error | Default | - |
|  | Table | `{ID:id,Description:description}` |
| All pages | Default | - |
|  | Table | `{ID:id,Description:description}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs data-access-rule-delete`
{: #cloud-logs-cli-data-access-rule-delete-command}

Delete a data access rule.

```sh
ibmcloud cloud-logs data-access-rule-delete --id ID
```


#### Command options
{: #cloud-logs-data-access-rule-delete-cli-options}

`--id` (strfmt.UUID)
:   ID of the data access rule to be deleted. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-data-access-rule-delete-examples}

```sh
ibmcloud cloud-logs data-access-rule-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

## Data Usage
{: #cloud-logs-data-usage-cli}

Data usage service.

### `ibmcloud cloud-logs data-usage`
{: #cloud-logs-cli-data-usage-command}

Get data usage metrics export status when invoked without query parameters. Get daily or detailed data usage report when invoked with query parameters.

```sh
ibmcloud cloud-logs data-usage --query QUERY [--range RANGE]
```


#### Command options
{: #cloud-logs-data-usage-cli-options}

`--query` (string)
:   Query to filter daily or detailed the data usage, by default it will use daily one. Required.

    The default value is `daily`. Allowable values are: `daily`, `detailed`.

`--range` (string)
:   The range of days to retrieve data usage, by default it will use current month.

    The default value is `current_month`. Allowable values are: `current_month`, `last_30_days`, `last_90_days`, `last_week`.

#### Example
{: #cloud-logs-data-usage-examples}

```sh
ibmcloud cloud-logs data-usage \
    --query daily \
    --range last_week
```
{: pre}

#### Default JMESPath
{: #cloud-logs-data-usage-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `data_usages` |
| Error | Default | - |
|  | Table | `data_usages` |
| All pages | Default | - |
|  | Table | `data_usages` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs data-usage-metrics-export-status-update`
{: #cloud-logs-cli-data-usage-metrics-export-status-update-command}

Update data usage metrics export status.

```sh
ibmcloud cloud-logs data-usage-metrics-export-status-update --enabled=ENABLED
```


#### Command options
{: #cloud-logs-data-usage-metrics-export-status-update-cli-options}

`--enabled` (bool)
:   Whether metrics export is enabled or not. When 'true' metrics are exported. Required.

#### Example
{: #cloud-logs-data-usage-metrics-export-status-update-examples}

```sh
ibmcloud cloud-logs data-usage-metrics-export-status-update \
    --enabled=true
```
{: pre}

## Enrichments
{: #cloud-logs-enrichments-cli}

Create and manage enrichments.

### `ibmcloud cloud-logs enrichments`
{: #cloud-logs-cli-enrichments-command}

List all enrichments.

```sh
ibmcloud cloud-logs enrichments
```


#### Example
{: #cloud-logs-enrichments-examples}

```sh
ibmcloud cloud-logs enrichments
```
{: pre}

#### Default JMESPath
{: #cloud-logs-enrichments-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `enrichments[*].{ID:id,Field_Name:field_name}` |
| Error | Default | - |
|  | Table | `enrichments[*].{ID:id,Field_Name:field_name}` |
| All pages | Default | - |
|  | Table | `enrichments[*].{ID:id,Field_Name:field_name}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs enrichment-create`
{: #cloud-logs-cli-enrichment-create-command}

Create an enrichment.

```sh
ibmcloud cloud-logs enrichment-create --field-name FIELD-NAME [--enrichment-type ENRICHMENT-TYPE | --enrichment-type-geo-ip ENRICHMENT-TYPE-GEO-IP --enrichment-type-suspicious-ip ENRICHMENT-TYPE-SUSPICIOUS-IP --enrichment-type-custom-enrichment ENRICHMENT-TYPE-CUSTOM-ENRICHMENT]
```


#### Command options
{: #cloud-logs-enrichment-create-cli-options}

`--field-name` (string)
:   The name of the field to enrich. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--enrichment-type` ([`EnrichmentV1EnrichmentType`](#cli-enrichment-v1-enrichment-type-example-schema))
:   The enrichment type. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enrichment-type=@path/to/file.json`.

`--enrichment-type-geo-ip` ([`EnrichmentV1GeoIpTypeEmpty`](#cli-enrichment-v1-geo-ip-type-empty-example-schema))
:   The geo IP enrichment. This option provides a value for a sub-field of the JSON option 'enrichment-type'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enrichment-type-geo-ip=@path/to/file.json`.

`--enrichment-type-suspicious-ip` ([`EnrichmentV1SuspiciousIpTypeEmpty`](#cli-enrichment-v1-suspicious-ip-type-empty-example-schema))
:   The suspicious IP enrichment. This option provides a value for a sub-field of the JSON option 'enrichment-type'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enrichment-type-suspicious-ip=@path/to/file.json`.

`--enrichment-type-custom-enrichment` ([`EnrichmentV1CustomEnrichmentType`](#cli-enrichment-v1-custom-enrichment-type-example-schema))
:   The custom enrichment. This option provides a value for a sub-field of the JSON option 'enrichment-type'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enrichment-type-custom-enrichment=@path/to/file.json`.

#### Examples
{: #cloud-logs-enrichment-create-examples}

```sh
ibmcloud cloud-logs enrichment-create \
    --field-name ip \
    --enrichment-type '{"geo_ip": {}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs enrichment-create \
    --field-name ip \
    --enrichment-type-geo-ip enrichmentV1GeoIpTypeEmpty
```
{: pre}

#### Default JMESPath
{: #cloud-logs-enrichment-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{,ID:id,Field_Name:field_name}` |
| Error | Default | - |
|  | Table | `{,ID:id,Field_Name:field_name}` |
| All pages | Default | - |
|  | Table | `{,ID:id,Field_Name:field_name}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs enrichment-delete`
{: #cloud-logs-cli-enrichment-delete-command}

Delete enrichments.

```sh
ibmcloud cloud-logs enrichment-delete --id ID
```


#### Command options
{: #cloud-logs-enrichment-delete-cli-options}

`--id` (int64)
:   The enrichment ID. Required.

    The maximum value is `4294967295`. The minimum value is `0`.

#### Example
{: #cloud-logs-enrichment-delete-examples}

```sh
ibmcloud cloud-logs enrichment-delete \
    --id 1
```
{: pre}

## Events To Metrics
{: #cloud-logs-events-to-metrics-cli}

Create and manage your events to metrics definitions.

### `ibmcloud cloud-logs events2metrics-list`
{: #cloud-logs-cli-events2metrics-list-command}

Lists events to metrics definitions.

```sh
ibmcloud cloud-logs events2metrics-list
```

#### Aliases
{: #cloud-logs-cli-events2metrics-list-command-aliases}

`events2metrics-list`, `e2m-list`

#### Example
{: #cloud-logs-events2metrics-list-examples}

```sh
ibmcloud cloud-logs events2metrics-list
```
{: pre}

#### Default JMESPath
{: #cloud-logs-events2metrics-list-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `events2metrics[*].{Name:name,ID:id,Create_Time:create_time,Update_Time:update_time,Type:type}` |
| Error | Default | - |
|  | Table | `events2metrics[*].{Name:name,ID:id,Create_Time:create_time,Update_Time:update_time,Type:type}` |
| All pages | Default | - |
|  | Table | `events2metrics[*].{Name:name,ID:id,Create_Time:create_time,Update_Time:update_time,Type:type}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs events2metrics-create`
{: #cloud-logs-cli-events2metrics-create-command}

Creates events to metrics definitions.

```sh
ibmcloud cloud-logs events2metrics-create [--event2-metric-prototype EVENT2-METRIC-PROTOTYPE | --event2-metric-name EVENT2-METRIC-NAME --event2-metric-description EVENT2-METRIC-DESCRIPTION --event2-metric-permutations-limit EVENT2-METRIC-PERMUTATIONS-LIMIT --event2-metric-metric-labels EVENT2-METRIC-METRIC-LABELS --event2-metric-metric-fields EVENT2-METRIC-METRIC-FIELDS --event2-metric-type EVENT2-METRIC-TYPE --event2-metric-logs-query EVENT2-METRIC-LOGS-QUERY]
```

#### Aliases
{: #cloud-logs-cli-events2metrics-create-command-aliases}

`events2metrics-create`, `e2m-create`

#### Command options
{: #cloud-logs-events2metrics-create-cli-options}

`--event2-metric-prototype` ([`Event2MetricPrototype`](#cli-event2-metric-prototype-example-schema))
:   Events to Metrics Create message. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-prototype=@path/to/file.json`.

`--event2-metric-name` (string)
:   Name of Events to Metrics to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--event2-metric-description` (string)
:   Description of Events to Metrics to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}0-9_\\-\\s]+$/`.

`--event2-metric-permutations-limit` (int64)
:   The permutation limit of the Events to Metrics. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum value is `2147483647`. The minimum value is `0`.

`--event2-metric-metric-labels` ([`ApisEvents2metricsV2MetricLabel[]`](#cli-apis-events2metrics-v2-metric-label-example-schema))
:   Events to Metrics metric labels. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-labels=@path/to/file.json`.

`--event2-metric-metric-fields` ([`ApisEvents2metricsV2MetricField[]`](#cli-apis-events2metrics-v2-metric-field-example-schema))
:   Events to Metrics metric fields. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-fields=@path/to/file.json`.

`--event2-metric-type` (string)
:   Events to Metrics type. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `logs2metrics`.

`--event2-metric-logs-query` ([`ApisLogs2metricsV2LogsQuery`](#cli-apis-logs2metrics-v2-logs-query-example-schema))
:   Events to Metrics logs query. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-logs-query=@path/to/file.json`.

#### Examples
{: #cloud-logs-events2metrics-create-examples}

```sh
ibmcloud cloud-logs events2metrics-create \
    --event2-metric-prototype '{"name": "test em2", "description": "Test Events to Metrics", "permutations_limit": 1, "metric_labels": [{"target_label": "alias_label_name", "source_field": "log_obj.string_value"}], "metric_fields": [{"target_base_metric_name": "alias_field_name", "source_field": "log_obj.numeric_field", "aggregations": [{"enabled": true, "agg_type": "samples", "target_metric_name": "alias_field_name_agg_func", "samples": {"sample_type": "max"}}]}], "type": "logs2metrics", "logs_query": {"lucene": "logs", "alias": "new_query", "applicationname_filters": ["app_name"], "subsystemname_filters": ["sub_name"], "severity_filters": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs events2metrics-create \
    --event2-metric-name 'Service catalog latency' \
    --event2-metric-description 'avg and max the latency of catalog service' \
    --event2-metric-permutations-limit 30000 \
    --event2-metric-metric-labels '[apisEvents2metricsV2MetricLabel]' \
    --event2-metric-metric-fields '[apisEvents2metricsV2MetricField]' \
    --event2-metric-type logs2metrics \
    --event2-metric-logs-query apisLogs2metricsV2LogsQuery
```
{: pre}

#### Default JMESPath
{: #cloud-logs-events2metrics-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Description:description,Create_Time:create_time,Update_Time:update_time,Type:type,Is_Internal:is_internal}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Description:description,Create_Time:create_time,Update_Time:update_time,Type:type,Is_Internal:is_internal}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Description:description,Create_Time:create_time,Update_Time:update_time,Type:type,Is_Internal:is_internal}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs events2metrics`
{: #cloud-logs-cli-events2metrics-command}

Gets events to metrics definitions by ID.

```sh
ibmcloud cloud-logs events2metrics --id ID
```

#### Aliases
{: #cloud-logs-cli-events2metrics-command-aliases}

`events2metrics`, `e2m`

#### Command options
{: #cloud-logs-events2metrics-cli-options}

`--id` (string)
:   ID of Events to Metrics to be deleted. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Example
{: #cloud-logs-events2metrics-examples}

```sh
ibmcloud cloud-logs events2metrics \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09
```
{: pre}

#### Default JMESPath
{: #cloud-logs-events2metrics-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Create_Time:create_time,Update_Time:update_time,Type:type}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Create_Time:create_time,Update_Time:update_time,Type:type}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Create_Time:create_time,Update_Time:update_time,Type:type}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs events2metrics-update`
{: #cloud-logs-cli-events2metrics-update-command}

Updates events to metrics definitions.

```sh
ibmcloud cloud-logs events2metrics-update --id ID [--event2-metric-prototype EVENT2-METRIC-PROTOTYPE | --event2-metric-name EVENT2-METRIC-NAME --event2-metric-description EVENT2-METRIC-DESCRIPTION --event2-metric-permutations-limit EVENT2-METRIC-PERMUTATIONS-LIMIT --event2-metric-metric-labels EVENT2-METRIC-METRIC-LABELS --event2-metric-metric-fields EVENT2-METRIC-METRIC-FIELDS --event2-metric-type EVENT2-METRIC-TYPE --event2-metric-logs-query EVENT2-METRIC-LOGS-QUERY]
```

#### Aliases
{: #cloud-logs-cli-events2metrics-update-command-aliases}

`events2metrics-update`, `e2m-update`

#### Command options
{: #cloud-logs-events2metrics-update-cli-options}

`--id` (string)
:   ID of Events to Metrics to be deleted. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--event2-metric-prototype` ([`Event2MetricPrototype`](#cli-event2-metric-prototype-example-schema))
:   Events to Metrics Create message. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-prototype=@path/to/file.json`.

`--event2-metric-name` (string)
:   Name of Events to Metrics to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--event2-metric-description` (string)
:   Description of Events to Metrics to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}0-9_\\-\\s]+$/`.

`--event2-metric-permutations-limit` (int64)
:   The permutation limit of the Events to Metrics. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum value is `2147483647`. The minimum value is `0`.

`--event2-metric-metric-labels` ([`ApisEvents2metricsV2MetricLabel[]`](#cli-apis-events2metrics-v2-metric-label-example-schema))
:   Events to Metrics metric labels. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-labels=@path/to/file.json`.

`--event2-metric-metric-fields` ([`ApisEvents2metricsV2MetricField[]`](#cli-apis-events2metrics-v2-metric-field-example-schema))
:   Events to Metrics metric fields. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-fields=@path/to/file.json`.

`--event2-metric-type` (string)
:   Events to Metrics type. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `logs2metrics`.

`--event2-metric-logs-query` ([`ApisLogs2metricsV2LogsQuery`](#cli-apis-logs2metrics-v2-logs-query-example-schema))
:   Events to Metrics logs query. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-logs-query=@path/to/file.json`.

#### Examples
{: #cloud-logs-events2metrics-update-examples}

```sh
ibmcloud cloud-logs events2metrics-update \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09 \
    --event2-metric-prototype '{"name": "test em2", "description": "Test Events to Metrics updated", "permutations_limit": 1, "metric_labels": [{"target_label": "alias_label_name", "source_field": "log_obj.string_value"}], "metric_fields": [{"target_base_metric_name": "alias_field_name", "source_field": "log_obj.numeric_field", "aggregations": [{"enabled": true, "agg_type": "samples", "target_metric_name": "alias_field_name_agg_func", "samples": {"sample_type": "max"}}]}], "type": "logs2metrics", "logs_query": {"lucene": "logs", "alias": "new_query", "applicationname_filters": ["app_name"], "subsystemname_filters": ["sub_name"], "severity_filters": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs events2metrics-update \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09 \
    --event2-metric-name 'Service catalog latency' \
    --event2-metric-description 'avg and max the latency of catalog service' \
    --event2-metric-permutations-limit 30000 \
    --event2-metric-metric-labels '[apisEvents2metricsV2MetricLabel]' \
    --event2-metric-metric-fields '[apisEvents2metricsV2MetricField]' \
    --event2-metric-type logs2metrics \
    --event2-metric-logs-query apisLogs2metricsV2LogsQuery
```
{: pre}

#### Default JMESPath
{: #cloud-logs-events2metrics-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Create_Time:create_time,Update_Time:update_time,Type:type,Is_Internal:is_internal}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Create_Time:create_time,Update_Time:update_time,Type:type,Is_Internal:is_internal}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Create_Time:create_time,Update_Time:update_time,Type:type,Is_Internal:is_internal}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs events2metrics-delete`
{: #cloud-logs-cli-events2metrics-delete-command}

Deletes events to metrics definitions by ID.

```sh
ibmcloud cloud-logs events2metrics-delete --id ID
```

#### Aliases
{: #cloud-logs-cli-events2metrics-delete-command-aliases}

`events2metrics-delete`, `e2m-delete`

#### Command options
{: #cloud-logs-events2metrics-delete-cli-options}

`--id` (string)
:   ID of Events to Metrics to be deleted. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Example
{: #cloud-logs-events2metrics-delete-examples}

```sh
ibmcloud cloud-logs events2metrics-delete \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09
```
{: pre}

## Extensions
{: #cloud-logs-extensions-cli}

Manage extensions and extension deployments.

### `ibmcloud cloud-logs extension`
{: #cloud-logs-cli-extension-command}

Get an extension by ID.

```sh
ibmcloud cloud-logs extension --id ID
```


#### Command options
{: #cloud-logs-extension-cli-options}

`--id` (string)
:   The unique identifier of the extension. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Example
{: #cloud-logs-extension-examples}

```sh
ibmcloud cloud-logs extension \
    --id exampleString
```
{: pre}

#### Default JMESPath
{: #cloud-logs-extension-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Revisions:revisions[*].version}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Revisions:revisions[*].version}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Revisions:revisions[*].version}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs extension-deployment`
{: #cloud-logs-cli-extension-deployment-command}

Get deployment details of an extension using id of an extension.

```sh
ibmcloud cloud-logs extension-deployment --id ID
```


#### Command options
{: #cloud-logs-extension-deployment-cli-options}

`--id` (string)
:   The unique identifier of the extension. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Example
{: #cloud-logs-extension-deployment-examples}

```sh
ibmcloud cloud-logs extension-deployment \
    --id exampleString
```
{: pre}

#### Default JMESPath
{: #cloud-logs-extension-deployment-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{DeployedVersion:version}` |
| Error | Default | - |
|  | Table | `{DeployedVersion:version}` |
| All pages | Default | - |
|  | Table | `{DeployedVersion:version}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs extension-deployment-manage`
{: #cloud-logs-cli-extension-deployment-manage-command}

Deploy or update deployment of an extension using extension ID.

```sh
ibmcloud cloud-logs extension-deployment-manage --id ID --version VERSION --item-ids ITEM-IDS [--applications APPLICATIONS] [--subsystems SUBSYSTEMS]
```


#### Command options
{: #cloud-logs-extension-deployment-manage-cli-options}

`--id` (string)
:   The unique identifier of the extension. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--version` (string)
:   The version of the Extension revision to deploy. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--item-ids` ([]string)
:   The list of Extension item IDs to deploy. Required.

    The list items must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`. The maximum length is `4096` items. The minimum length is `1` item.

`--applications` ([]string)
:   Applications that the Extension is deployed for. When this is empty, it is applied to all applications.

    The list items must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`. The maximum length is `4096` items. The minimum length is `0` items.

`--subsystems` ([]string)
:   Subsystems that the Extension is deployed. When this is empty, it is applied to all subsystems.

    The list items must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`. The maximum length is `4096` items. The minimum length is `0` items.

#### Example
{: #cloud-logs-extension-deployment-manage-examples}

```sh
ibmcloud cloud-logs extension-deployment-manage \
    --id exampleString \
    --version exampleString \
    --item-ids b9a5500c-715e-4ead-9bbe-56fdefffbfcd \
    --applications ltest_0401 \
    --subsystems ltest_0401
```
{: pre}

#### Default JMESPath
{: #cloud-logs-extension-deployment-manage-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Version:version,ItemIds:item_ids[*]}` |
| Error | Default | - |
|  | Table | `{Version:version,ItemIds:item_ids[*]}` |
| All pages | Default | - |
|  | Table | `{Version:version,ItemIds:item_ids[*]}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs extension-deployment-delete`
{: #cloud-logs-cli-extension-deployment-delete-command}

Delete deployment of an extension using extension ID.

```sh
ibmcloud cloud-logs extension-deployment-delete --id ID
```


#### Command options
{: #cloud-logs-extension-deployment-delete-cli-options}

`--id` (string)
:   The unique identifier of the extension. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Example
{: #cloud-logs-extension-deployment-delete-examples}

```sh
ibmcloud cloud-logs extension-deployment-delete \
    --id exampleString
```
{: pre}

#### Default JMESPath
{: #cloud-logs-extension-deployment-delete-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{FailedItem:failed_items.item_id,FailureReason:failed_items.reason}` |
| Error | Default | - |
|  | Table | `{FailedItem:failed_items.item_id,FailureReason:failed_items.reason}` |
| All pages | Default | - |
|  | Table | `{FailedItem:failed_items.item_id,FailureReason:failed_items.reason}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs extensions`
{: #cloud-logs-cli-extensions-command}

Get list of extensions.

```sh
ibmcloud cloud-logs extensions [--deployed=DEPLOYED]
```


#### Command options
{: #cloud-logs-extensions-cli-options}

`--deployed` (bool)
:   Optional deployment filter. If omitted, returns all extensions. If true, returns only deployed extensions. If false, returns only non-deployed extensions.

#### Example
{: #cloud-logs-extensions-examples}

```sh
ibmcloud cloud-logs extensions \
    --deployed=true
```
{: pre}

#### Default JMESPath
{: #cloud-logs-extensions-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `extensions[*].{Name:name,ID:id,Revisions:revisions[*].version,DeployedVersion:deployment.version}` |
| Error | Default | - |
|  | Table | `extensions[*].{Name:name,ID:id,Revisions:revisions[*].version,DeployedVersion:deployment.version}` |
| All pages | Default | - |
|  | Table | `extensions[*].{Name:name,ID:id,Revisions:revisions[*].version,DeployedVersion:deployment.version}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

## Folders For Views
{: #cloud-logs-folders-for-views-cli}

Create and manage view folders.

### `ibmcloud cloud-logs view-folders`
{: #cloud-logs-cli-view-folders-command}

List view's folders.

```sh
ibmcloud cloud-logs view-folders
```


#### Example
{: #cloud-logs-view-folders-examples}

```sh
ibmcloud cloud-logs view-folders
```
{: pre}

#### Default JMESPath
{: #cloud-logs-view-folders-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `view_folders[*].{Name:name,ID:id}` |
| Error | Default | - |
|  | Table | `view_folders[*].{Name:name,ID:id}` |
| All pages | Default | - |
|  | Table | `view_folders[*].{Name:name,ID:id}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs view-folder-create`
{: #cloud-logs-cli-view-folder-create-command}

Create view folder.

```sh
ibmcloud cloud-logs view-folder-create --name NAME
```


#### Command options
{: #cloud-logs-view-folder-create-cli-options}

`--name` (string)
:   View folder name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Example
{: #cloud-logs-view-folder-create-examples}

```sh
ibmcloud cloud-logs view-folder-create \
    --name 'My Folder'
```
{: pre}

#### Default JMESPath
{: #cloud-logs-view-folder-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs view-folder`
{: #cloud-logs-cli-view-folder-command}

Get view folder.

```sh
ibmcloud cloud-logs view-folder --id ID
```


#### Command options
{: #cloud-logs-view-folder-cli-options}

`--id` (strfmt.UUID)
:   Folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-view-folder-examples}

```sh
ibmcloud cloud-logs view-folder \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

#### Default JMESPath
{: #cloud-logs-view-folder-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `view_folders[*].{Name:name,ID:id}` |
| Error | Default | - |
|  | Table | `view_folders[*].{Name:name,ID:id}` |
| All pages | Default | - |
|  | Table | `view_folders[*].{Name:name,ID:id}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs view-folder-update`
{: #cloud-logs-cli-view-folder-update-command}

Replaces an existing view folder.

```sh
ibmcloud cloud-logs view-folder-update --id ID --name NAME
```


#### Command options
{: #cloud-logs-view-folder-update-cli-options}

`--id` (strfmt.UUID)
:   Folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--name` (string)
:   View folder name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Example
{: #cloud-logs-view-folder-update-examples}

```sh
ibmcloud cloud-logs view-folder-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'My Folder'
```
{: pre}

#### Default JMESPath
{: #cloud-logs-view-folder-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `view_folders[*].{Name:name,ID:id}` |
| Error | Default | - |
|  | Table | `view_folders[*].{Name:name,ID:id}` |
| All pages | Default | - |
|  | Table | `view_folders[*].{Name:name,ID:id}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs view-folder-delete`
{: #cloud-logs-cli-view-folder-delete-command}

Deletes a view folder by ID.

```sh
ibmcloud cloud-logs view-folder-delete --id ID
```


#### Command options
{: #cloud-logs-view-folder-delete-cli-options}

`--id` (strfmt.UUID)
:   Folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-view-folder-delete-examples}

```sh
ibmcloud cloud-logs view-folder-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

## Log Data Retention Tags
{: #cloud-logs-log-data-retention-tags-cli}

Get and update log data retention tags.

### `ibmcloud cloud-logs log-data-retention-tags`
{: #cloud-logs-cli-log-data-retention-tags-command}

Get log data retention tags. Returns 404 if retention tags have not been activated.

```sh
ibmcloud cloud-logs log-data-retention-tags
```


#### Example
{: #cloud-logs-log-data-retention-tags-examples}

```sh
ibmcloud cloud-logs log-data-retention-tags
```
{: pre}

#### Default JMESPath
{: #cloud-logs-log-data-retention-tags-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `tags` |
| Error | Default | - |
|  | Table | `tags` |
| All pages | Default | - |
|  | Table | `tags` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs log-data-retention-tags-update`
{: #cloud-logs-cli-log-data-retention-tags-update-command}

Update log data retention tags. If retention tags have not been activated yet, the first successful PUT request will activate them. An archive bucket must be configured before retention tags can be activated.

```sh
ibmcloud cloud-logs log-data-retention-tags-update --tags TAGS
```


#### Command options
{: #cloud-logs-log-data-retention-tags-update-cli-options}

`--tags` ([]string)
:   List of editable archive retention tags, excluding non-editable tags such as Default. Required.

    The list items must match regular expression `/^[a-zA-Z0-9_-]+$/`. The maximum length is `3` items. The minimum length is `3` items.

#### Example
{: #cloud-logs-log-data-retention-tags-update-examples}

```sh
ibmcloud cloud-logs log-data-retention-tags-update \
    --tags Short,Intermediate,Long
```
{: pre}

## Outbound Integrations
{: #cloud-logs-outbound-integrations-cli}

Create and manage your outbound integrations so that you can receive alerts.

### `ibmcloud cloud-logs outgoing-webhooks`
{: #cloud-logs-cli-outgoing-webhooks-command}

List Outbound Integrations.

```sh
ibmcloud cloud-logs outgoing-webhooks [--type TYPE]
```


#### Command options
{: #cloud-logs-outgoing-webhooks-cli-options}

`--type` (string)
:   The type of the deployed outbound integrations to list.

    Allowable values are: `ibm_event_notifications`.

#### Example
{: #cloud-logs-outgoing-webhooks-examples}

```sh
ibmcloud cloud-logs outgoing-webhooks \
    --type ibm_event_notifications
```
{: pre}

#### Default JMESPath
{: #cloud-logs-outgoing-webhooks-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `outgoing_webhooks[*].{Name:name,ID:id,URL:url,Created_At:created_at,Updated_At:updated_at,External_ID:external_id}` |
| Error | Default | - |
|  | Table | `outgoing_webhooks[*].{Name:name,ID:id,URL:url,Created_At:created_at,Updated_At:updated_at,External_ID:external_id}` |
| All pages | Default | - |
|  | Table | `outgoing_webhooks[*].{Name:name,ID:id,URL:url,Created_At:created_at,Updated_At:updated_at,External_ID:external_id}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs outgoing-webhook-create`
{: #cloud-logs-cli-outgoing-webhook-create-command}

Create an outbound integration.

```sh
ibmcloud cloud-logs outgoing-webhook-create [--prototype PROTOTYPE | --type TYPE --name NAME --url URL --ibm-event-notifications IBM-EVENT-NOTIFICATIONS]
```


#### Command options
{: #cloud-logs-outgoing-webhook-create-cli-options}

`--prototype` ([`OutgoingWebhookPrototype`](#cli-prototype-example-schema))
:   The input data of the outbound integration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--type` (string)
:   The type of the deployed outbound integrations to list. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `ibm_event_notifications`.

`--name` (string)
:   The name of the outbound integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--url` (string)
:   The URL of the outbound integration. This value is null for IBM Events Notifications integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--ibm-event-notifications` ([`OutgoingWebhooksV1IbmEventNotificationsConfig`](#cli-outgoing-webhooks-v1-ibm-event-notifications-config-example-schema))
:   The configuration of the IBM Event Notifications outbound integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--ibm-event-notifications=@path/to/file.json`.

#### Examples
{: #cloud-logs-outgoing-webhook-create-examples}

```sh
ibmcloud cloud-logs outgoing-webhook-create \
    --prototype '{"type": "ibm_event_notifications", "name": "Event Notifications Integration", "url": "https://example.com", "ibm_event_notifications": {"event_notifications_instance_id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "region_id": "eu-es", "source_id": "crn:v1:staging:public:logs:eu-gb:a/223af6f4260f42ebe23e95fcddd33cb7:63a3e4be-cb73-4f52-898e-8e93484a70a5::", "source_name": "IBM Cloud Event Notifications", "endpoint_type": "private"}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs outgoing-webhook-create \
    --type ibm_event_notifications \
    --name 'Event Notifications Integration' \
    --url https://example.com \
    --ibm-event-notifications outgoingWebhooksV1IbmEventNotificationsConfig
```
{: pre}

#### Default JMESPath
{: #cloud-logs-outgoing-webhook-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Type:type,URL:url,Endpoint_Type:ibm_event_notifications.endpoint_type,Created_At:created_at,Updated_At:updated_at,External_ID:external_id,Source_ID:ibm_event_notifications.source_id,Source_Name:ibm_event_notifications.source_name}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Type:type,URL:url,Endpoint_Type:ibm_event_notifications.endpoint_type,Created_At:created_at,Updated_At:updated_at,External_ID:external_id,Source_ID:ibm_event_notifications.source_id,Source_Name:ibm_event_notifications.source_name}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Type:type,URL:url,Endpoint_Type:ibm_event_notifications.endpoint_type,Created_At:created_at,Updated_At:updated_at,External_ID:external_id,Source_ID:ibm_event_notifications.source_id,Source_Name:ibm_event_notifications.source_name}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs outgoing-webhook`
{: #cloud-logs-cli-command}

Gets an outbound integration by ID.

```sh
ibmcloud cloud-logs outgoing-webhook --id ID
```


#### Command options
{: #cloud-logs-cli-options}

`--id` (strfmt.UUID)
:   The ID of the outbound integration to delete. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-examples}

```sh
ibmcloud cloud-logs outgoing-webhook \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660
```
{: pre}

#### Default JMESPath
{: #cloud-logs-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Type:type,URL:url,Endpoint_Type:ibm_event_notifications.endpoint_type,Created_At:created_at,Updated_At:updated_at,External_ID:external_id,Source_ID:ibm_event_notifications.source_id,Source_Name:ibm_event_notifications.source_name}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Type:type,URL:url,Endpoint_Type:ibm_event_notifications.endpoint_type,Created_At:created_at,Updated_At:updated_at,External_ID:external_id,Source_ID:ibm_event_notifications.source_id,Source_Name:ibm_event_notifications.source_name}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Type:type,URL:url,Endpoint_Type:ibm_event_notifications.endpoint_type,Created_At:created_at,Updated_At:updated_at,External_ID:external_id,Source_ID:ibm_event_notifications.source_id,Source_Name:ibm_event_notifications.source_name}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs outgoing-webhook-update`
{: #cloud-logs-cli-outgoing-webhook-update-command}

Update an outbound integration.

```sh
ibmcloud cloud-logs outgoing-webhook-update --id ID [--prototype PROTOTYPE | --type TYPE --name NAME --url URL --ibm-event-notifications IBM-EVENT-NOTIFICATIONS]
```


#### Command options
{: #cloud-logs-outgoing-webhook-update-cli-options}

`--id` (strfmt.UUID)
:   The ID of the outbound integration to delete. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--prototype` ([`OutgoingWebhookPrototype`](#cli-prototype-example-schema))
:   The input data of the outbound integration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--type` (string)
:   The type of the deployed outbound integrations to list. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `ibm_event_notifications`.

`--name` (string)
:   The name of the outbound integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--url` (string)
:   The URL of the outbound integration. This value is null for IBM Events Notifications integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--ibm-event-notifications` ([`OutgoingWebhooksV1IbmEventNotificationsConfig`](#cli-outgoing-webhooks-v1-ibm-event-notifications-config-example-schema))
:   The configuration of the IBM Event Notifications outbound integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--ibm-event-notifications=@path/to/file.json`.

#### Examples
{: #cloud-logs-outgoing-webhook-update-examples}

```sh
ibmcloud cloud-logs outgoing-webhook-update \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660 \
    --prototype '{"type": "ibm_event_notifications", "name": "Event Notifications Integration", "url": "https://example.com", "ibm_event_notifications": {"event_notifications_instance_id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "region_id": "eu-es", "source_id": "crn:v1:staging:public:logs:eu-gb:a/223af6f4260f42ebe23e95fcddd33cb7:63a3e4be-cb73-4f52-898e-8e93484a70a5::", "source_name": "IBM Cloud Event Notifications", "endpoint_type": "private"}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs outgoing-webhook-update \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660 \
    --type ibm_event_notifications \
    --name 'Event Notifications Integration' \
    --url https://example.com \
    --ibm-event-notifications outgoingWebhooksV1IbmEventNotificationsConfig
```
{: pre}

#### Default JMESPath
{: #cloud-logs-outgoing-webhook-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Type:type,URL:url,Endpoint_Type:ibm_event_notifications.endpoint_type,Created_At:created_at,Updated_At:updated_at,External_ID:external_id,Source_ID:ibm_event_notifications.source_id,Source_Name:ibm_event_notifications.source_name}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Type:type,URL:url,Endpoint_Type:ibm_event_notifications.endpoint_type,Created_At:created_at,Updated_At:updated_at,External_ID:external_id,Source_ID:ibm_event_notifications.source_id,Source_Name:ibm_event_notifications.source_name}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Type:type,URL:url,Endpoint_Type:ibm_event_notifications.endpoint_type,Created_At:created_at,Updated_At:updated_at,External_ID:external_id,Source_ID:ibm_event_notifications.source_id,Source_Name:ibm_event_notifications.source_name}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs outgoing-webhook-delete`
{: #cloud-logs-cli-outgoing-webhook-delete-command}

Delete an outbound integration.

```sh
ibmcloud cloud-logs outgoing-webhook-delete --id ID
```


#### Command options
{: #cloud-logs-outgoing-webhook-delete-cli-options}

`--id` (strfmt.UUID)
:   The ID of the outbound integration to delete. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-outgoing-webhook-delete-examples}

```sh
ibmcloud cloud-logs outgoing-webhook-delete \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660
```
{: pre}

## Policies
{: #cloud-logs-policies-cli}

Create and manage TCO policies.

### `ibmcloud cloud-logs policy`
{: #cloud-logs-cli-command}

Gets policy by ID.

```sh
ibmcloud cloud-logs policy --id ID
```


#### Command options
{: #cloud-logs-cli-options}

`--id` (strfmt.UUID)
:   ID of policy. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-examples}

```sh
ibmcloud cloud-logs policy \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

#### Default JMESPath
{: #cloud-logs-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs policy-update`
{: #cloud-logs-cli-policy-update-command}

Updates an existing policy.

```sh
ibmcloud cloud-logs policy-update --id ID [--prototype PROTOTYPE | --name NAME --before BEFORE --description DESCRIPTION --priority PRIORITY --application-rule APPLICATION-RULE --subsystem-rule SUBSYSTEM-RULE --archive-retention-tag ARCHIVE-RETENTION-TAG --enabled=ENABLED --log-rules LOG-RULES]
```


#### Command options
{: #cloud-logs-policy-update-cli-options}

`--id` (strfmt.UUID)
:   ID of policy. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--prototype` ([`PolicyPrototype`](#cli-prototype-example-schema))
:   Create policy request. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--name` (string)
:   Policy name. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--before` ([`PolicyBeforePrototype`](#cli-before-prototype-example-schema))
:   The policy will be inserted immediately before the existing policy with this ID. If unspecified, the policy will be inserted after all existing policies. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--before=@path/to/file.json`.

`--description` (string)
:   Policy description. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}0-9_\\-\\s]+$/`.

`--priority` (string)
:   The data pipeline sources that match the policy rules will continue to be processed by Cloud Logs. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `type_unspecified`, `type_block`, `type_low`, `type_medium`, `type_high`.

`--application-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching the application name. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--application-rule=@path/to/file.json`.

`--subsystem-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching the application name. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--subsystem-rule=@path/to/file.json`.

`--archive-retention-tag` (string)
:   Archive retention tag. Required when retention tags are active. Cannot be set when retention tags are not active. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `255` characters. The minimum length is `1` character. The value must match regular expression `/^[a-zA-Z0-9_-]+$/`.

`--enabled` (bool)
:   Flag to enable or disable a policy. This flag is supported only while updating a policy, since the policies are always enabled during creation. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The default value is `true`.

`--log-rules` ([`QuotaV1LogRules`](#cli-quota-v1-log-rules-example-schema))
:   Log rules. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--log-rules=@path/to/file.json`.

#### Examples
{: #cloud-logs-policy-update-examples}

```sh
ibmcloud cloud-logs policy-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --prototype '{"name": "Med_policy", "before": {"id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "description": "Medium policy", "priority": "type_high", "application_rule": {"rule_type_id": "is", "name": "test"}, "subsystem_rule": {"rule_type_id": "is", "name": "test"}, "archive_retention_tag": "Default", "enabled": true, "log_rules": {"severities": ["debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs policy-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'My Policy' \
    --before policyBeforePrototype \
    --description 'My Policy description' \
    --priority type_high \
    --application-rule quotaV1Rule \
    --subsystem-rule quotaV1Rule \
    --archive-retention-tag Default \
    --enabled=true \
    --log-rules quotaV1LogRules
```
{: pre}

#### Default JMESPath
{: #cloud-logs-policy-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs policy-delete`
{: #cloud-logs-cli-policy-delete-command}

Deletes an existing policy.

```sh
ibmcloud cloud-logs policy-delete --id ID
```


#### Command options
{: #cloud-logs-policy-delete-cli-options}

`--id` (strfmt.UUID)
:   ID of policy. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-policy-delete-examples}

```sh
ibmcloud cloud-logs policy-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs policies`
{: #cloud-logs-cli-policies-command}

Gets policies.

```sh
ibmcloud cloud-logs policies [--enabled-only=ENABLED-ONLY] [--source-type SOURCE-TYPE]
```


#### Command options
{: #cloud-logs-policies-cli-options}

`--enabled-only` (bool)
:   Optionally filter only enabled policies.

`--source-type` (string)
:   Source type used to filter policies.

    Allowable values are: `unspecified`, `logs`.

#### Example
{: #cloud-logs-policies-examples}

```sh
ibmcloud cloud-logs policies \
    --enabled-only=true \
    --source-type logs
```
{: pre}

#### Default JMESPath
{: #cloud-logs-policies-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `policies[*].{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
| Error | Default | - |
|  | Table | `policies[*].{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
| All pages | Default | - |
|  | Table | `policies[*].{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs policy-create`
{: #cloud-logs-cli-policy-create-command}

Creates a new policy.

```sh
ibmcloud cloud-logs policy-create [--prototype PROTOTYPE | --name NAME --before BEFORE --description DESCRIPTION --priority PRIORITY --application-rule APPLICATION-RULE --subsystem-rule SUBSYSTEM-RULE --archive-retention-tag ARCHIVE-RETENTION-TAG --enabled=ENABLED --log-rules LOG-RULES]
```


#### Command options
{: #cloud-logs-policy-create-cli-options}

`--prototype` ([`PolicyPrototype`](#cli-prototype-example-schema))
:   Create policy request. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--name` (string)
:   Policy name. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--before` ([`PolicyBeforePrototype`](#cli-before-prototype-example-schema))
:   The policy will be inserted immediately before the existing policy with this ID. If unspecified, the policy will be inserted after all existing policies. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--before=@path/to/file.json`.

`--description` (string)
:   Policy description. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}0-9_\\-\\s]+$/`.

`--priority` (string)
:   The data pipeline sources that match the policy rules will continue to be processed by Cloud Logs. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `type_unspecified`, `type_block`, `type_low`, `type_medium`, `type_high`.

`--application-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching the application name. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--application-rule=@path/to/file.json`.

`--subsystem-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching the application name. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--subsystem-rule=@path/to/file.json`.

`--archive-retention-tag` (string)
:   Archive retention tag. Required when retention tags are active. Cannot be set when retention tags are not active. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `255` characters. The minimum length is `1` character. The value must match regular expression `/^[a-zA-Z0-9_-]+$/`.

`--enabled` (bool)
:   Flag to enable or disable a policy. This flag is supported only while updating a policy, since the policies are always enabled during creation. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The default value is `true`.

`--log-rules` ([`QuotaV1LogRules`](#cli-quota-v1-log-rules-example-schema))
:   Log rules. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--log-rules=@path/to/file.json`.

#### Examples
{: #cloud-logs-policy-create-examples}

```sh
ibmcloud cloud-logs policy-create \
    --prototype '{"name": "Med_policy", "before": {"id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "description": "Medium Policy", "priority": "type_high", "application_rule": {"rule_type_id": "is", "name": "test"}, "subsystem_rule": {"rule_type_id": "is", "name": "test"}, "archive_retention_tag": "Default", "enabled": true, "log_rules": {"severities": ["debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs policy-create \
    --name 'My Policy' \
    --before policyBeforePrototype \
    --description 'My Policy description' \
    --priority type_high \
    --application-rule quotaV1Rule \
    --subsystem-rule quotaV1Rule \
    --archive-retention-tag Default \
    --enabled=true \
    --log-rules quotaV1LogRules
```
{: pre}

#### Default JMESPath
{: #cloud-logs-policy-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled,Created_At:created_at,Updated_At:updated_at}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

## Rules
{: #cloud-logs-rules-cli}

Create and manage parsing rules.

### `ibmcloud cloud-logs rule-group`
{: #cloud-logs-cli-rule-group-command}

Gets rule group by groupid.

```sh
ibmcloud cloud-logs rule-group --id id
```


#### Command options
{: #cloud-logs-rule-group-cli-options}

`--id` (strfmt.UUID)
:   The group ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-rule-group-examples}

```sh
ibmcloud cloud-logs rule-group \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

#### Default JMESPath
{: #cloud-logs-rule-group-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs rule-group-update`
{: #cloud-logs-cli-rule-group-update-command}

Updates rule group by groupid.

```sh
ibmcloud cloud-logs rule-group-update --id id --name NAME --rule-subgroups RULE-SUBGROUPS [--description DESCRIPTION] [--enabled=ENABLED] [--rule-matchers RULE-MATCHERS] [--order ORDER]
```


#### Command options
{: #cloud-logs-rule-group-update-cli-options}

`--id` (strfmt.UUID)
:   The group ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--name` (string)
:   The name of the rule group. Required.

    The maximum length is `255` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--rule-subgroups` ([`RulesV1CreateRuleGroupRequestCreateRuleSubgroup[]`](#cli-rules-v1-create-rule-group-request-create-rule-subgroup-example-schema))
:   Rule subgroups. The first rule subgroup will be executed first. If there is no match, subsequent rule groups will be attempted until there is a match. Rule groups are attempted in order. Required.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-subgroups=@path/to/file.json`.

`--description` (string)
:   A description of the rule group. The description will describe the purpose of the rule group.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}0-9_\\-\\s]+$/`.

`--enabled` (bool)
:   Whether or not the rule is enabled.

`--rule-matchers` ([`RulesV1RuleMatcher[]`](#cli-rules-v1-rule-matcher-example-schema))
:   Optional rule matchers which, if matched, will process the rule through the rule group.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-matchers=@path/to/file.json`.

`--order` (int64)
:   The order in which the rule group will be evaluated. The lower the order, the more priority the group will have. Not providing the order will, by default, create a group with the last order.

    The maximum value is `4294967295`. The minimum value is `0`.

#### Example
{: #cloud-logs-rule-group-update-examples}

```sh
ibmcloud cloud-logs rule-group-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name mysql-extractrule \
    --rule-subgroups '[{"rules": [{"name": "mysql-parse", "description": "mysql-parse", "source_field": "text", "parameters": {"parse_parameters": {"destination_field": "text", "rule": "(?P<timestamp>[^,]+),(?P<hostname>[^,]+),(?P<username>[^,]+),(?P<ip>[^,]+),(?P<connectionId>[0-9]+),(?P<queryId>[0-9]+),(?P<operation>[^,]+),(?P<database>[^,]+),\'?(?P<object>.*)\'?,(?P<returnCode>[0-9]+)"}}, "enabled": true, "order": 1}], "enabled": true, "order": 1}]' \
    --description 'mysql audit logs parser' \
    --enabled=true \
    --rule-matchers '[{"subsystem_name": {"value": "mysql"}}]' \
    --order 39
```
{: pre}

#### Default JMESPath
{: #cloud-logs-rule-group-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs rule-group-delete`
{: #cloud-logs-cli-rule-group-delete-command}

Deletes rule group by groupid.

```sh
ibmcloud cloud-logs rule-group-delete --id id
```


#### Command options
{: #cloud-logs-rule-group-delete-cli-options}

`--id` (strfmt.UUID)
:   The group ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-rule-group-delete-examples}

```sh
ibmcloud cloud-logs rule-group-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs rule-groups`
{: #cloud-logs-cli-rule-groups-command}

Gets all rule groups.

```sh
ibmcloud cloud-logs rule-groups
```


#### Example
{: #cloud-logs-rule-groups-examples}

```sh
ibmcloud cloud-logs rule-groups
```
{: pre}

#### Default JMESPath
{: #cloud-logs-rule-groups-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `rulegroups[*].{Name:name,ID:id,Enabled:enabled}` |
| Error | Default | - |
|  | Table | `rulegroups[*].{Name:name,ID:id,Enabled:enabled}` |
| All pages | Default | - |
|  | Table | `rulegroups[*].{Name:name,ID:id,Enabled:enabled}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs rule-group-create`
{: #cloud-logs-cli-rule-group-create-command}

Creates rule group.

```sh
ibmcloud cloud-logs rule-group-create --name NAME --rule-subgroups RULE-SUBGROUPS [--description DESCRIPTION] [--enabled=ENABLED] [--rule-matchers RULE-MATCHERS] [--order ORDER]
```


#### Command options
{: #cloud-logs-rule-group-create-cli-options}

`--name` (string)
:   The name of the rule group. Required.

    The maximum length is `255` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--rule-subgroups` ([`RulesV1CreateRuleGroupRequestCreateRuleSubgroup[]`](#cli-rules-v1-create-rule-group-request-create-rule-subgroup-example-schema))
:   Rule subgroups. The first rule subgroup will be executed first. If there is no match, subsequent rule groups will be attempted until there is a match. Rule groups are attempted in order. Required.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-subgroups=@path/to/file.json`.

`--description` (string)
:   A description of the rule group. The description will describe the purpose of the rule group.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}0-9_\\-\\s]+$/`.

`--enabled` (bool)
:   Whether or not the rule is enabled.

`--rule-matchers` ([`RulesV1RuleMatcher[]`](#cli-rules-v1-rule-matcher-example-schema))
:   Optional rule matchers which, if matched, will process the rule through the rule group.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-matchers=@path/to/file.json`.

`--order` (int64)
:   The order in which the rule group will be evaluated. The lower the order, the more priority the group will have. Not providing the order will, by default, create a group with the last order.

    The maximum value is `4294967295`. The minimum value is `0`.

#### Example
{: #cloud-logs-rule-group-create-examples}

```sh
ibmcloud cloud-logs rule-group-create \
    --name mysql-extractrule \
    --rule-subgroups '[{"rules": [{"name": "mysql-parse", "description": "mysql-parse", "source_field": "text", "parameters": {"parse_parameters": {"destination_field": "text", "rule": "(?P<timestamp>[^,]+),(?P<hostname>[^,]+),(?P<username>[^,]+),(?P<ip>[^,]+),(?P<connectionId>[0-9]+),(?P<queryId>[0-9]+),(?P<operation>[^,]+),(?P<database>[^,]+),\'?(?P<object>.*)\'?,(?P<returnCode>[0-9]+)"}}, "enabled": true, "order": 1}], "enabled": true, "order": 1}]' \
    --description 'mysql audit logs  parser' \
    --enabled=true \
    --rule-matchers '[{"subsystem_name": {"value": "mysql"}}]' \
    --order 39
```
{: pre}

#### Default JMESPath
{: #cloud-logs-rule-group-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id,Enabled:enabled}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

## Streams
{: #cloud-logs-streams-cli}

Create and manage your Event Streams Integrations.

### `ibmcloud cloud-logs event-stream-targets`
{: #cloud-logs-cli-event-stream-targets-command}

List all Event Streams.

```sh
ibmcloud cloud-logs event-stream-targets
```


#### Example
{: #cloud-logs-event-stream-targets-examples}

```sh
ibmcloud cloud-logs event-stream-targets
```
{: pre}

#### Default JMESPath
{: #cloud-logs-event-stream-targets-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `streams[*].{Name:name, ID:id, Status:is_active, Brokers:ibm_event_streams.brokers, DpxlExpression:dpxl_expression, Topic:ibm_event_streams.topic, Compression:compression_type, CreatedAt:created_at, UpdatedAt:updated_at}` |
| Error | Default | - |
|  | Table | `streams[*].{Name:name, ID:id, Status:is_active, Brokers:ibm_event_streams.brokers, DpxlExpression:dpxl_expression, Topic:ibm_event_streams.topic, Compression:compression_type, CreatedAt:created_at, UpdatedAt:updated_at}` |
| All pages | Default | - |
|  | Table | `streams[*].{Name:name, ID:id, Status:is_active, Brokers:ibm_event_streams.brokers, DpxlExpression:dpxl_expression, Topic:ibm_event_streams.topic, Compression:compression_type, CreatedAt:created_at, UpdatedAt:updated_at}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs event-stream-target-create`
{: #cloud-logs-cli-event-stream-target-create-command}

Create an Event Stream Integration.

```sh
ibmcloud cloud-logs event-stream-target-create --name NAME --dpxl-expression DPXL-EXPRESSION [--is-active=IS-ACTIVE] [--compression-type COMPRESSION-TYPE] [--ibm-event-streams IBM-EVENT-STREAMS | --ibm-event-streams-brokers IBM-EVENT-STREAMS-BROKERS --ibm-event-streams-topic IBM-EVENT-STREAMS-TOPIC]
```


#### Command options
{: #cloud-logs-event-stream-target-create-cli-options}

`--name` (string)
:   The name of the Event stream. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--dpxl-expression` (string)
:   The DPXL expression of the Event stream. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--is-active` (bool)
:   Whether the event stream is active.

`--compression-type` (string)
:   The compression type of the stream.

    Allowable values are: `unspecified`, `gzip`.

`--ibm-event-streams` ([`IbmEventStreams`](#cli-ibm-event-streams-example-schema))
:   Configuration for IBM Event Streams. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--ibm-event-streams=@path/to/file.json`.

`--ibm-event-streams-brokers` (string)
:   The brokers of the IBM Event Streams. Multiple broker endpoints can be provided as comma separated values. This option provides a value for a sub-field of the JSON option 'ibm-event-streams'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--ibm-event-streams-topic` (string)
:   The topic of the IBM Event Streams. This option provides a value for a sub-field of the JSON option 'ibm-event-streams'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Examples
{: #cloud-logs-event-stream-target-create-examples}

```sh
ibmcloud cloud-logs event-stream-target-create \
    --name 'Live Screen' \
    --dpxl-expression '<v1>contains(kubernetes.labels.CX_AZ, \'eu-west-1\')' \
    --is-active=true \
    --compression-type gzip \
    --ibm-event-streams '{"brokers": "kafka01.example.com:9093", "topic": "live.screen"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs event-stream-target-create \
    --name 'Live Screen' \
    --dpxl-expression '<v1>contains(kubernetes.labels.CX_AZ, \'eu-west-1\')' \
    --is-active=true \
    --compression-type gzip \
    --ibm-event-streams-brokers kafka01.example.com:9093 \
    --ibm-event-streams-topic live.screen
```
{: pre}

#### Default JMESPath
{: #cloud-logs-event-stream-target-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name, ID:id, Status:is_active, Brokers:ibm_event_streams.brokers, DpxlExpression:dpxl_expression, Topic:ibm_event_streams.topic, Compression:compression_type, CreatedAt:created_at, UpdatedAt:updated_at}` |
| Error | Default | - |
|  | Table | `{Name:name, ID:id, Status:is_active, Brokers:ibm_event_streams.brokers, DpxlExpression:dpxl_expression, Topic:ibm_event_streams.topic, Compression:compression_type, CreatedAt:created_at, UpdatedAt:updated_at}` |
| All pages | Default | - |
|  | Table | `{Name:name, ID:id, Status:is_active, Brokers:ibm_event_streams.brokers, DpxlExpression:dpxl_expression, Topic:ibm_event_streams.topic, Compression:compression_type, CreatedAt:created_at, UpdatedAt:updated_at}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs event-stream-target-update`
{: #cloud-logs-cli-event-stream-target-update-command}

Update an Event Stream.

```sh
ibmcloud cloud-logs event-stream-target-update --id ID --name NAME --dpxl-expression DPXL-EXPRESSION [--is-active=IS-ACTIVE] [--compression-type COMPRESSION-TYPE] [--ibm-event-streams IBM-EVENT-STREAMS | --ibm-event-streams-brokers IBM-EVENT-STREAMS-BROKERS --ibm-event-streams-topic IBM-EVENT-STREAMS-TOPIC]
```


#### Command options
{: #cloud-logs-event-stream-target-update-cli-options}

`--id` (int64)
:   The ID of the Event Stream. Required.

    The maximum value is `4294967295`. The minimum value is `0`.

`--name` (string)
:   The name of the Event stream. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--dpxl-expression` (string)
:   The DPXL expression of the Event stream. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--is-active` (bool)
:   Whether the event stream is active.

`--compression-type` (string)
:   The compression type of the stream.

    Allowable values are: `unspecified`, `gzip`.

`--ibm-event-streams` ([`IbmEventStreams`](#cli-ibm-event-streams-example-schema))
:   Configuration for IBM Event Streams. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--ibm-event-streams=@path/to/file.json`.

`--ibm-event-streams-brokers` (string)
:   The brokers of the IBM Event Streams. Multiple broker endpoints can be provided as comma separated values. This option provides a value for a sub-field of the JSON option 'ibm-event-streams'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--ibm-event-streams-topic` (string)
:   The topic of the IBM Event Streams. This option provides a value for a sub-field of the JSON option 'ibm-event-streams'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

#### Examples
{: #cloud-logs-event-stream-target-update-examples}

```sh
ibmcloud cloud-logs event-stream-target-update \
    --id 0 \
    --name 'Live Screen' \
    --dpxl-expression '<v1>contains(kubernetes.labels.CX_AZ, \'eu-west-1\')' \
    --is-active=true \
    --compression-type gzip \
    --ibm-event-streams '{"brokers": "kafka01.example.com:9093", "topic": "live.screen"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs event-stream-target-update \
    --id 0 \
    --name 'Live Screen' \
    --dpxl-expression '<v1>contains(kubernetes.labels.CX_AZ, \'eu-west-1\')' \
    --is-active=true \
    --compression-type gzip \
    --ibm-event-streams-brokers kafka01.example.com:9093 \
    --ibm-event-streams-topic live.screen
```
{: pre}

#### Default JMESPath
{: #cloud-logs-event-stream-target-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name, ID:id, Status:is_active, Brokers:ibm_event_streams.brokers, DpxlExpression:dpxl_expression, Topic:ibm_event_streams.topic, CompressionType:compression_type, CreatedAt:created_at, UpdatedAt:updated_at}` |
| Error | Default | - |
|  | Table | `{Name:name, ID:id, Status:is_active, Brokers:ibm_event_streams.brokers, DpxlExpression:dpxl_expression, Topic:ibm_event_streams.topic, CompressionType:compression_type, CreatedAt:created_at, UpdatedAt:updated_at}` |
| All pages | Default | - |
|  | Table | `{Name:name, ID:id, Status:is_active, Brokers:ibm_event_streams.brokers, DpxlExpression:dpxl_expression, Topic:ibm_event_streams.topic, CompressionType:compression_type, CreatedAt:created_at, UpdatedAt:updated_at}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs event-stream-target-delete`
{: #cloud-logs-cli-event-stream-target-delete-command}

Delete an Event Stream integration by ID.

```sh
ibmcloud cloud-logs event-stream-target-delete --id ID
```


#### Command options
{: #cloud-logs-event-stream-target-delete-cli-options}

`--id` (int64)
:   The ID of the Event Stream. Required.

    The maximum value is `4294967295`. The minimum value is `0`.

#### Example
{: #cloud-logs-event-stream-target-delete-examples}

```sh
ibmcloud cloud-logs event-stream-target-delete \
    --id 0
```
{: pre}

## Views
{: #cloud-logs-views-cli}

Create and manage views.

### `ibmcloud cloud-logs views`
{: #cloud-logs-cli-views-command}

Lists all company public views.

```sh
ibmcloud cloud-logs views
```


#### Example
{: #cloud-logs-views-examples}

```sh
ibmcloud cloud-logs views
```
{: pre}

#### Default JMESPath
{: #cloud-logs-views-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `views[*].{Name:name,ID:id}` |
| Error | Default | - |
|  | Table | `views[*].{Name:name,ID:id}` |
| All pages | Default | - |
|  | Table | `views[*].{Name:name,ID:id}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs view-create`
{: #cloud-logs-cli-view-create-command}

Creates a new view.

```sh
ibmcloud cloud-logs view-create --name NAME [--time-selection TIME-SELECTION | --time-selection-quick-selection TIME-SELECTION-QUICK-SELECTION --time-selection-custom-selection TIME-SELECTION-CUSTOM-SELECTION] [--search-query SEARCH-QUERY  --search-query-syntax-type SEARCH-QUERY-SYNTAX-TYPE] [--filters FILTERS ] [--folder-id FOLDER-ID] [--tier TIER]
```


#### Command options
{: #cloud-logs-view-create-cli-options}

`--name` (string)
:   View name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--time-selection` ([`ApisViewsV1TimeSelection`](#cli-apis-views-v1-time-selection-example-schema))
:   View time selection. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection=@path/to/file.json`.

`--search-query` ([`ApisViewsV1SearchQuery`](#cli-apis-views-v1-search-query-example-schema))
:   View search query. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--search-query=@path/to/file.json`.

`--filters` ([`ApisViewsV1SelectedFilters`](#cli-apis-views-v1-selected-filters-example-schema))
:   View selected filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--folder-id` (strfmt.UUID)
:   View folder ID.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--tier` (string)
:   Type of view.

    Allowable values are: `priority_insights`, `priority_insights_templates`, `all_logs`, `all_logs_templates`.

`--time-selection-quick-selection` ([`ApisViewsV1QuickTimeSelection`](#cli-apis-views-v1-quick-time-selection-example-schema))
:   Quick time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-quick-selection=@path/to/file.json`.

`--time-selection-custom-selection` ([`ApisViewsV1CustomTimeSelection`](#cli-apis-views-v1-custom-time-selection-example-schema))
:   Custom time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-custom-selection=@path/to/file.json`.

`--search-query-query` (string)
:   View search query. This option provides a value for a sub-field of the JSON option 'search-query'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--search-query-syntax-type` (string)
:   Syntax type for the query used in views. This option provides a value for a sub-field of the JSON option 'search-query'. It is mutually exclusive with that option.

    Allowable values are: `lucene`, `dataprime`.

`--filters-filters` ([`ApisViewsV1Filter[]`](#cli-apis-views-v1-filter-example-schema))
:   Selected filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-filters=@path/to/file.json`.

#### Examples
{: #cloud-logs-view-create-examples}

```sh
ibmcloud cloud-logs view-create \
    --name 'Logs view' \
    --time-selection '{"custom_selection": {"from_time": "2024-01-25T11:31:43.152Z", "to_time": "2024-01-25T11:37:13.238Z"}}' \
    --search-query '{"query": "logs", "syntax_type": "dataprime"}' \
    --filters '{"filters": [{"name": "applicationName", "selected_values": {}}]}' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673 \
    --tier all_logs
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs view-create \
    --name 'Logs view' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673 \
    --tier all_logs \
    --time-selection-custom-selection apisViewsV1CustomTimeSelection \
    --search-query-query error \
    --search-query-syntax-type dataprime \
    --filters-filters '[apisViewsV1Filter]'
```
{: pre}

#### Default JMESPath
{: #cloud-logs-view-create-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs view`
{: #cloud-logs-cli-view-command}

Gets a view by ID.

```sh
ibmcloud cloud-logs view --id ID
```


#### Command options
{: #cloud-logs-view-cli-options}

`--id` (int64)
:   View ID. Required.

    The maximum value is `2147483647`. The minimum value is `0`.

#### Example
{: #cloud-logs-view-examples}

```sh
ibmcloud cloud-logs view \
    --id 52
```
{: pre}

#### Default JMESPath
{: #cloud-logs-view-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{Name:name,ID:id}` |
| Error | Default | - |
|  | Table | `{Name:name,ID:id}` |
| All pages | Default | - |
|  | Table | `{Name:name,ID:id}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs view-update`
{: #cloud-logs-cli-view-update-command}

Replaces an existing view.

```sh
ibmcloud cloud-logs view-update --id ID --name NAME [--time-selection TIME-SELECTION | --time-selection-quick-selection TIME-SELECTION-QUICK-SELECTION --time-selection-custom-selection TIME-SELECTION-CUSTOM-SELECTION] [--search-query SEARCH-QUERY  --search-query-syntax-type SEARCH-QUERY-SYNTAX-TYPE] [--filters FILTERS ] [--folder-id FOLDER-ID] [--tier TIER]
```


#### Command options
{: #cloud-logs-view-update-cli-options}

`--id` (int64)
:   View ID. Required.

    The maximum value is `2147483647`. The minimum value is `0`.

`--name` (string)
:   View name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--time-selection` ([`ApisViewsV1TimeSelection`](#cli-apis-views-v1-time-selection-example-schema))
:   View time selection. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection=@path/to/file.json`.

`--search-query` ([`ApisViewsV1SearchQuery`](#cli-apis-views-v1-search-query-example-schema))
:   View search query. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--search-query=@path/to/file.json`.

`--filters` ([`ApisViewsV1SelectedFilters`](#cli-apis-views-v1-selected-filters-example-schema))
:   View selected filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--folder-id` (strfmt.UUID)
:   View folder ID.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--tier` (string)
:   Type of view.

    Allowable values are: `priority_insights`, `priority_insights_templates`, `all_logs`, `all_logs_templates`.

`--time-selection-quick-selection` ([`ApisViewsV1QuickTimeSelection`](#cli-apis-views-v1-quick-time-selection-example-schema))
:   Quick time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-quick-selection=@path/to/file.json`.

`--time-selection-custom-selection` ([`ApisViewsV1CustomTimeSelection`](#cli-apis-views-v1-custom-time-selection-example-schema))
:   Custom time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-custom-selection=@path/to/file.json`.

`--search-query-query` (string)
:   View search query. This option provides a value for a sub-field of the JSON option 'search-query'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[\\p{L}\\p{N}\\p{P}\\p{Z}\\p{S}\\p{M}]+$/`.

`--search-query-syntax-type` (string)
:   Syntax type for the query used in views. This option provides a value for a sub-field of the JSON option 'search-query'. It is mutually exclusive with that option.

    Allowable values are: `lucene`, `dataprime`.

`--filters-filters` ([`ApisViewsV1Filter[]`](#cli-apis-views-v1-filter-example-schema))
:   Selected filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-filters=@path/to/file.json`.

#### Examples
{: #cloud-logs-view-update-examples}

```sh
ibmcloud cloud-logs view-update \
    --id 52 \
    --name 'Logs view' \
    --time-selection '{"custom_selection": {"from_time": "2024-01-25T11:31:43.152Z", "to_time": "2024-01-25T11:37:13.238Z"}}' \
    --search-query '{"query": "logs new", "syntax_type": "lucene"}' \
    --filters '{"filters": [{"name": "applicationName", "selected_values": {}}]}' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673 \
    --tier priority_insights_templates
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud cloud-logs view-update \
    --id 52 \
    --name 'Logs view' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673 \
    --tier priority_insights_templates \
    --time-selection-custom-selection apisViewsV1CustomTimeSelection \
    --search-query-query error \
    --search-query-syntax-type dataprime \
    --filters-filters '[apisViewsV1Filter]'
```
{: pre}

#### Default JMESPath
{: #cloud-logs-view-update-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `views[*].{Name:name,ID:id}` |
| Error | Default | - |
|  | Table | `views[*].{Name:name,ID:id}` |
| All pages | Default | - |
|  | Table | `views[*].{Name:name,ID:id}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud cloud-logs view-delete`
{: #cloud-logs-cli-view-delete-command}

Deletes a view by ID.

```sh
ibmcloud cloud-logs view-delete --id ID
```


#### Command options
{: #cloud-logs-view-delete-cli-options}

`--id` (int64)
:   View ID. Required.

    The maximum value is `2147483647`. The minimum value is `0`.

#### Example
{: #cloud-logs-view-delete-examples}

```sh
ibmcloud cloud-logs view-delete \
    --id 52
```
{: pre}

## Schema examples
{: #cloud-logs-schema-examples}

The following schema examples represent the data that you need to specify for a command option. These examples model the data structure and include placeholder values for the expected value type. When you run a command, replace these values with the values that apply to your environment as appropriate.

### AlertDefinitionPrototype
{: #cli-prototype-example-schema}

The following example shows the format of the AlertDefinitionPrototype object.

```json

{
  "name" : "Alert 1738141279354",
  "description" : "Example Alert definition",
  "enabled" : true,
  "priority" : "p5_or_unspecified",
  "active_on" : {
    "day_of_week" : [ "monday_or_unspecified", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday" ],
    "start_time" : {
      "hours" : 22,
      "minutes" : 30
    },
    "end_time" : {
      "hours" : 22,
      "minutes" : 30
    }
  },
  "type" : "logs_threshold",
  "group_by_keys" : [ ],
  "incidents_settings" : {
    "notify_on" : "triggered_only_unspecified",
    "minutes" : 10
  },
  "notification_group" : {
    "group_by_keys" : [ ],
    "webhooks" : [ {
      "notify_on" : "triggered_and_resolved",
      "integration" : {
        "integration_id" : 123
      },
      "minutes" : 15
    } ]
  },
  "entity_labels" : { },
  "phantom_mode" : false,
  "deleted" : false,
  "logs_threshold" : {
    "logs_filter" : {
      "simple_filter" : {
        "lucene_query" : "text:\"error\"",
        "label_filters" : {
          "application_name" : [ {
            "value" : "my-app",
            "operation" : "starts_with"
          } ],
          "subsystem_name" : [ {
            "value" : "my-app",
            "operation" : "starts_with"
          } ],
          "severities" : [ "verbose_unspecified", "debug", "info", "warning", "error", "critical" ]
        }
      }
    },
    "undetected_values_management" : {
      "trigger_undetected_values" : true,
      "auto_retire_timeframe" : "hours_24"
    },
    "rules" : [ {
      "condition" : {
        "threshold" : 1,
        "time_window" : {
          "logs_time_window_specific_value" : "minutes_10"
        }
      },
      "override" : {
        "priority" : "p5_or_unspecified"
      }
    } ],
    "condition_type" : "more_than_or_unspecified",
    "notification_payload_filter" : [ ],
    "evaluation_delay_ms" : 60000
  }
}
```
{: codeblock}

### AlertsV1AlertActiveTimeframe
{: #cli-alerts-v1-alert-active-timeframe-example-schema}

The following example shows the format of the AlertsV1AlertActiveTimeframe object.

```json

{
  "hours" : 22,
  "minutes" : 22,
  "seconds" : 22
}
```
{: codeblock}

### AlertsV1AlertActiveWhen
{: #cli-alerts-v1-alert-active-when-example-schema}

The following example shows the format of the AlertsV1AlertActiveWhen object.

```json

{
  "timeframes" : [ {
    "days_of_week" : [ "monday_or_unspecified", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday" ],
    "range" : {
      "start" : {
        "hours" : 18,
        "minutes" : 30,
        "seconds" : 0
      },
      "end" : {
        "hours" : 18,
        "minutes" : 30,
        "seconds" : 0
      }
    }
  } ]
}
```
{: codeblock}

### AlertsV1AlertFilters
{: #cli-alerts-v1-alert-filters-example-schema}

The following example shows the format of the AlertsV1AlertFilters object.

```json

{
  "severities" : [ "debug_or_unspecified", "verbose", "info", "warning", "error", "critical" ],
  "metadata" : {
    "applications" : [ "CpuMonitoring", "WebApi" ],
    "subsystems" : [ "SnapshotGenerator", "PermissionControl" ]
  },
  "alias" : "monitorQuery",
  "text" : "initiator.id.keyword:iam-ServiceId-10820fd6-c3fe-414e-8fd5-44ce95f7d34d AND action.keyword:cloud-object-storage.object.create",
  "ratio_alerts" : [ {
    "alias" : "TopLevelAlert",
    "text" : "_exists_:\"container_name\"",
    "severities" : [ "debug_or_unspecified", "verbose", "info", "warning", "error", "critical" ],
    "applications" : [ "CpuMonitoring", "WebApi" ],
    "subsystems" : [ "SnapshotGenerator", "PermissionControl" ],
    "group_by" : [ "Host", "Thread" ]
  } ],
  "filter_type" : "text_or_unspecified"
}
```
{: codeblock}

### AlertsV1AlertFiltersMetadataFilters
{: #cli-alerts-v1-alert-filters-metadata-filters-example-schema}

The following example shows the format of the AlertsV1AlertFiltersMetadataFilters object.

```json

{
  "applications" : [ "CpuMonitoring", "WebApi" ],
  "subsystems" : [ "SnapshotGenerator", "PermissionControl" ]
}
```
{: codeblock}

### AlertsV1AlertFiltersRatioAlert
{: #cli-alerts-v1-alert-filters-ratio-alert-example-schema}

The following example shows the format of the AlertsV1AlertFiltersRatioAlert object.

```json

{
  "alias" : "TopLevelAlert",
  "text" : "_exists_:\"container_name\"",
  "severities" : [ "debug_or_unspecified", "verbose", "info", "warning", "error", "critical" ],
  "applications" : [ "CpuMonitoring", "WebApi" ],
  "subsystems" : [ "SnapshotGenerator", "PermissionControl" ],
  "group_by" : [ "Host", "Thread" ]
}
```
{: codeblock}

### AlertsV1Date
{: #cli-alerts-v1-date-example-schema}

The following example shows the format of the AlertsV1Date object.

```json

{
  "year" : 2012,
  "month" : 12,
  "day" : 24
}
```
{: codeblock}

### AlertsV1MetaLabel[]
{: #cli-alerts-v1-meta-label-example-schema}

The following example shows the format of the AlertsV1MetaLabel[] object.

```json

[ {
  "key" : "env",
  "value" : "dev"
} ]
```
{: codeblock}

### AlertsV2AlertCondition
{: #cli-alerts-v2-alert-condition-example-schema}

The following example shows the format of the AlertsV2AlertCondition object.

```json

{
  "more_than" : {
    "parameters" : {
      "threshold" : 1,
      "timeframe" : "timeframe_10_min",
      "group_by" : [ "coralogix.metadata.applicationName" ],
      "metric_alert_parameters" : {
        "metric_field" : "cpu_usage",
        "metric_source" : "prometheus",
        "arithmetic_operator" : "percentile",
        "arithmetic_operator_modifier" : 1,
        "sample_threshold_percentage" : 100,
        "non_null_percentage" : 100,
        "swap_null_values" : true
      },
      "metric_alert_promql_parameters" : {
        "promql_text" : "sum(rate(container_cpu_usage_seconds_total{container_name=\"my-container\"}[5m])) by (pod_name)",
        "arithmetic_operator_modifier" : 1,
        "sample_threshold_percentage" : 100,
        "non_null_percentage" : 100,
        "swap_null_values" : true
      },
      "ignore_infinity" : true,
      "relative_timeframe" : "hour_or_unspecified",
      "cardinality_fields" : [ ],
      "related_extended_data" : {
        "cleanup_deadman_duration" : "cleanup_deadman_duration_24h",
        "should_trigger_deadman" : true
      }
    },
    "evaluation_window" : "rolling_or_unspecified"
  }
}
```
{: codeblock}

### AlertsV2AlertIncidentSettings
{: #cli-alerts-v2-alert-incident-settings-example-schema}

The following example shows the format of the AlertsV2AlertIncidentSettings object.

```json

{
  "retriggering_period_seconds" : 300,
  "notify_on" : "triggered_only",
  "use_as_notification_settings" : true
}
```
{: codeblock}

### AlertsV2AlertNotificationGroups[]
{: #cli-alerts-v2-alert-notification-groups-example-schema}

The following example shows the format of the AlertsV2AlertNotificationGroups[] object.

```json

[ {
  "group_by_fields" : [ "coralogix.metadata.applicationName" ],
  "notifications" : [ {
    "retriggering_period_seconds" : 60,
    "notify_on" : "triggered_and_resolved",
    "integration_id" : 123
  } ]
} ]
```
{: codeblock}

### AlertsV2FlowCondition
{: #cli-alerts-v2-flow-condition-example-schema}

The following example shows the format of the AlertsV2FlowCondition object.

```json

{
  "id" : "6ad87d32-1613-4cb1-b7e3-d97fee561913",
  "not" : true
}
```
{: codeblock}

### AlertsV2ImmediateConditionEmpty
{: #cli-alerts-v2-immediate-condition-empty-example-schema}

The following example shows the format of the AlertsV2ImmediateConditionEmpty object.

```json

{ }
```
{: codeblock}

### AlertsV2LessThanCondition
{: #cli-alerts-v2-less-than-condition-example-schema}

The following example shows the format of the AlertsV2LessThanCondition object.

```json

{
  "metric_field" : "cpu_usage",
  "metric_source" : "prometheus",
  "arithmetic_operator" : "percentile",
  "arithmetic_operator_modifier" : 1,
  "sample_threshold_percentage" : 100,
  "non_null_percentage" : 100,
  "swap_null_values" : true
}
```
{: codeblock}

### AlertsV2LessThanUsualCondition
{: #cli-alerts-v2-less-than-usual-condition-example-schema}

The following example shows the format of the AlertsV2LessThanUsualCondition object.

```json

{
  "metric_field" : "cpu_usage",
  "metric_source" : "prometheus",
  "arithmetic_operator" : "percentile",
  "arithmetic_operator_modifier" : 1,
  "sample_threshold_percentage" : 100,
  "non_null_percentage" : 100,
  "swap_null_values" : true
}
```
{: codeblock}

### AlertsV2MoreThanCondition
{: #cli-alerts-v2-more-than-condition-example-schema}

The following example shows the format of the AlertsV2MoreThanCondition object.

```json

{
  "metric_field" : "cpu_usage",
  "metric_source" : "prometheus",
  "arithmetic_operator" : "percentile",
  "arithmetic_operator_modifier" : 1,
  "sample_threshold_percentage" : 100,
  "non_null_percentage" : 100,
  "swap_null_values" : true
}
```
{: codeblock}

### AlertsV2MoreThanUsualCondition
{: #cli-alerts-v2-more-than-usual-condition-example-schema}

The following example shows the format of the AlertsV2MoreThanUsualCondition object.

```json

{
  "metric_field" : "cpu_usage",
  "metric_source" : "prometheus",
  "arithmetic_operator" : "percentile",
  "arithmetic_operator_modifier" : 1,
  "sample_threshold_percentage" : 100,
  "non_null_percentage" : 100,
  "swap_null_values" : true
}
```
{: codeblock}

### AlertsV2NewValueCondition
{: #cli-alerts-v2-new-value-condition-example-schema}

The following example shows the format of the AlertsV2NewValueCondition object.

```json

{
  "metric_field" : "cpu_usage",
  "metric_source" : "prometheus",
  "arithmetic_operator" : "percentile",
  "arithmetic_operator_modifier" : 1,
  "sample_threshold_percentage" : 100,
  "non_null_percentage" : 100,
  "swap_null_values" : true
}
```
{: codeblock}

### AlertsV2UniqueCountCondition
{: #cli-alerts-v2-unique-count-condition-example-schema}

The following example shows the format of the AlertsV2UniqueCountCondition object.

```json

{
  "metric_field" : "cpu_usage",
  "metric_source" : "prometheus",
  "arithmetic_operator" : "percentile",
  "arithmetic_operator_modifier" : 1,
  "sample_threshold_percentage" : 100,
  "non_null_percentage" : 100,
  "swap_null_values" : true
}
```
{: codeblock}

### ApisAlertDefinitionActivitySchedule
{: #cli-apis-activity-schedule-example-schema}

The following example shows the format of the ApisAlertDefinitionActivitySchedule object.

```json

{
  "hours" : 14,
  "minutes" : 30
}
```
{: codeblock}

### ApisAlertDefinitionAlertDefIncidentSettings
{: #cli-apis-alert-def-incident-settings-example-schema}

The following example shows the format of the ApisAlertDefinitionAlertDefIncidentSettings object.

```json

{
  "notify_on" : "triggered_and_resolved",
  "minutes" : 30
}
```
{: codeblock}

### ApisAlertDefinitionAlertDefNotificationGroup
{: #cli-apis-alert-def-notification-group-example-schema}

The following example shows the format of the ApisAlertDefinitionAlertDefNotificationGroup object.

```json

{
  "integration_id" : 123
}
```
{: codeblock}

### ApisAlertDefinitionFlowType
{: #cli-apis-flow-type-example-schema}

The following example shows the format of the ApisAlertDefinitionFlowType object.

```json

{
  "id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673",
  "not" : true
}
```
{: codeblock}

### ApisAlertDefinitionLogsAnomalyType
{: #cli-apis-logs-anomaly-type-example-schema}

The following example shows the format of the ApisAlertDefinitionLogsAnomalyType object.

```json

{
  "value" : "my-app",
  "operation" : "starts_with"
}
```
{: codeblock}

### ApisAlertDefinitionLogsImmediateType
{: #cli-apis-logs-immediate-type-example-schema}

The following example shows the format of the ApisAlertDefinitionLogsImmediateType object.

```json

{
  "value" : "my-app",
  "operation" : "starts_with"
}
```
{: codeblock}

### ApisAlertDefinitionLogsNewValueType
{: #cli-apis-logs-new-value-type-example-schema}

The following example shows the format of the ApisAlertDefinitionLogsNewValueType object.

```json

{
  "value" : "my-app",
  "operation" : "starts_with"
}
```
{: codeblock}

### ApisAlertDefinitionLogsRatioThresholdType
{: #cli-apis-logs-ratio-threshold-type-example-schema}

The following example shows the format of the ApisAlertDefinitionLogsRatioThresholdType object.

```json

{
  "value" : "my-app",
  "operation" : "starts_with"
}
```
{: codeblock}

### ApisAlertDefinitionLogsThresholdType
{: #cli-apis-logs-threshold-type-example-schema}

The following example shows the format of the ApisAlertDefinitionLogsThresholdType object.

```json

{
  "value" : "my-app",
  "operation" : "starts_with"
}
```
{: codeblock}

### ApisAlertDefinitionLogsTimeRelativeThresholdType
{: #cli-apis-logs-time-relative-threshold-type-example-schema}

The following example shows the format of the ApisAlertDefinitionLogsTimeRelativeThresholdType object.

```json

{
  "value" : "my-app",
  "operation" : "starts_with"
}
```
{: codeblock}

### ApisAlertDefinitionLogsUniqueCountType
{: #cli-apis-logs-unique-count-type-example-schema}

The following example shows the format of the ApisAlertDefinitionLogsUniqueCountType object.

```json

{
  "value" : "my-app",
  "operation" : "starts_with"
}
```
{: codeblock}

### ApisAlertDefinitionMetricAnomalyType
{: #cli-apis-metric-anomaly-type-example-schema}

The following example shows the format of the ApisAlertDefinitionMetricAnomalyType object.

```json

{
  "promql" : "avg_over_time(metric_name[5m]) > 10"
}
```
{: codeblock}

### ApisAlertDefinitionMetricThresholdType
{: #cli-apis-metric-threshold-type-example-schema}

The following example shows the format of the ApisAlertDefinitionMetricThresholdType object.

```json

{
  "promql" : "avg_over_time(metric_name[5m]) > 10"
}
```
{: codeblock}

### ApisEvents2metricsV2MetricField
{: #cli-apis-events2metrics-v2-metric-field-example-schema}

The following example shows the format of the ApisEvents2metricsV2MetricField object.

```json

{
  "sample_type" : "max"
}
```
{: codeblock}

### ApisEvents2metricsV2MetricLabel
{: #cli-apis-events2metrics-v2-metric-label-example-schema}

The following example shows the format of the ApisEvents2metricsV2MetricLabel object.

```json

{
  "target_label" : "alias_label_name",
  "source_field" : "log_obj.string_value"
}
```
{: codeblock}

### ApisLogs2metricsV2LogsQuery
{: #cli-apis-logs2metrics-v2-logs-query-example-schema}

The following example shows the format of the ApisLogs2metricsV2LogsQuery object.

```json

{
  "lucene" : "log_obj.numeric_field: [50 TO 100]",
  "alias" : "new_query",
  "applicationname_filters" : [ "app_name" ],
  "subsystemname_filters" : [ "sub_name" ],
  "severity_filters" : [ "unspecified", "debug", "verbose", "info", "warning", "error", "critical" ]
}
```
{: codeblock}

### ApisViewsV1CustomTimeSelection
{: #cli-apis-views-v1-custom-time-selection-example-schema}

The following example shows the format of the ApisViewsV1CustomTimeSelection object.

```json

{
  "from_time" : "2024-01-25T11:31:43.152Z",
  "to_time" : "2024-01-25T11:35:43.152Z"
}
```
{: codeblock}

### ApisViewsV1Filter
{: #cli-apis-views-v1-filter-example-schema}

The following example shows the format of the ApisViewsV1Filter object.

```json

{
  "name" : "applicationName",
  "selected_values" : { }
}
```
{: codeblock}

### ApisViewsV1QuickTimeSelection
{: #cli-apis-views-v1-quick-time-selection-example-schema}

The following example shows the format of the ApisViewsV1QuickTimeSelection object.

```json

{
  "caption" : "Last hour",
  "seconds" : 3600
}
```
{: codeblock}

### ApisViewsV1SearchQuery
{: #cli-apis-views-v1-search-query-example-schema}

The following example shows the format of the ApisViewsV1SearchQuery object.

```json

{
  "query" : "logs",
  "syntax_type" : "dataprime"
}
```
{: codeblock}

### ApisViewsV1SelectedFilters
{: #cli-apis-views-v1-selected-filters-example-schema}

The following example shows the format of the ApisViewsV1SelectedFilters object.

```json

{
  "filters" : [ {
    "name" : "applicationName",
    "selected_values" : { }
  } ]
}
```
{: codeblock}

### ApisViewsV1TimeSelection
{: #cli-apis-views-v1-time-selection-example-schema}

The following example shows the format of the ApisViewsV1TimeSelection object.

```json

{
  "custom_selection" : {
    "from_time" : "2024-01-25T11:31:43.152Z",
    "to_time" : "2024-01-25T11:37:13.238Z"
  }
}
```
{: codeblock}

### DataAccessRuleFilter[]
{: #cli-data-access-rule-filter-example-schema}

The following example shows the format of the DataAccessRuleFilter[] object.

```json

[ {
  "entity_type" : "logs",
  "expression" : "<v1> foo == 'bar'"
} ]
```
{: codeblock}

### EnrichmentV1CustomEnrichmentType
{: #cli-enrichment-v1-custom-enrichment-type-example-schema}

The following example shows the format of the EnrichmentV1CustomEnrichmentType object.

```json

{
  "id" : 1
}
```
{: codeblock}

### EnrichmentV1EnrichmentType
{: #cli-enrichment-v1-enrichment-type-example-schema}

The following example shows the format of the EnrichmentV1EnrichmentType object.

```json

{
  "geo_ip" : { }
}
```
{: codeblock}

### EnrichmentV1GeoIpTypeEmpty
{: #cli-enrichment-v1-geo-ip-type-empty-example-schema}

The following example shows the format of the EnrichmentV1GeoIpTypeEmpty object.

```json

{ }
```
{: codeblock}

### EnrichmentV1SuspiciousIpTypeEmpty
{: #cli-enrichment-v1-suspicious-ip-type-empty-example-schema}

The following example shows the format of the EnrichmentV1SuspiciousIpTypeEmpty object.

```json

{ }
```
{: codeblock}

### Event2MetricPrototype
{: #cli-event2-metric-prototype-example-schema}

The following example shows the format of the Event2MetricPrototype object.

```json

{
  "name" : "test em2",
  "description" : "Test Events to Metrics",
  "permutations_limit" : 1,
  "metric_labels" : [ {
    "target_label" : "alias_label_name",
    "source_field" : "log_obj.string_value"
  } ],
  "metric_fields" : [ {
    "target_base_metric_name" : "alias_field_name",
    "source_field" : "log_obj.numeric_field",
    "aggregations" : [ {
      "enabled" : true,
      "agg_type" : "samples",
      "target_metric_name" : "alias_field_name_agg_func",
      "samples" : {
        "sample_type" : "max"
      }
    } ]
  } ],
  "type" : "logs2metrics",
  "logs_query" : {
    "lucene" : "logs",
    "alias" : "new_query",
    "applicationname_filters" : [ "app_name" ],
    "subsystemname_filters" : [ "sub_name" ],
    "severity_filters" : [ "unspecified", "debug", "verbose", "info", "warning", "error", "critical" ]
  }
}
```
{: codeblock}

### IbmEventStreams
{: #cli-ibm-event-streams-example-schema}

The following example shows the format of the IbmEventStreams object.

```json

{
  "brokers" : "kafka01.example.com:9093",
  "topic" : "live.screen"
}
```
{: codeblock}

### OutgoingWebhookPrototype
{: #cli-prototype-example-schema}

The following example shows the format of the OutgoingWebhookPrototype object.

```json

{
  "type" : "ibm_event_notifications",
  "name" : "Event Notifications Integration",
  "url" : "https://example.com",
  "ibm_event_notifications" : {
    "event_notifications_instance_id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673",
    "region_id" : "eu-es",
    "source_id" : "crn:v1:staging:public:logs:eu-gb:a/223af6f4260f42ebe23e95fcddd33cb7:63a3e4be-cb73-4f52-898e-8e93484a70a5::",
    "source_name" : "IBM Cloud Event Notifications",
    "endpoint_type" : "private"
  }
}
```
{: codeblock}

### OutgoingWebhooksV1IbmEventNotificationsConfig
{: #cli-outgoing-webhooks-v1-ibm-event-notifications-config-example-schema}

The following example shows the format of the OutgoingWebhooksV1IbmEventNotificationsConfig object.

```json

{
  "event_notifications_instance_id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673",
  "region_id" : "eu-es",
  "source_id" : "crn:v1:staging:public:logs:eu-gb:a/223af6f4260f42ebe23e95fcddd33cb7:63a3e4be-cb73-4f52-898e-8e93484a70a5::",
  "source_name" : "IBM Cloud Event Notifications",
  "endpoint_type" : "private"
}
```
{: codeblock}

### PolicyBeforePrototype
{: #cli-before-prototype-example-schema}

The following example shows the format of the PolicyBeforePrototype object.

```json

{
  "id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673"
}
```
{: codeblock}

### PolicyPrototype
{: #cli-prototype-example-schema}

The following example shows the format of the PolicyPrototype object.

```json

{
  "name" : "Med_policy",
  "before" : {
    "id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673"
  },
  "description" : "Medium policy",
  "priority" : "type_high",
  "application_rule" : {
    "rule_type_id" : "is",
    "name" : "test"
  },
  "subsystem_rule" : {
    "rule_type_id" : "is",
    "name" : "test"
  },
  "archive_retention_tag" : "Default",
  "enabled" : true,
  "log_rules" : {
    "severities" : [ "debug", "verbose", "info", "warning", "error", "critical" ]
  }
}
```
{: codeblock}

### QuotaV1LogRules
{: #cli-quota-v1-log-rules-example-schema}

The following example shows the format of the QuotaV1LogRules object.

```json

{
  "severities" : [ "debug", "verbose", "info", "warning", "error", "critical" ]
}
```
{: codeblock}

### QuotaV1Rule
{: #cli-quota-v1-rule-example-schema}

The following example shows the format of the QuotaV1Rule object.

```json

{
  "rule_type_id" : "includes",
  "name" : "Rule Name"
}
```
{: codeblock}

### RulesV1CreateRuleGroupRequestCreateRuleSubgroup[]
{: #cli-rules-v1-create-rule-group-request-create-rule-subgroup-example-schema}

The following example shows the format of the RulesV1CreateRuleGroupRequestCreateRuleSubgroup[] object.

```json

[ {
  "rules" : [ {
    "name" : "mysql-parse",
    "description" : "mysql-parse",
    "source_field" : "text",
    "parameters" : {
      "parse_parameters" : {
        "destination_field" : "text",
        "rule" : "(?P<timestamp>[^,]+),(?P<hostname>[^,]+),(?P<username>[^,]+),(?P<ip>[^,]+),(?P<connectionId>[0-9]+),(?P<queryId>[0-9]+),(?P<operation>[^,]+),(?P<database>[^,]+),'?(?P<object>.*)'?,(?P<returnCode>[0-9]+)"
      }
    },
    "enabled" : true,
    "order" : 1
  } ],
  "enabled" : true,
  "order" : 1
} ]
```
{: codeblock}

### RulesV1RuleMatcher[]
{: #cli-rules-v1-rule-matcher-example-schema}

The following example shows the format of the RulesV1RuleMatcher[] object.

```json

[ {
  "subsystem_name" : {
    "value" : "mysql"
  }
} ]
```
{: codeblock}
