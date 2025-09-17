---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-17"

keywords:

subcollection: cloud-logs

---

# {{site.data.keyword.logs_full_notm}} CLI
{: #cloud-logs-cli}

You can use the {{site.data.keyword.logs_full}} command-line interface (CLI) to manage your {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

## Prerequisites
{: #logs-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the {{site.data.keyword.logs_full_notm}} CLI plug-in by running the following command:

    ```text
    ibmcloud plugin install logs
    ```
    {: pre}

    You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
    {: tip}

* To target the {{site.data.keyword.logs_full_notm}} instance, use one of the following options.

    * Run the `ibmcloud logs config set` command.

      ```text
       ibmcloud logs config set service-url https://{instance_ID}.api.{region}.logs.cloud.ibm.com
      ```
      {: pre}


    * Export an environment variable with your {{site.data.keyword.logs_full_notm}} service endpoint URL.

      ```text
      export LOGS_URL=https://{instance_ID}.api.{region}.logs.cloud.ibm.com
      ```
      {: pre}

    * Set the service endpoint in the command.

      ```text
      ibmcloud logs --service-url https://{instance_ID}.api.{region}.logs.cloud.ibm.com
      ```
      {: pre}

    Replace `{instance_ID}` and `{region}` with the values that apply to your {{site.data.keyword.logs_full_notm}} service instance. The endpoint URL that is specific to your instance can be copied from the service details page in the {{site.data.keyword.logs_full_notm}} UI.

## Global configuration commands
{: #cloud-logs-globals}

Global parameters can also be stored in persistent configuration so that they do not need to be manually specified each time the plugin is invoked. Each parameter can be configured with the `config` command and its subcommands.

### `ibmcloud cloud-logs config`
{: #cloud-logs-cli-config-command}

```text
ibmcloud cloud-logs config
```
{: pre}

### `ibmcloud cloud-logs config set`
{: #cloud-logs-cli-config-set-command}

Set a new config value for a specific option. The `value` must be of type string.

```text
ibmcloud cloud-logs config set <option> <value>
```

#### Examples
{: #cloud-logs-config-set-command-examples}

```text
ibmcloud cloud-logs config set service-url \
    'https://ibm.cloud.com/my-api'
```
{: pre}

### `ibmcloud cloud-logs config get`
{: #cloud-logs-cli-config-get-command}

Display the currently set value for a specific option.

```text
ibmcloud cloud-logs config get <option>
```
{: pre}

#### Examples
{: #cloud-logs-config-get-command-examples}

```text
ibmcloud cloud-logs config get service-url
```
{: pre}

### `ibmcloud cloud-logs config unset`
{: #cloud-logs-cli-config-unset-command}

Unset the currently set value for a specific option.

The options available for this service are: `service-url`, .

```text
ibmcloud cloud-logs config unset <option>
```

#### Examples
{: #cloud-logs-config-unset-command-examples}

```text
ibmcloud cloud-logs config unset service-url
```
{: pre}

### `ibmcloud cloud-logs config list`
{: #cloud-logs-cli-config-list-command}

List out all of the currently set config values.

```text
ibmcloud cloud-logs config list
```
{: pre}

#### Examples
{: #cloud-logs-config-list-command-examples}

```text
ibmcloud cloud-logs config list
```
{: pre}

## Alerts
{: #cloud-logs-alerts-cli}

Create and manage alerts.

### `ibmcloud cloud-logs alert`
{: #cloud-logs-cli-alert-command}

Get an alert by ID.

```text
ibmcloud cloud-logs alert --id ID
```


#### Command options
{: #cloud-logs-alert-cli-options}

`--id` (strfmt.UUID)
:   Alert ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-alert-examples}

```text
ibmcloud cloud-logs alert \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs alert-update`
{: #cloud-logs-cli-alert-update-command}

Update an alert.

```text
ibmcloud cloud-logs alert-update --id ID --name NAME --is-active IS-ACTIVE --severity SEVERITY [--condition CONDITION | --condition-immediate CONDITION-IMMEDIATE --condition-less-than CONDITION-LESS-THAN --condition-more-than CONDITION-MORE-THAN --condition-more-than-usual CONDITION-MORE-THAN-USUAL --condition-new-value CONDITION-NEW-VALUE --condition-flow CONDITION-FLOW --condition-unique-count CONDITION-UNIQUE-COUNT --condition-less-than-usual CONDITION-LESS-THAN-USUAL] --notification-groups NOTIFICATION-GROUPS [--filters FILTERS | --filters-severities FILTERS-SEVERITIES --filters-metadata FILTERS-METADATA --filters-alias FILTERS-ALIAS --filters-text FILTERS-TEXT --filters-ratio-alerts FILTERS-RATIO-ALERTS --filters-filter-type FILTERS-FILTER-TYPE] [--description DESCRIPTION] [--expiration EXPIRATION | --expiration-year EXPIRATION-YEAR --expiration-month EXPIRATION-MONTH --expiration-day EXPIRATION-DAY] [--active-when ACTIVE-WHEN | --active-when-timeframes ACTIVE-WHEN-TIMEFRAMES] [--notification-payload-filters NOTIFICATION-PAYLOAD-FILTERS] [--meta-labels META-LABELS] [--meta-labels-strings META-LABELS-STRINGS] [--incident-settings INCIDENT-SETTINGS | --incident-settings-retriggering-period-seconds INCIDENT-SETTINGS-RETRIGGERING-PERIOD-SECONDS --incident-settings-notify-on INCIDENT-SETTINGS-NOTIFY-ON --incident-settings-use-as-notification-settings INCIDENT-SETTINGS-USE-AS-NOTIFICATION-SETTINGS]
```


#### Command options
{: #cloud-logs-alert-update-cli-options}

`--id` (strfmt.UUID)
:   Alert ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--name` (string)
:   Alert name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--is-active` (bool)
:   Alert is active. Required.

`--severity` (string)
:   Alert severity. Required.

    Allowable values are: `info_or_unspecified`, `warning`, `critical`, `error`.

`--condition` ([`AlertsV2AlertCondition`](#cli-alerts-v2-alert-condition-example-schema))
:   Alert condition. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition=@path/to/file.json`.

`--notification-groups` ([`AlertsV2AlertNotificationGroups[]`](#cli-alerts-v2-alert-notification-groups-example-schema))
:   Alert notification groups. Required.

    The maximum length is `10` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--notification-groups=@path/to/file.json`.

`--filters` ([`AlertsV1AlertFilters`](#cli-alerts-v1-alert-filters-example-schema))
:   Alert filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--description` (string)
:   Alert description.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--expiration` ([`AlertsV1Date`](#cli-alerts-v1-date-example-schema))
:   Alert expiration date. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--expiration=@path/to/file.json`.

`--active-when` ([`AlertsV1AlertActiveWhen`](#cli-alerts-v1-alert-active-when-example-schema))
:   When should the alert be active. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when=@path/to/file.json`.

`--notification-payload-filters` ([]string)
:   JSON keys to include in the alert notification, if left empty get the full log text in the alert notification.

    The list items must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`. The maximum length is `100` items. The minimum length is `0` items.

`--meta-labels` ([`AlertsV1MetaLabel[]`](#cli-alerts-v1-meta-label-example-schema))
:   The Meta labels to add to the alert.

    The maximum length is `200` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--meta-labels=@path/to/file.json`.

`--meta-labels-strings` ([]string)
:   The Meta labels to add to the alert as string with ':' separator.

    The list items must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`. The maximum length is `4096` items. The minimum length is `0` items.

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

`--filters-severities` ([]string)
:   The severity of the logs to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable list items are: `debug_or_unspecified`, `verbose`, `info`, `warning`, `error`, `critical`. The maximum length is `4096` items. The minimum length is `0` items.

`--filters-metadata` ([`AlertsV1AlertFiltersMetadataFilters`](#cli-alerts-v1-alert-filters-metadata-filters-example-schema))
:   The metadata filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-metadata=@path/to/file.json`.

`--filters-alias` (string)
:   The alias of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters-text` (string)
:   The text to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters-ratio-alerts` ([`AlertsV1AlertFiltersRatioAlert[]`](#cli-alerts-v1-alert-filters-ratio-alert-example-schema))
:   The ratio alerts. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-ratio-alerts=@path/to/file.json`.

`--filters-filter-type` (string)
:   The type of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable values are: `text_or_unspecified`, `template`, `ratio`, `unique_count`, `time_relative`, `metric`, `flow`.

`--expiration-year` (int64)
:   Year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--expiration-month` (int64)
:   Month of the year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--expiration-day` (int64)
:   Day of the month. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

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

```text
ibmcloud cloud-logs alert-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'Test alert' \
    --is-active true \
    --severity info_or_unspecified \
    --condition '{"more_than": {"parameters": {"threshold": 1, "timeframe": "timeframe_10_min", "group_by": ["coralogix.metadata.applicationName"], "metric_alert_parameters": {"metric_field": "cpu_usage", "metric_source": "prometheus", "arithmetic_operator": "percentile", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "metric_alert_promql_parameters": {"promql_text": "sum(rate(container_cpu_usage_seconds_total{container_name=\"my-container\"}[5m])) by (pod_name)", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "ignore_infinity": true, "relative_timeframe": "hour_or_unspecified", "cardinality_fields": [], "related_extended_data": {"cleanup_deadman_duration": "cleanup_deadman_duration_24h", "should_trigger_deadman": true}}, "evaluation_window": "rolling_or_unspecified"}}' \
    --notification-groups '[{"group_by_fields": ["coralogix.metadata.applicationName"], "notifications": [{"retriggering_period_seconds": 60, "notify_on": "triggered_and_resolved", "integration_id": 123}]}]' \
    --filters '{"severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "metadata": {"applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"]}, "alias": "monitorQuery", "text": "initiator.id.keyword:iam-ServiceId-10820fd6-c3fe-414e-8fd5-44ce95f7d34d AND action.keyword:cloud-object-storage.object.create", "ratio_alerts": [{"alias": "TopLevelAlert", "text": "_exists_:\"container_name\"", "severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"], "group_by": ["Host","Thread"]}], "filter_type": "text_or_unspecified"}' \
    --description 'Alert if the number of logs reaches a threshold' \
    --expiration '{"year": 2012, "month": 12, "day": 24}' \
    --active-when '{"timeframes": [{"days_of_week": ["monday_or_unspecified","tuesday","wednesday","thursday","friday","saturday","sunday"], "range": {"start": {"hours": 18, "minutes": 30, "seconds": 0}, "end": {"hours": 18, "minutes": 30, "seconds": 0}}}]}' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[{"key": "env", "value": "dev"}]' \
    --meta-labels-strings '[]' \
    --incident-settings '{"retriggering_period_seconds": 300, "notify_on": "triggered_only", "use_as_notification_settings": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs alert-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'Test alert' \
    --is-active true \
    --severity info_or_unspecified \
    --notification-groups '[alertsV2AlertNotificationGroups]' \
    --description 'Alert if the number of logs reaches a threshold' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[alertsV1MetaLabel]' \
    --meta-labels-strings '[]' \
    --condition-more-than alertsV2MoreThanCondition \
    --filters-severities debug_or_unspecified,verbose,info,warning,error,critical \
    --filters-metadata alertsV1AlertFiltersMetadataFilters \
    --filters-alias monitorQuery \
    --filters-text _exists_:"container_name" \
    --filters-ratio-alerts '[alertsV1AlertFiltersRatioAlert]' \
    --filters-filter-type flow \
    --expiration-year 2012 \
    --expiration-month 12 \
    --expiration-day 24 \
    --active-when-timeframes '[alertsV1AlertActiveTimeframe]' \
    --incident-settings-retriggering-period-seconds 60 \
    --incident-settings-notify-on triggered_and_resolved \
    --incident-settings-use-as-notification-settings true
```
{: pre}

### `ibmcloud cloud-logs alert-delete`
{: #cloud-logs-cli-alert-delete-command}

Delete an alert.

```text
ibmcloud cloud-logs alert-delete --id ID
```


#### Command options
{: #cloud-logs-alert-delete-cli-options}

`--id` (strfmt.UUID)
:   Alert ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-alert-delete-examples}

```text
ibmcloud cloud-logs alert-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs alerts`
{: #cloud-logs-cli-alerts-command}

List alerts.

```text
ibmcloud cloud-logs alerts
```


#### Example
{: #cloud-logs-alerts-examples}

```text
ibmcloud cloud-logs alerts
```
{: pre}

### `ibmcloud cloud-logs alert-create`
{: #cloud-logs-cli-alert-create-command}

Create an alert.

```text
ibmcloud cloud-logs alert-create --name NAME --is-active IS-ACTIVE --severity SEVERITY [--condition CONDITION | --condition-immediate CONDITION-IMMEDIATE --condition-less-than CONDITION-LESS-THAN --condition-more-than CONDITION-MORE-THAN --condition-more-than-usual CONDITION-MORE-THAN-USUAL --condition-new-value CONDITION-NEW-VALUE --condition-flow CONDITION-FLOW --condition-unique-count CONDITION-UNIQUE-COUNT --condition-less-than-usual CONDITION-LESS-THAN-USUAL] --notification-groups NOTIFICATION-GROUPS [--filters FILTERS | --filters-severities FILTERS-SEVERITIES --filters-metadata FILTERS-METADATA --filters-alias FILTERS-ALIAS --filters-text FILTERS-TEXT --filters-ratio-alerts FILTERS-RATIO-ALERTS --filters-filter-type FILTERS-FILTER-TYPE] [--description DESCRIPTION] [--expiration EXPIRATION | --expiration-year EXPIRATION-YEAR --expiration-month EXPIRATION-MONTH --expiration-day EXPIRATION-DAY] [--active-when ACTIVE-WHEN | --active-when-timeframes ACTIVE-WHEN-TIMEFRAMES] [--notification-payload-filters NOTIFICATION-PAYLOAD-FILTERS] [--meta-labels META-LABELS] [--meta-labels-strings META-LABELS-STRINGS] [--incident-settings INCIDENT-SETTINGS | --incident-settings-retriggering-period-seconds INCIDENT-SETTINGS-RETRIGGERING-PERIOD-SECONDS --incident-settings-notify-on INCIDENT-SETTINGS-NOTIFY-ON --incident-settings-use-as-notification-settings INCIDENT-SETTINGS-USE-AS-NOTIFICATION-SETTINGS]
```


#### Command options
{: #cloud-logs-alert-create-cli-options}

`--name` (string)
:   Alert name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--is-active` (bool)
:   Alert is active. Required.

`--severity` (string)
:   Alert severity. Required.

    Allowable values are: `info_or_unspecified`, `warning`, `critical`, `error`.

`--condition` ([`AlertsV2AlertCondition`](#cli-alerts-v2-alert-condition-example-schema))
:   Alert condition. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition=@path/to/file.json`.

`--notification-groups` ([`AlertsV2AlertNotificationGroups[]`](#cli-alerts-v2-alert-notification-groups-example-schema))
:   Alert notification groups. Required.

    The maximum length is `10` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--notification-groups=@path/to/file.json`.

`--filters` ([`AlertsV1AlertFilters`](#cli-alerts-v1-alert-filters-example-schema))
:   Alert filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--description` (string)
:   Alert description.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--expiration` ([`AlertsV1Date`](#cli-alerts-v1-date-example-schema))
:   Alert expiration date. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--expiration=@path/to/file.json`.

`--active-when` ([`AlertsV1AlertActiveWhen`](#cli-alerts-v1-alert-active-when-example-schema))
:   When should the alert be active. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when=@path/to/file.json`.

`--notification-payload-filters` ([]string)
:   JSON keys to include in the alert notification, if left empty get the full log text in the alert notification.

    The list items must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`. The maximum length is `100` items. The minimum length is `0` items.

`--meta-labels` ([`AlertsV1MetaLabel[]`](#cli-alerts-v1-meta-label-example-schema))
:   The Meta labels to add to the alert.

    The maximum length is `200` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--meta-labels=@path/to/file.json`.

`--meta-labels-strings` ([]string)
:   The Meta labels to add to the alert as string with ':' separator.

    The list items must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`. The maximum length is `4096` items. The minimum length is `0` items.

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

`--filters-severities` ([]string)
:   The severity of the logs to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable list items are: `debug_or_unspecified`, `verbose`, `info`, `warning`, `error`, `critical`. The maximum length is `4096` items. The minimum length is `0` items.

`--filters-metadata` ([`AlertsV1AlertFiltersMetadataFilters`](#cli-alerts-v1-alert-filters-metadata-filters-example-schema))
:   The metadata filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-metadata=@path/to/file.json`.

`--filters-alias` (string)
:   The alias of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters-text` (string)
:   The text to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters-ratio-alerts` ([`AlertsV1AlertFiltersRatioAlert[]`](#cli-alerts-v1-alert-filters-ratio-alert-example-schema))
:   The ratio alerts. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-ratio-alerts=@path/to/file.json`.

`--filters-filter-type` (string)
:   The type of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable values are: `text_or_unspecified`, `template`, `ratio`, `unique_count`, `time_relative`, `metric`, `flow`.

`--expiration-year` (int64)
:   Year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--expiration-month` (int64)
:   Month of the year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--expiration-day` (int64)
:   Day of the month. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

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

```text
ibmcloud cloud-logs alert-create \
    --name 'Test alert' \
    --is-active true \
    --severity info_or_unspecified \
    --condition '{"more_than": {"parameters": {"threshold": 1, "timeframe": "timeframe_10_min", "group_by": ["coralogix.metadata.applicationName"], "metric_alert_parameters": {"metric_field": "cpu_usage", "metric_source": "prometheus", "arithmetic_operator": "percentile", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "metric_alert_promql_parameters": {"promql_text": "sum(rate(container_cpu_usage_seconds_total{container_name=\"my-container\"}[5m])) by (pod_name)", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "ignore_infinity": true, "relative_timeframe": "hour_or_unspecified", "cardinality_fields": [], "related_extended_data": {"cleanup_deadman_duration": "cleanup_deadman_duration_24h", "should_trigger_deadman": true}}, "evaluation_window": "rolling_or_unspecified"}}' \
    --notification-groups '[{"group_by_fields": ["coralogix.metadata.applicationName"], "notifications": [{"retriggering_period_seconds": 60, "notify_on": "triggered_and_resolved", "integration_id": 123}]}]' \
    --filters '{"severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "metadata": {"applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"]}, "alias": "monitorQuery", "text": "initiator.id.keyword:iam-ServiceId-10820fd6-c3fe-414e-8fd5-44ce95f7d34d AND action.keyword:cloud-object-storage.object.create", "ratio_alerts": [{"alias": "TopLevelAlert", "text": "_exists_:\"container_name\"", "severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"], "group_by": ["Host","Thread"]}], "filter_type": "text_or_unspecified"}' \
    --description 'Alert if the number of logs reaches a threshold' \
    --expiration '{"year": 2012, "month": 12, "day": 24}' \
    --active-when '{"timeframes": [{"days_of_week": ["monday_or_unspecified","tuesday","wednesday","thursday","friday","saturday","sunday"], "range": {"start": {"hours": 18, "minutes": 30, "seconds": 0}, "end": {"hours": 18, "minutes": 30, "seconds": 0}}}]}' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[{"key": "env", "value": "dev"}]' \
    --meta-labels-strings '[]' \
    --incident-settings '{"retriggering_period_seconds": 300, "notify_on": "triggered_only", "use_as_notification_settings": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs alert-create \
    --name 'Test alert' \
    --is-active true \
    --severity info_or_unspecified \
    --notification-groups '[alertsV2AlertNotificationGroups]' \
    --description 'Alert if the number of logs reaches a threshold' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[alertsV1MetaLabel]' \
    --meta-labels-strings '[]' \
    --condition-more-than alertsV2MoreThanCondition \
    --filters-severities debug_or_unspecified,verbose,info,warning,error,critical \
    --filters-metadata alertsV1AlertFiltersMetadataFilters \
    --filters-alias monitorQuery \
    --filters-text _exists_:"container_name" \
    --filters-ratio-alerts '[alertsV1AlertFiltersRatioAlert]' \
    --filters-filter-type flow \
    --expiration-year 2012 \
    --expiration-month 12 \
    --expiration-day 24 \
    --active-when-timeframes '[alertsV1AlertActiveTimeframe]' \
    --incident-settings-retriggering-period-seconds 60 \
    --incident-settings-notify-on triggered_and_resolved \
    --incident-settings-use-as-notification-settings true
```
{: pre}

## Rules
{: #cloud-logs-rules-cli}

Create and manage parsing rules.

### `ibmcloud cloud-logs rule-group`
{: #cloud-logs-cli-rule-group-command}

Gets rule group by groupid.

```text
ibmcloud cloud-logs rule-group --id ID
```


#### Command options
{: #cloud-logs-rule-group-cli-options}

`--id` (strfmt.UUID)
:   The group ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-rule-group-examples}

```text
ibmcloud cloud-logs rule-group \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs rule-group-update`
{: #cloud-logs-cli-rule-group-update-command}

Updates rule group by groupid.

```text
ibmcloud cloud-logs rule-group-update --id ID --name NAME --rule-subgroups RULE-SUBGROUPS [--description DESCRIPTION] [--enabled ENABLED] [--rule-matchers RULE-MATCHERS] [--order ORDER]
```


#### Command options
{: #cloud-logs-rule-group-update-cli-options}

`--id` (strfmt.UUID)
:   The group ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--name` (string)
:   The name of the rule group. Required.

    The maximum length is `255` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--rule-subgroups` ([`RulesV1CreateRuleGroupRequestCreateRuleSubgroup[]`](#cli-rules-v1-create-rule-group-request-create-rule-subgroup-example-schema))
:   Rule subgroups. Will try to execute the first rule subgroup, and if not matched will try to match the next one in order. Required.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-subgroups=@path/to/file.json`.

`--description` (string)
:   A description for the rule group, should express what is the rule group purpose.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--enabled` (bool)
:   Whether or not the rule is enabled.

`--rule-matchers` ([`RulesV1RuleMatcher[]`](#cli-rules-v1-rule-matcher-example-schema))
:   Optional rule matchers which if matched will make the rule go through the rule group.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-matchers=@path/to/file.json`.

`--order` (int64)
:   The order in which the rule group will be evaluated. The lower the order, the more priority the group will have. Not providing the order will by default create a group with the last order.

    The maximum value is `4294967295`. The minimum value is `0`.

#### Example
{: #cloud-logs-rule-group-update-examples}

```text
ibmcloud cloud-logs rule-group-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name mysql-extractrule \
    --rule-subgroups '[{"rules": [{"name": "mysql-parse", "description": "mysql-parse", "source_field": "text", "parameters": {"parse_parameters": {"destination_field": "text", "rule": "(?P<timestamp>[^,]+),(?P<hostname>[^,]+),(?P<username>[^,]+),(?P<ip>[^,]+),(?P<connectionId>[0-9]+),(?P<queryId>[0-9]+),(?P<operation>[^,]+),(?P<database>[^,]+),\'?(?P<object>.*)\'?,(?P<returnCode>[0-9]+)"}}, "enabled": true, "order": 1}], "enabled": true, "order": 1}]' \
    --description 'mysql audit logs parser' \
    --enabled true \
    --rule-matchers '[{"subsystem_name": {"value": "mysql"}}]' \
    --order 39
```
{: pre}

### `ibmcloud cloud-logs rule-group-delete`
{: #cloud-logs-cli-rule-group-delete-command}

Deletes rule group by groupid.

```text
ibmcloud cloud-logs rule-group-delete --id ID
```


#### Command options
{: #cloud-logs-rule-group-delete-cli-options}

`--id` (strfmt.UUID)
:   The group ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-rule-group-delete-examples}

```text
ibmcloud cloud-logs rule-group-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs rule-groups`
{: #cloud-logs-cli-rule-groups-command}

Gets all rule groups.

```text
ibmcloud cloud-logs rule-groups
```


#### Example
{: #cloud-logs-rule-groups-examples}

```text
ibmcloud cloud-logs rule-groups
```
{: pre}

### `ibmcloud cloud-logs rule-group-create`
{: #cloud-logs-cli-rule-group-create-command}

Creates rule group.

```text
ibmcloud cloud-logs rule-group-create --name NAME --rule-subgroups RULE-SUBGROUPS [--description DESCRIPTION] [--enabled ENABLED] [--rule-matchers RULE-MATCHERS] [--order ORDER]
```


#### Command options
{: #cloud-logs-rule-group-create-cli-options}

`--name` (string)
:   The name of the rule group. Required.

    The maximum length is `255` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--rule-subgroups` ([`RulesV1CreateRuleGroupRequestCreateRuleSubgroup[]`](#cli-rules-v1-create-rule-group-request-create-rule-subgroup-example-schema))
:   Rule subgroups. Will try to execute the first rule subgroup, and if not matched will try to match the next one in order. Required.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-subgroups=@path/to/file.json`.

`--description` (string)
:   A description for the rule group, should express what is the rule group purpose.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--enabled` (bool)
:   Whether or not the rule is enabled.

`--rule-matchers` ([`RulesV1RuleMatcher[]`](#cli-rules-v1-rule-matcher-example-schema))
:   Optional rule matchers which if matched will make the rule go through the rule group.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-matchers=@path/to/file.json`.

`--order` (int64)
:   The order in which the rule group will be evaluated. The lower the order, the more priority the group will have. Not providing the order will by default create a group with the last order.

    The maximum value is `4294967295`. The minimum value is `0`.

#### Example
{: #cloud-logs-rule-group-create-examples}

```text
ibmcloud cloud-logs rule-group-create \
    --name mysql-extractrule \
    --rule-subgroups '[{"rules": [{"name": "mysql-parse", "description": "mysql-parse", "source_field": "text", "parameters": {"parse_parameters": {"destination_field": "text", "rule": "(?P<timestamp>[^,]+),(?P<hostname>[^,]+),(?P<username>[^,]+),(?P<ip>[^,]+),(?P<connectionId>[0-9]+),(?P<queryId>[0-9]+),(?P<operation>[^,]+),(?P<database>[^,]+),\'?(?P<object>.*)\'?,(?P<returnCode>[0-9]+)"}}, "enabled": true, "order": 1}], "enabled": true, "order": 1}]' \
    --description 'mysql audit logs  parser' \
    --enabled true \
    --rule-matchers '[{"subsystem_name": {"value": "mysql"}}]' \
    --order 39
```
{: pre}

## Outbound Integrations
{: #cloud-logs-outbound-integrations-cli}

Create and manage your Outbound integrations so that you can receive alerts.

### `ibmcloud cloud-logs outgoing-webhooks`
{: #cloud-logs-cli-outgoing-webhooks-command}

List Outbound Integrations.

```text
ibmcloud cloud-logs outgoing-webhooks [--type TYPE]
```


#### Command options
{: #cloud-logs-outgoing-webhooks-cli-options}

`--type` (string)
:   The type of the deployed Outbound Integrations to list.

    Allowable values are: `ibm_event_notifications`.

#### Example
{: #cloud-logs-outgoing-webhooks-examples}

```text
ibmcloud cloud-logs outgoing-webhooks \
    --type ibm_event_notifications
```
{: pre}

### `ibmcloud cloud-logs outgoing-webhook-create`
{: #cloud-logs-cli-outgoing-webhook-create-command}

Create an Outbound Integration.

```text
ibmcloud cloud-logs outgoing-webhook-create [--prototype PROTOTYPE | --type TYPE --name NAME --url URL --ibm-event-notifications IBM-EVENT-NOTIFICATIONS]
```


#### Command options
{: #cloud-logs-outgoing-webhook-create-cli-options}

`--prototype` ([`OutgoingWebhookPrototype`](#cli-outgoing-webhook-prototype-example-schema))
:   The input data of the Outbound Integration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--type` (string)
:   The type of the deployed Outbound Integrations to list. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `ibm_event_notifications`.

`--name` (string)
:   The name of the Outbound Integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--url` (string)
:   The URL of the Outbound Integration. Null for IBM Event Notifications integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--ibm-event-notifications` ([`OutgoingWebhooksV1IbmEventNotificationsConfig`](#cli-outgoing-webhooks-v1-ibm-event-notifications-config-example-schema))
:   The configuration of the IBM Event Notifications Outbound Integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--ibm-event-notifications=@path/to/file.json`.

#### Examples
{: #cloud-logs-outgoing-webhook-create-examples}

```text
ibmcloud cloud-logs outgoing-webhook-create \
    --prototype '{"type": "ibm_event_notifications", "name": "Event Notifications Integration", "url": "https://example.com", "ibm_event_notifications": {"event_notifications_instance_id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "region_id": "eu-es", "source_id": "crn:v1:staging:public:logs:eu-gb:a/223af6f4260f42ebe23e95fcddd33cb7:63a3e4be-cb73-4f52-898e-8e93484a70a5::", "source_name": "IBM Cloud Event Notifications"}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs outgoing-webhook-create \
    --type ibm_event_notifications \
    --name 'Event Notifications Integration' \
    --url https://example.com \
    --ibm-event-notifications outgoingWebhooksV1IbmEventNotificationsConfig
```
{: pre}

### `ibmcloud cloud-logs outgoing-webhook`
{: #cloud-logs-cli-command}

Gets an Outbound Integration by ID.

```text
ibmcloud cloud-logs outgoing-webhook --id ID
```


#### Command options
{: #cloud-logs-cli-options}

`--id` (strfmt.UUID)
:   The ID of the Outbound Integration to delete. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-examples}

```text
ibmcloud cloud-logs outgoing-webhook \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660
```
{: pre}

### `ibmcloud cloud-logs outgoing-webhook-update`
{: #cloud-logs-cli-outgoing-webhook-update-command}

Update an Outbound Integration.

```text
ibmcloud cloud-logs outgoing-webhook-update --id ID [--prototype PROTOTYPE | --type TYPE --name NAME --url URL --ibm-event-notifications IBM-EVENT-NOTIFICATIONS]
```


#### Command options
{: #cloud-logs-outgoing-webhook-update-cli-options}

`--id` (strfmt.UUID)
:   The ID of the Outbound Integration to delete. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--prototype` ([`OutgoingWebhookPrototype`](#cli-outgoing-webhook-prototype-example-schema))
:   The input data of the Outbound Integration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--type` (string)
:   The type of the deployed Outbound Integrations to list. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `ibm_event_notifications`.

`--name` (string)
:   The name of the Outbound Integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--url` (string)
:   The URL of the Outbound Integration. Null for IBM Event Notifications integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--ibm-event-notifications` ([`OutgoingWebhooksV1IbmEventNotificationsConfig`](#cli-outgoing-webhooks-v1-ibm-event-notifications-config-example-schema))
:   The configuration of the IBM Event Notifications Outbound Integration. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--ibm-event-notifications=@path/to/file.json`.

#### Examples
{: #cloud-logs-outgoing-webhook-update-examples}

```text
ibmcloud cloud-logs outgoing-webhook-update \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660 \
    --prototype '{"type": "ibm_event_notifications", "name": "Event Notifications Integration", "url": "https://example.com", "ibm_event_notifications": {"event_notifications_instance_id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "region_id": "eu-es", "source_id": "crn:v1:staging:public:logs:eu-gb:a/223af6f4260f42ebe23e95fcddd33cb7:63a3e4be-cb73-4f52-898e-8e93484a70a5::", "source_name": "IBM Cloud Event Notifications"}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs outgoing-webhook-update \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660 \
    --type ibm_event_notifications \
    --name 'Event Notifications Integration' \
    --url https://example.com \
    --ibm-event-notifications outgoingWebhooksV1IbmEventNotificationsConfig
```
{: pre}

### `ibmcloud cloud-logs outgoing-webhook-delete`
{: #cloud-logs-cli-outgoing-webhook-delete-command}

Delete an Outbound Integration.

```text
ibmcloud cloud-logs outgoing-webhook-delete --id ID
```


#### Command options
{: #cloud-logs-outgoing-webhook-delete-cli-options}

`--id` (strfmt.UUID)
:   The ID of the Outbound Integration to delete. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-outgoing-webhook-delete-examples}

```text
ibmcloud cloud-logs outgoing-webhook-delete \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660
```
{: pre}

## Policies
{: #cloud-logs-policies-cli}

Create and manage TCO policies.

### `ibmcloud cloud-logs policy`
{: #cloud-logs-cli-command}

Gets policy by id.

```text
ibmcloud cloud-logs policy --id ID
```


#### Command options
{: #cloud-logs-cli-options}

`--id` (strfmt.UUID)
:   ID of policy. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-examples}

```text
ibmcloud cloud-logs policy \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs policy-update`
{: #cloud-logs-cli-policy-update-command}

Updates an existing policy.

```text
ibmcloud cloud-logs policy-update --id ID [--prototype PROTOTYPE | --name NAME --description DESCRIPTION --priority PRIORITY --application-rule APPLICATION-RULE --subsystem-rule SUBSYSTEM-RULE --archive-retention ARCHIVE-RETENTION --log-rules LOG-RULES]
```


#### Command options
{: #cloud-logs-policy-update-cli-options}

`--id` (strfmt.UUID)
:   ID of policy. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--prototype` ([`PolicyPrototype`](#cli-policy-prototype-example-schema))
:   Create policy request. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--name` (string)
:   Policy name. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--description` (string)
:   Policy description. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--priority` (string)
:   The data pipeline sources that match the policy rules will go through. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `type_unspecified`, `type_block`, `type_low`, `type_medium`, `type_high`.

`--application-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching with application. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--application-rule=@path/to/file.json`.

`--subsystem-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching with application. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--subsystem-rule=@path/to/file.json`.

`--archive-retention` ([`QuotaV1ArchiveRetention`](#cli-quota-v1-archive-retention-example-schema))
:   Archive retention definition. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--archive-retention=@path/to/file.json`.

`--log-rules` ([`QuotaV1LogRules`](#cli-quota-v1-log-rules-example-schema))
:   Log rules. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--log-rules=@path/to/file.json`.

#### Examples
{: #cloud-logs-policy-update-examples}

```text
ibmcloud cloud-logs policy-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --prototype '{"name": "Med_policy", "description": "Medium policy", "priority": "type_high", "application_rule": {"rule_type_id": "is", "name": "test"}, "subsystem_rule": {"rule_type_id": "is", "name": "test"}, "archive_retention": {"id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "log_rules": {"severities": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs policy-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'My Policy' \
    --description 'My Policy Description' \
    --priority type_high \
    --application-rule quotaV1Rule \
    --subsystem-rule quotaV1Rule \
    --archive-retention quotaV1ArchiveRetention \
    --log-rules quotaV1LogRules
```
{: pre}

### `ibmcloud cloud-logs policy-delete`
{: #cloud-logs-cli-policy-delete-command}

Deletes an existing policy.

```text
ibmcloud cloud-logs policy-delete --id ID
```


#### Command options
{: #cloud-logs-policy-delete-cli-options}

`--id` (strfmt.UUID)
:   ID of policy. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-policy-delete-examples}

```text
ibmcloud cloud-logs policy-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs policies`
{: #cloud-logs-cli-policies-command}

Gets policies.

```text
ibmcloud cloud-logs policies [--enabled-only ENABLED-ONLY] [--source-type SOURCE-TYPE]
```


#### Command options
{: #cloud-logs-policies-cli-options}

`--enabled-only` (bool)
:   Optionally filter only enabled policies.

`--source-type` (string)
:   Source type to filter policies by.

    Allowable values are: `unspecified`, `logs`.

#### Example
{: #cloud-logs-policies-examples}

```text
ibmcloud cloud-logs policies \
    --enabled-only true \
    --source-type logs
```
{: pre}

### `ibmcloud cloud-logs policy-create`
{: #cloud-logs-cli-policy-create-command}

Creates a new policy.

```text
ibmcloud cloud-logs policy-create [--prototype PROTOTYPE | --name NAME --description DESCRIPTION --priority PRIORITY --application-rule APPLICATION-RULE --subsystem-rule SUBSYSTEM-RULE --archive-retention ARCHIVE-RETENTION --log-rules LOG-RULES]
```


#### Command options
{: #cloud-logs-policy-create-cli-options}

`--prototype` ([`PolicyPrototype`](#cli-policy-prototype-example-schema))
:   Create policy request. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--prototype=@path/to/file.json`.

`--name` (string)
:   Policy name. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--description` (string)
:   Policy description. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--priority` (string)
:   The data pipeline sources that match the policy rules will go through. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Allowable values are: `type_unspecified`, `type_block`, `type_low`, `type_medium`, `type_high`.

`--application-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching with application. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--application-rule=@path/to/file.json`.

`--subsystem-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching with application. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--subsystem-rule=@path/to/file.json`.

`--archive-retention` ([`QuotaV1ArchiveRetention`](#cli-quota-v1-archive-retention-example-schema))
:   Archive retention definition. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--archive-retention=@path/to/file.json`.

`--log-rules` ([`QuotaV1LogRules`](#cli-quota-v1-log-rules-example-schema))
:   Log rules. This option provides a value for a sub-field of the JSON option 'prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--log-rules=@path/to/file.json`.

#### Examples
{: #cloud-logs-policy-create-examples}

```text
ibmcloud cloud-logs policy-create \
    --prototype '{"name": "Med_policy", "description": "Medium Policy", "priority": "type_high", "application_rule": {"rule_type_id": "is", "name": "test"}, "subsystem_rule": {"rule_type_id": "is", "name": "test"}, "archive_retention": {"id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "log_rules": {"severities": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs policy-create \
    --name 'My Policy' \
    --description 'My Policy Description' \
    --priority type_high \
    --application-rule quotaV1Rule \
    --subsystem-rule quotaV1Rule \
    --archive-retention quotaV1ArchiveRetention \
    --log-rules quotaV1LogRules
```
{: pre}

## Events to metrics
{: #cloud-logs-events-to-metrics-cli}

Create and manage your events to metrics definitions.

### `ibmcloud cloud-logs events2metrics-list`
{: #cloud-logs-cli-events2metrics-list-command}

Lists event to metrics definitions.

```text
ibmcloud cloud-logs events2metrics-list
```

#### Aliases
{: #e2n-aliases}

`events2metrics-list`, `e2m-list`

#### Example
{: #cloud-logs-events2metrics-list-examples}

```text
ibmcloud cloud-logs events2metrics-list
```
{: pre}

### `ibmcloud cloud-logs events2metrics-create`
{: #cloud-logs-cli-events2metrics-create-command}

Creates event to metrics definitions.

```text
ibmcloud cloud-logs events2metrics-create [--event2-metric-prototype EVENT2-METRIC-PROTOTYPE | --event2-metric-name EVENT2-METRIC-NAME --event2-metric-description EVENT2-METRIC-DESCRIPTION --event2-metric-permutations-limit EVENT2-METRIC-PERMUTATIONS-LIMIT --event2-metric-metric-labels EVENT2-METRIC-METRIC-LABELS --event2-metric-metric-fields EVENT2-METRIC-METRIC-FIELDS --event2-metric-type EVENT2-METRIC-TYPE --event2-metric-logs-query EVENT2-METRIC-LOGS-QUERY]
```

#### Aliases

`events2metrics-create`, `e2m-create`

#### Command options
{: #cloud-logs-events2metrics-create-cli-options}

`--event2-metric-prototype` ([`Event2MetricPrototype`](#cli-event2-metric-prototype-example-schema))
:   E2M Create message. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-prototype=@path/to/file.json`.

`--event2-metric-name` (string)
:   Name of E2M to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--event2-metric-description` (string)
:   Description of E2M to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--event2-metric-permutations-limit` (int64)
:   The permutation limit of the E2M. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

`--event2-metric-metric-labels` ([`ApisEvents2metricsV2MetricLabel[]`](#cli-apis-events2metrics-v2-metric-label-example-schema))
:   E2M metric labels. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-labels=@path/to/file.json`.

`--event2-metric-metric-fields` ([`ApisEvents2metricsV2MetricField[]`](#cli-apis-events2metrics-v2-metric-field-example-schema))
:   E2M metric fields. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-fields=@path/to/file.json`.

`--event2-metric-type` (string)
:   E2M type. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `logs2metrics`.

`--event2-metric-logs-query` ([`ApisLogs2metricsV2LogsQuery`](#cli-apis-logs2metrics-v2-logs-query-example-schema))
:   E2M logs query. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-logs-query=@path/to/file.json`.

#### Examples
{: #cloud-logs-events2metrics-create-examples}

```text
ibmcloud cloud-logs events2metrics-create \
    --event2-metric-prototype '{"name": "test em2", "description": "Test e2m", "permutations_limit": 1, "metric_labels": [{"target_label": "alias_label_name", "source_field": "log_obj.string_value"}], "metric_fields": [{"target_base_metric_name": "alias_field_name", "source_field": "log_obj.numeric_field", "aggregations": [{"enabled": true, "agg_type": "samples", "target_metric_name": "alias_field_name_agg_func", "samples": {"sample_type": "max"}}]}], "type": "logs2metrics", "logs_query": {"lucene": "logs", "alias": "new_query", "applicationname_filters": ["app_name"], "subsystemname_filters": ["sub_name"], "severity_filters": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
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

### `ibmcloud cloud-logs events2metrics`
{: #cloud-logs-cli-events2metrics-command}

Gets event to metrics definitions by id.

```text
ibmcloud cloud-logs events2metrics --id ID
```

#### Aliases

`events2metrics`, `e2m`

#### Command options
{: #cloud-logs-events2metrics-cli-options}

`--id` (string)
:   ID of e2m to be deleted. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-events2metrics-examples}

```text
ibmcloud cloud-logs events2metrics \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09
```
{: pre}

### `ibmcloud cloud-logs events2metrics-update`
{: #cloud-logs-cli-events2metrics-update-command}

Updates event to metrics definitions.

```text
ibmcloud cloud-logs events2metrics-update --id ID [--event2-metric-prototype EVENT2-METRIC-PROTOTYPE | --event2-metric-name EVENT2-METRIC-NAME --event2-metric-description EVENT2-METRIC-DESCRIPTION --event2-metric-permutations-limit EVENT2-METRIC-PERMUTATIONS-LIMIT --event2-metric-metric-labels EVENT2-METRIC-METRIC-LABELS --event2-metric-metric-fields EVENT2-METRIC-METRIC-FIELDS --event2-metric-type EVENT2-METRIC-TYPE --event2-metric-logs-query EVENT2-METRIC-LOGS-QUERY]
```

#### Aliases

`events2metrics-update`, `e2m-update`

#### Command options
{: #cloud-logs-events2metrics-update-cli-options}

`--id` (string)
:   ID of e2m to be deleted. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--event2-metric-prototype` ([`Event2MetricPrototype`](#cli-event2-metric-prototype-example-schema))
:   E2M Create message. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-prototype=@path/to/file.json`.

`--event2-metric-name` (string)
:   Name of E2M to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--event2-metric-description` (string)
:   Description of E2M to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--event2-metric-permutations-limit` (int64)
:   The permutation limit of the E2M. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

`--event2-metric-metric-labels` ([`ApisEvents2metricsV2MetricLabel[]`](#cli-apis-events2metrics-v2-metric-label-example-schema))
:   E2M metric labels. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-labels=@path/to/file.json`.

`--event2-metric-metric-fields` ([`ApisEvents2metricsV2MetricField[]`](#cli-apis-events2metrics-v2-metric-field-example-schema))
:   E2M metric fields. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-fields=@path/to/file.json`.

`--event2-metric-type` (string)
:   E2M type. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `logs2metrics`.

`--event2-metric-logs-query` ([`ApisLogs2metricsV2LogsQuery`](#cli-apis-logs2metrics-v2-logs-query-example-schema))
:   E2M logs query. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-logs-query=@path/to/file.json`.

#### Examples
{: #cloud-logs-events2metrics-update-examples}

```text
ibmcloud cloud-logs events2metrics-update \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09 \
    --event2-metric-prototype '{"name": "test em2", "description": "Test e2m updated", "permutations_limit": 1, "metric_labels": [{"target_label": "alias_label_name", "source_field": "log_obj.string_value"}], "metric_fields": [{"target_base_metric_name": "alias_field_name", "source_field": "log_obj.numeric_field", "aggregations": [{"enabled": true, "agg_type": "samples", "target_metric_name": "alias_field_name_agg_func", "samples": {"sample_type": "max"}}]}], "type": "logs2metrics", "logs_query": {"lucene": "logs", "alias": "new_query", "applicationname_filters": ["app_name"], "subsystemname_filters": ["sub_name"], "severity_filters": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
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

### `ibmcloud cloud-logs events2metrics-delete`
{: #cloud-logs-cli-events2metrics-delete-command}

Deletes event to metrics definitions by id.

```text
ibmcloud cloud-logs events2metrics-delete --id ID
```

#### Aliases

`events2metrics-delete`, `e2m-delete`

#### Command options
{: #cloud-logs-events2metrics-delete-cli-options}

`--id` (string)
:   ID of e2m to be deleted. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-events2metrics-delete-examples}

```text
ibmcloud cloud-logs events2metrics-delete \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09
```
{: pre}

## Views
{: #cloud-logs-views-cli}

Create and manage views.

### `ibmcloud cloud-logs views`
{: #cloud-logs-cli-views-command}

Lists all company public views.

```text
ibmcloud cloud-logs views
```


#### Example
{: #cloud-logs-views-examples}

```text
ibmcloud cloud-logs views
```
{: pre}

### `ibmcloud cloud-logs view-create`
{: #cloud-logs-cli-view-create-command}

Creates a new view.

```text
ibmcloud cloud-logs view-create --name NAME [--time-selection TIME-SELECTION | --time-selection-quick-selection TIME-SELECTION-QUICK-SELECTION --time-selection-custom-selection TIME-SELECTION-CUSTOM-SELECTION] [--search-query SEARCH-QUERY ] [--filters FILTERS ] [--folder-id FOLDER-ID]
```


#### Command options
{: #cloud-logs-view-create-cli-options}

`--name` (string)
:   View name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

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

`--time-selection-quick-selection` ([`ApisViewsV1QuickTimeSelection`](#cli-apis-views-v1-quick-time-selection-example-schema))
:   Quick time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-quick-selection=@path/to/file.json`.

`--time-selection-custom-selection` ([`ApisViewsV1CustomTimeSelection`](#cli-apis-views-v1-custom-time-selection-example-schema))
:   Custom time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-custom-selection=@path/to/file.json`.

#### Examples
{: #cloud-logs-view-create-examples}

```text
ibmcloud cloud-logs view-create \
    --name 'Logs view' \
    --time-selection '{"custom_selection": {"from_time": "2024-01-25T11:31:43.152Z", "to_time": "2024-01-25T11:37:13.238Z"}}' \
    --search-query '{"query": "logs"}' \
    --filters '{"filters": [{"name": "applicationName", "selected_values": {}}]}' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs view-create \
    --name 'Logs view' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673 \
    --time-selection-custom-selection apisViewsV1CustomTimeSelection \
    --search-query-query error \
    --filters-filters '[apisViewsV1Filter]'
```
{: pre}

### `ibmcloud cloud-logs view`
{: #cloud-logs-cli-view-command}

Gets a view by ID.

```text
ibmcloud cloud-logs view --id ID
```


#### Command options
{: #cloud-logs-view-cli-options}

`--id` (int64)
:   View ID. Required.

#### Example
{: #cloud-logs-view-examples}

```text
ibmcloud cloud-logs view \
    --id 52
```
{: pre}

### `ibmcloud cloud-logs view-update`
{: #cloud-logs-cli-view-update-command}

Replaces an existing view.

```text
ibmcloud cloud-logs view-update --id ID --name NAME [--time-selection TIME-SELECTION | --time-selection-quick-selection TIME-SELECTION-QUICK-SELECTION --time-selection-custom-selection TIME-SELECTION-CUSTOM-SELECTION] [--search-query SEARCH-QUERY ] [--filters FILTERS ] [--folder-id FOLDER-ID]
```


#### Command options
{: #cloud-logs-view-update-cli-options}

`--id` (int64)
:   View ID. Required.

`--name` (string)
:   View name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

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

`--time-selection-quick-selection` ([`ApisViewsV1QuickTimeSelection`](#cli-apis-views-v1-quick-time-selection-example-schema))
:   Quick time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-quick-selection=@path/to/file.json`.

`--time-selection-custom-selection` ([`ApisViewsV1CustomTimeSelection`](#cli-apis-views-v1-custom-time-selection-example-schema))
:   Custom time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-custom-selection=@path/to/file.json`.


#### Examples
{: #cloud-logs-view-update-examples}

```text
ibmcloud cloud-logs view-update \
    --id 52 \
    --name 'Logs view' \
    --time-selection '{"custom_selection": {"from_time": "2024-01-25T11:31:43.152Z", "to_time": "2024-01-25T11:37:13.238Z"}}' \
    --search-query '{"query": "logs new"}' \
    --filters '{"filters": [{"name": "applicationName", "selected_values": {}}]}' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs view-update \
    --id 52 \
    --name 'Logs view' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673 \
    --time-selection-custom-selection apisViewsV1CustomTimeSelection \
    --search-query-query error \
    --filters-filters '[apisViewsV1Filter]'
```
{: pre}

### `ibmcloud cloud-logs view-delete`
{: #cloud-logs-cli-view-delete-command}

Deletes a view by ID.

```text
ibmcloud cloud-logs view-delete --id ID
```


#### Command options
{: #cloud-logs-view-delete-cli-options}

`--id` (int64)
:   View ID. Required.

#### Example
{: #cloud-logs-view-delete-examples}

```text
ibmcloud cloud-logs view-delete \
    --id 52
```
{: pre}

## Folders for views
{: #cloud-logs-folders-for-views-cli}

Create and manage view folders.

### `ibmcloud cloud-logs view-folders`
{: #cloud-logs-cli-view-folders-command}

List view's folders.

```text
ibmcloud cloud-logs view-folders
```


#### Example
{: #cloud-logs-view-folders-examples}

```text
ibmcloud cloud-logs view-folders
```
{: pre}

### `ibmcloud cloud-logs view-folder-create`
{: #cloud-logs-cli-view-folder-create-command}

Create view folder.

```text
ibmcloud cloud-logs view-folder-create --name NAME
```


#### Command options
{: #cloud-logs-view-folder-create-cli-options}

`--name` (string)
:   View folder name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-view-folder-create-examples}

```text
ibmcloud cloud-logs view-folder-create \
    --name 'My Folder'
```
{: pre}

### `ibmcloud cloud-logs view-folder`
{: #cloud-logs-cli-view-folder-command}

Get view folder.

```text
ibmcloud cloud-logs view-folder --id ID
```


#### Command options
{: #cloud-logs-view-folder-cli-options}

`--id` (strfmt.UUID)
:   Folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-view-folder-examples}

```text
ibmcloud cloud-logs view-folder \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs view-folder-update`
{: #cloud-logs-cli-view-folder-update-command}

Replaces an existing view folder.

```text
ibmcloud cloud-logs view-folder-update --id ID --name NAME
```


#### Command options
{: #cloud-logs-view-folder-update-cli-options}

`--id` (strfmt.UUID)
:   Folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--name` (string)
:   View folder name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-view-folder-update-examples}

```text
ibmcloud cloud-logs view-folder-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'My Folder'
```
{: pre}

### `ibmcloud cloud-logs view-folder-delete`
{: #cloud-logs-cli-view-folder-delete-command}

Deletes a view folder by ID.

```text
ibmcloud cloud-logs view-folder-delete --id ID
```


#### Command options
{: #cloud-logs-view-folder-delete-cli-options}

`--id` (strfmt.UUID)
:   Folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-view-folder-delete-examples}

```text
ibmcloud cloud-logs view-folder-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

## Data access rules
{: #cloud-logs-data-access-rules-cli}

Create and manage Data Access Rules.

### `ibmcloud cloud-logs data-access-rules`
{: #cloud-logs-cli-data-access-rules-command}

List service instance's Data Access Rules with provided ids.

```text
ibmcloud cloud-logs data-access-rules [--id ID]
```


#### Command options
{: #cloud-logs-data-access-rules-cli-options}

`--id` ([]strfmt.UUID)
:   Array of data access rule IDs.

    The list items must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`. The maximum length is `4096` items. The minimum length is `0` items.

#### Example
{: #cloud-logs-data-access-rules-examples}

```text
ibmcloud cloud-logs data-access-rules \
    --id 4f966911-4bda-407e-b069-477394effa59
```
{: pre}

### `ibmcloud cloud-logs data-access-rule-create`
{: #cloud-logs-cli-data-access-rule-create-command}

Create a Data Access Rule.

```text
ibmcloud cloud-logs data-access-rule-create --display-name DISPLAY-NAME --filters FILTERS --default-expression DEFAULT-EXPRESSION [--description DESCRIPTION]
```


#### Command options
{: #cloud-logs-data-access-rule-create-cli-options}

`--display-name` (string)
:   Display Name for new Data Access Rule. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters` ([`DataAccessRuleFilter[]`](#cli-data-access-rule-filter-example-schema))
:   Filters for new Data Access Rule. Required.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--default-expression` (string)
:   Default Expression for new Data Access Rule. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|'<> ]+$/`.

`--description` (string)
:   Description for new Data Access Rule.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

#### Example
{: #cloud-logs-data-access-rule-create-examples}

```text
ibmcloud cloud-logs data-access-rule-create \
    --display-name 'Test Data Access Rule' \
    --filters '[{"entity_type": "logs", "expression": "<v1> foo == \'bar\'"}]' \
    --default-expression '<v1>true' \
    --description 'Data Access Rule intended for testing'
```
{: pre}

### `ibmcloud cloud-logs data-access-rule-update`
{: #cloud-logs-cli-data-access-rule-update-command}

Update a Data Access Rule.

```text
ibmcloud cloud-logs data-access-rule-update --id ID --display-name DISPLAY-NAME --filters FILTERS --default-expression DEFAULT-EXPRESSION [--description DESCRIPTION]
```


#### Command options
{: #cloud-logs-data-access-rule-update-cli-options}

`--id` (strfmt.UUID)
:   ID of Data Access Rule to be deleted. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--display-name` (string)
:   Display Name for new Data Access Rule. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters` ([`DataAccessRuleFilter[]`](#cli-data-access-rule-filter-example-schema))
:   Filters for new Data Access Rule. Required.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--default-expression` (string)
:   Default Expression for new Data Access Rule. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|'<> ]+$/`.

`--description` (string)
:   Description for new Data Access Rule.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

#### Example
{: #cloud-logs-data-access-rule-update-examples}

```text
ibmcloud cloud-logs data-access-rule-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --display-name 'Test Data Access Rule' \
    --filters '[{"entity_type": "logs", "expression": "<v1> foo == \'bar\'"}]' \
    --default-expression '<v1>true' \
    --description 'Data Access Rule intended for testing'
```
{: pre}

### `ibmcloud cloud-logs data-access-rule-delete`
{: #cloud-logs-cli-data-access-rule-delete-command}

Delete a Data Access Rule.

```text
ibmcloud cloud-logs data-access-rule-delete --id ID
```


#### Command options
{: #cloud-logs-data-access-rule-delete-cli-options}

`--id` (strfmt.UUID)
:   ID of Data Access Rule to be deleted. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-data-access-rule-delete-examples}

```text
ibmcloud cloud-logs data-access-rule-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

## Enrichments
{: #cloud-logs-enrichments-cli}

Create and manage enrichments.

### `ibmcloud cloud-logs enrichments`
{: #cloud-logs-cli-enrichments-command}

List all enrichments.

```text
ibmcloud cloud-logs enrichments
```


#### Example
{: #cloud-logs-enrichments-examples}

```text
ibmcloud cloud-logs enrichments
```
{: pre}

### `ibmcloud cloud-logs enrichment-create`
{: #cloud-logs-cli-enrichment-create-command}

Create an enrichment.

```text
ibmcloud cloud-logs enrichment-create --field-name FIELD-NAME [--enrichment-type ENRICHMENT-TYPE | --enrichment-type-geo-ip ENRICHMENT-TYPE-GEO-IP --enrichment-type-suspicious-ip ENRICHMENT-TYPE-SUSPICIOUS-IP --enrichment-type-custom-enrichment ENRICHMENT-TYPE-CUSTOM-ENRICHMENT]
```


#### Command options
{: #cloud-logs-enrichment-create-cli-options}

`--field-name` (string)
:   The name of the field to enrich. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--enrichment-type` ([`EnrichmentV1EnrichmentType`](#cli-enrichment-v1-enrichment-type-example-schema))
:   The enrichment type. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enrichment-type=@path/to/file.json`.

`--enrichment-type-geo-ip` ([`EnrichmentV1GeoIpTypeEmpty`](#cli-enrichment-v1-geo-ip-type-empty-example-schema))
:   The geo ip enrichment. This option provides a value for a sub-field of the JSON option 'enrichment-type'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enrichment-type-geo-ip=@path/to/file.json`.

`--enrichment-type-suspicious-ip` ([`EnrichmentV1SuspiciousIpTypeEmpty`](#cli-enrichment-v1-suspicious-ip-type-empty-example-schema))
:   The suspicious ip enrichment. This option provides a value for a sub-field of the JSON option 'enrichment-type'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enrichment-type-suspicious-ip=@path/to/file.json`.

`--enrichment-type-custom-enrichment` ([`EnrichmentV1CustomEnrichmentType`](#cli-enrichment-v1-custom-enrichment-type-example-schema))
:   The custom enrichment. This option provides a value for a sub-field of the JSON option 'enrichment-type'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enrichment-type-custom-enrichment=@path/to/file.json`.

#### Examples
{: #cloud-logs-enrichment-create-examples}

```text
ibmcloud cloud-logs enrichment-create \
    --field-name ip \
    --enrichment-type '{"geo_ip": {}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs enrichment-create \
    --field-name ip \
    --enrichment-type-geo-ip enrichmentV1GeoIpTypeEmpty
```
{: pre}

### `ibmcloud cloud-logs enrichment-delete`
{: #cloud-logs-cli-enrichment-delete-command}

Delete enrichments.

```text
ibmcloud cloud-logs enrichment-delete --id ID
```


#### Command options
{: #cloud-logs-enrichment-delete-cli-options}

`--id` (int64)
:   The enrichment ID. Required.

    The maximum value is `4294967295`. The minimum value is `0`.

#### Example
{: #cloud-logs-enrichment-delete-examples}

```text
ibmcloud cloud-logs enrichment-delete \
    --id 1
```
{: pre}

## Data usage metrics
{: #cloud-logs-data-usage-metrics-cli}

Data usage service.

### `ibmcloud cloud-logs data-usage-metrics-export-status`
{: #cloud-logs-cli-data-usage-metrics-export-status-command}

Get data usage metrics export status.

```text
ibmcloud cloud-logs data-usage-metrics-export-status
```


#### Example
{: #cloud-logs-data-usage-metrics-export-status-examples}

```text
ibmcloud cloud-logs data-usage-metrics-export-status
```
{: pre}

### `ibmcloud cloud-logs data-usage-metrics-export-status-update`
{: #cloud-logs-cli-data-usage-metrics-export-status-update-command}

Update data usage metrics export status.

```text
ibmcloud cloud-logs data-usage-metrics-export-status-update --enabled ENABLED
```


#### Command options
{: #cloud-logs-data-usage-metrics-export-status-update-cli-options}

`--enabled` (bool)
:   The "enabled" parameter for metrics export. Required.

#### Example
{: #cloud-logs-data-usage-metrics-export-status-update-examples}

```text
ibmcloud cloud-logs data-usage-metrics-export-status-update \
    --enabled true
```
{: pre}

## QueryService
{: #cloud-logs-query-service-cli}

Query and process your logs.

### `ibmcloud cloud-logs query`
{: #cloud-logs-cli-query-command}

Run a query to search the logs.

```text
ibmcloud cloud-logs query --query QUDATAPRIME_OR_LUCENE_QUERY [--metadata METADATA | --start-date START-DATE --end-date END-DATE --default-source DEFAULT-SOURCE --tier TIER --syntax SYNTAX --limit LIMIT --strict-fields-validation STRICT-FIELDS-VALIDATION] [--since SINCE] [--local-time LOCAL-TIME]
```

#### Command options
{: #cloud-logs-query-cli-options}

`--query` (string)
:   The query for which you are seeking results. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--metadata` ([`ApisDataprimeV1Metadata`](#cli-apis-dataprime-v1-metadata-example-schema))
:   Configuration for query execution. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--metadata=@path/to/file.json`.

`--start-date` (strfmt.DateTime)
:   Beginning of the time range for the query. Default: end - 15 min or current time - 15 min if end is not defined. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--end-date` (strfmt.DateTime)
:   End of the time range for the query. Default: start + 15 min or current time if start is not defined. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--default-source` (string)
:   Default value for the source to be used when the source is omitted in a query. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--tier` (string)
:   Tier on which the query runs. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `archive`, `frequent_search`.

`--syntax` (string)
:   The syntax in which the query is written. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `lucene`, `dataprime`.

`--limit` (int64)
:   Limit the number of results. Default: 2000; max for TIER_FREQUENT_SEARCH: 12000; max for TIER_ARCHIVE: 50000. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--strict-fields-validation` (bool)
:   Prohibit the use of unknown fields, i.e., those not detected in the ingested data. Default: false. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--since` (duration)
: Query lookback window. Default 1h. Using this flag overrides metadata-start-date and metadata-end-date.

`--local-time` (bool)
: Converts the timestamp of the logs to local time.

#### Examples
{: #cloud-logs-query-examples}

```text
ibmcloud cloud-logs query \
    --query 'source logs | filter $d.apiVersion == 42' \
    --metadata '{"start_date": "2021-01-01T00:00:00.000Z", "end_date": "2021-01-01T00:00:00.000Z", "default_source": "logs", "tier": "frequent_search", "syntax": "dataprime", "limit": 2000, "strict_fields_validation": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:

```text
ibmcloud cloud-logs query \
    --query 'source logs | filter $d.apiVersion == 42' \
    --start-date 2021-01-01T00:00:00.000Z \
    --end-date 2021-01-01T00:00:00.000Z \
    --default-source logs \
    --tier frequent_search \
    --syntax dataprime \
    --limit 2000 \
    --strict-fields-validation true
```
{: pre}

## Schema examples
{: #cloud-logs-schema-examples}

The following schema examples represent the data that you need to specify for a command option. These examples model the data structure and include placeholder values for the expected value type. When you run a command, replace these values with the values that apply to your environment as appropriate.

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

### ApisLogs2metricsV2LogsQuery
{: #cli-apis-logs2metrics-v2-logs-query-example-schema}

The following example shows the format of the ApisLogs2metricsV2LogsQuery object.

```json

{
  "lucene" : "logs",
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
  "to_time" : "2024-01-25T11:37:13.238Z"
}
```
{: codeblock}

### ApisViewsV1SearchQuery
{: #cli-apis-views-v1-search-query-example-schema}

The following example shows the format of the ApisViewsV1SearchQuery object.

```json

{
  "query" : "logs"
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

### Event2MetricPrototype
{: #cli-event2-metric-prototype-example-schema}

The following example shows the format of the Event2MetricPrototype object.

```json

{
  "name" : "test em2",
  "description" : "Test e2m",
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

### OutgoingWebhookPrototype
{: #cli-outgoing-webhook-prototype-example-schema}

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
    "source_name" : "IBM Cloud Event Notifications"
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
  "source_name" : "IBM Cloud Event Notifications"
}
```
{: codeblock}

### PolicyPrototype
{: #cli-policy-prototype-example-schema}

The following example shows the format of the PolicyPrototype object.

```json

{
  "name" : "Med_policy",
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
  "archive_retention" : {
    "id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673"
  },
  "log_rules" : {
    "severities" : [ "unspecified", "debug", "verbose", "info", "warning", "error", "critical" ]
  }
}
```
{: codeblock}

### QuotaV1ArchiveRetention
{: #cli-quota-v1-archive-retention-example-schema}

The following example shows the format of the QuotaV1ArchiveRetention object.

```json

{
  "id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673"
}
```
{: codeblock}

### QuotaV1LogRules
{: #cli-quota-v1-log-rules-example-schema}

The following example shows the format of the QuotaV1LogRules object.

```json

{
  "severities" : [ "unspecified", "debug", "verbose", "info", "warning", "error", "critical" ]
}
```
{: codeblock}

### QuotaV1Rule
{: #cli-quota-v1-rule-example-schema}

The following example shows the format of the QuotaV1Rule object.

```json

{
  "rule_type_id" : "is",
  "name" : "test"
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
