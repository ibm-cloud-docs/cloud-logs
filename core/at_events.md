---

copyright:
  years:  2024
lastupdated: "2024-08-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.logs_full_notm}}
{: #at_events}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.logs_full_notm}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Activity tracking events are the same for both {{site.data.keyword.at_full_notm}} and {{site.data.keyword.logs_full_notm}}. Until {{site.data.keyword.at_full_notm}} is no longer supported, {{site.data.keyword.logs_full_notm}} activity tracking events can be routed to both {{site.data.keyword.at_full_notm}} and {{site.data.keyword.logs_full_notm}} by using {{site.data.keyword.atracker_full_notm}}.
{: important}

## Locations where activity tracking events are generated
{: #at-locations}

{{site.data.keyword.logs_full_notm}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}


## Viewing activity tracking events for {{site.data.keyword.logs_full_notm}}
{: #at-viewing}


You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI.](/docs/cloud-logs?topic=cloud-logs-instance-launch)


## List of platform events
{: #at_actions_platform}

The following table lists the activity tracking event actions that the {{site.data.keyword.cloud_notm}} platform generates when {{site.data.keyword.logs_full_notm}} instances are processed.

| Action                                   | Description |
|------------------------------------------|---------|
| `logs.instance.create`           | An event is generated when you provision a service instance. |
| `logs.instance.update`           | An event is generated when you rename a service instance or when you change the service plan. |
| `logs.instance.delete`           | An event is generated when a service instance is deleted. |
| `logs>.instance.schedule_reclaim` | An event is generated when a service instance is pending_reclamation. |
| `logs.instance.restore`          | An event is generated when a service instance is restored. |
{: caption="Actions that generate platform events" caption-side="bottom"}

The following table lists the actions that generate an event for managing service credentials that are associated with a service instance.

| Action                         | Description |
|--------------------------------|---------|
| `logs.key.create` | An event is generated when an API key is created for a service instance through the *Service credentials* section of the service instance UI. |
| `logs.key.delete` | An event is generated when an API key that is associated with a service instance is deleted from the *Service credentials* section of the service instance UI. |
{: caption="Actions that generate service credentials events" caption-side="bottom"}


## Data usage events
{: #at_events_data_usage}

The following tables lists the data usage events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.data-usage.read`	| Getting data-usage for each requested day |
{: caption="Events for data usage" caption-side="top"}


## Scope events
{: #at_events_scope}

The following tables lists the scope events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.user-scope.read` |	Getting details of a scope |
| `logs.user-scope.list` |	Listing scopes |
| `logs.user-scope.create` |	Creating a scope |
| `logs.user-scope.update` |	Updating a scope |
| `logs.user-scope.delete` |	Deleting a scope |
{: caption="Events for scope" caption-side="top"}


## Action events
{: #at_events_action}

The following tables lists the action events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.team-action-config.read` |	Reading team-level actions configuration |
| `logs.team-action-config.create` |	Creating team-level actions configuration |
| `logs.team-action-config.update` |	Updating team-level actions configuration |
| `logs.team-action-config.delete` |	Deleting team-level actions configuration |
| `logs.team-action.execute` |	Running team-level actions |
| `logs.user-action-config.read` |	Reading user-level actions configuration |
| `logs.user-action-config.create` | 	Creating user-level actions configuration |
| `logs.user-action-config.update` |	Updating user-level actions configuration |
| `logs.user-action-config.delete` |	Deleting user-level actions configuration |
| `logs.user-action.execute` |	Running user-level actions |
{: caption="Events for actions" caption-side="top"}


## Alert events
{: #at_events_alert}

The following tables lists the alert events that are generated by {{site.data.keyword.logs_full_notm}}:


| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.alert-config.read` |	Getting an alert |
| `logs.alert-config.read`	 | Searching alerts |
| `logs.alert-config.read` |	Searching anomalies grouped by type |
| `logs.alert-config.read` |	Getting an alert |
| `logs.alert-config.list` |	Listing alerts |
| `logs.alert-config.read` |	Getting alert by unique ID |
| `logs.alert-config.read` |	Getting alert mapping |
| `logs.alert-config.list` |	Getting alert events |
| `logs.alert-config.read` |	Validating an alert |
| `logs.alert-config.read` |	Getting the alert events count by severity |
| `logs.alert-config.read` |	Getting the company alerts limit |
| `logs.alert-config.create` |	Creating an alert |
| `logs.alert-config.update` |	Updating an alert |
| `logs.alert-config.delete` |	Deleting an alert |
| `logs.alert.snooze` |	Snoozing or Unsnoozing an alert |
| `logs.alert-map.config` |	Configuring an alert map |
| `logs.alert-map.read` |	Viewing visualized alerts in the alerts map |
{: caption="Events for alert" caption-side="top"}

## View events
{: #at_events_view}

The following tables lists the view events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.shared-view.list` |	Listing shared views |
| `logs.shared-view.read` |	Viewing a public saved views |
| `logs.shared-view.create` |	Creating a public view |
| `logs.shared-view.update` |	Updating a public view |
| `logs.shared-view.delete` |	Deleting a public saved view |
| `logs.private-view.list` |	Listing private views |
| `logs.private-view.read` |	Viewing private saved views |
| `logs.private-view.create` |	Creating a private view |
| `logs.private-view.update` |	Updating a private view |
| `logs.private-view.delete` |	Deleting a private view |
{: caption="Events for views" caption-side="top"}

## Dashboard events
{: #at_events_dashboard}

The following tables lists the dashboard events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.shared-dashboard.read` |	Getting a dashboard |
| `logs.shared-dashboard.pin` |	Pinning a dashboard |
| `logs.shared-dashboard.unpin` |	Unpinning a dashboard |
| `logs.default-dashboard.set` |	Setting the default home dashboard |
| `logs.default-dashboard.replace` |	Replacing the default dashboard |
| `logs.shared-dashboards.list`	 | Getting the dashboard catalog |
| `logs.shared-dashboard.search` | 	Searching DataPrime |
| `logs.shared-dashboard.create` |	Creating a dashboard |
| `logs.shared-dashboard.update` |	Replacing a dashboard |
| `logs.shared-dashboard.delete` |	Deleting a dashboard |
| `logs.user-dashboard.list` |	Listing private dashboards |
| `logs.user-dashboard.read` |	Viewing a private custom dashboard |
| `logs.user-dashboard.create` |	Creating a private custom dashboard |
| `logs.user-dashboard.update` | 	Updating a private custom dashboard |
| `logs.user-dashboard.delete` |	Deleting a private custom dashboard |
{: caption="Events for dashboards" caption-side="top"}


## DataMap events
{: #at_events_datamap}

The following tables lists the DataMap events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.data-map.read` |	Viewing DataMap configurations |
| `logs.data-map.update` |	Configuring a DataMap |
{: caption="Events for DataMap actions" caption-side="top"}

## TCO policy events
{: #at_events_tco_policy}

The following tables lists the TCO policy events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.logs-tco-policy.read` | 	Getting a policy |
| `logs.logs-tco-policy.create` |	Creating a policy |
| `logs.logs-tco-policy.update` |	Updating a policy |
| `logs.logs-tco-policy.list` |	Getting company policies |
| `logs.logs-tco-policy.delete` |	Deleting a policy |
{: caption="Events for TCO policies" caption-side="top"}

## Enrichment events
{: #at_events_enrichment}

The following tables lists the enrichment events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.geo-enrichment-config.read` |	Viewing geo enrichment configuration |
| `logs.geo-enrichment-config.create` |	Creating geo enrichment configuration |
| `logs.geo-enrichment-config.update`	| Updating geo enrichment configuration |
| `logs.geo-enrichment-config.delete` |	Deleting geo enrichment configuration |
| `logs.security-enrichment-config.read` |	Viewing unified threat intelligence enrichment configuration |
| `logs.security-enrichment-config.create` |	Creating unified threat intelligence enrichment configuration |
| `logs.security-enrichment-config.update` |	Updating unified threat intelligence enrichment configuration |
| `logs.security-enrichment-config.delete` |	Deleting unified threat intelligence enrichment configuration |
| `logs.custom-enrichment-config.read` |	Getting custom enrichment by ID |
| `logs.custom-enrichment-config.list` |	Getting all custom enrichments |
| `logs.custom-enrichment-config.create` |	Creating custom enrichment |
| `logs.custom-enrichment-config.update` |	Updating custom enrichment |
| `logs.custom-enrichment-config.delete` |	Deleting custom enrichment |
| `logs.custom-enrichment-data.read` |	Getting custom enrichment by ID |
| `logs.custom-enrichment-data.read` |	Getting all custom enrichments |
| `logs.custom-enrichment-data.create` |	Creating a custom enrichment |
| `logs.custom-enrichment-data.update` |	Updating a custom enrichment |
| `logs.custom-enrichment-data.delete` |	Deleting custom enrichment |
{: caption="Events for enrichment" caption-side="top"}

## Insight events
{: #at_events_insight}

The following tables lists the insight events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.insight.read` | Searching insights |
{: caption="Events for insights" caption-side="top"}


## Incident events
{: #at_events_incident}

The following tables lists the incident events that are generated by {{site.data.keyword.logs_full_notm}}:


| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.incident.read` |	Getting incident |
| `logs.incident.list` |	Getting incidents list |
| `logs.incident-aggregations.list` |	Listing incident aggregations |
| `logs.incident.acknowledge` |	Acknowledging events in triggered alerts |
| `logs.incident.snooze` |	Snoozing events |
| `logs.incident.assign` |	Assigning incidents |
| `logs.incident.unassign` |	Unassigning incidents |
| `logs.incident.close`	| Closing incidents |
| `logs.incident.resolve` |	Resolving incidents |
{: caption="Events for incidents" caption-side="top"}


## Extension events
{: #at_events_extension}

The following tables lists the extension events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.deployed-extensions.list` |	Getting deployed extensions  |
| `logs.extensions.list` |	Getting all extensions |
| `logs.extension.read` |	Getting extension by ID |
| `logs.extension-quota.list` |	Getting quotas for various extension domains |
| `logs.extension.deploy` |	Deploying an extension |
| `logs.extension.update` |	Updating an extension |
| `logs.extension.delete` |	Removing an extension |
{: caption="Events for extension data" caption-side="top"}

## LiveTail events
{: #at_events_livetail}

The following tables lists the LiveTail events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.livetail.view` | 	Viewing LiveTail data |
{: caption="Events for LiveTail data" caption-side="top"}


## Analytics events
{: #at_events_analytics}

The following tables lists the analytics events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.data-analytics-high.read` |	Viewing {{site.data.keyword.frequent-search}} mapping statistics (Logs) |
| `logs.data-analytics-low.read` |	Viewing archive analytics (Logs) |
{: caption="Events for data analytics" caption-side="top"}


## Log events
{: #at_events_log}

The following tables lists the log events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.logs-timeseries.search`	 | Searching logs time series |
| `logs.events-from-logs.search` |	Searching logs events |
| `logs.aggregated-logs-series.search`|	Searching grouped logs series |
| `logs.aggregated-logs-timeseries.search` |	Searching grouped logs time series |
| `logs.logs-events.search` |	Searching logs event groups |
| `logs.aggregated-logs.search` |	Searching logs aggregated value |
| `logs.logs-activity.search` |	Searching logs activity |
| `logs.data.send` |	Sending Logs |
{: caption="Events for logs" caption-side="top"}

## Archive log events
{: #at_events_archive_log}

The following tables lists the archive log events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.archive-timeseries.search` | Searching archive logs time series |
| `logs.archive-events.search` |	Searching archive logs event groups|
| `logs.aggregated-archive-series.search` |	Searching archive grouped logs series |
| `logs.aggregated-archive-timeseries.search` |	Searching archive grouped logs time series |
| `logs.aggregated-archive-logs.search` |	Searching archive logs aggregated value |
{: caption="Events for archive logs" caption-side="top"}

## Data setup events
{: #at_events_data_setup}

The following tables lists the data setup events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.logs-data-setup-high-config.read` |	Reading configuration to send high tier data |
| `logs.logs-data-setup-high-config.update` |	Updating configuration to send high tier data |
| `logs.logs-data-setup-low-config.read` |	Reading configuration to send low tier data |
| `logs.logs-data-setup-low-config.update` |	Updating configuration to send low tier data |
| `logs.metrics-data-setup-low-config.read` |	Reading metrics archive configuration |
{: caption="Events for data setup" caption-side="top"}


## Parsing rule events
{: #at_events_parsing_rule}

The following tables lists the parsing rule events that are generated by {{site.data.keyword.logs_full_notm}}:


| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.parsing-rule.read` | 	Getting rule group |
| `logs.parsing-rule-usage-limits.read` |	Getting company usage with limits |
| `logs.parsing-rule.create` |	Creating a rule group |
| `logs.parsing-rule.update` |	Updating a rule group |
| `logs.parsing-rule.delete` |	Deleting a rule group |
| `logs.parsing-rules-bulk.delete` |	Bulk deleting rule groups |
{: caption="Events for parsing rules" caption-side="top"}


## Events to Metrics events
{: #at_events_events2metrics}

The following tables lists the Events to Metrics events that are generated by {{site.data.keyword.logs_full_notm}}:


| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.logs-events2metrics-config.read` |	Getting events2metrics configuration |
| `logs.logs-events2metrics-config.unset` |	Disabling events2metrics |
| `logs.logs-events2metrics-config.set` |	Enabling events2metrics |
{: caption="Events for events2metrics" caption-side="top"}

## Benchmark events
{: #at_events_benchmark}

The following tables lists the benchmark events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.version-benchmark-tag.create`	| Creating external tag |
| `logs.version-benchmark-tag.attach`	 | Adding external tag with get |
| `logs.version-benchmark-bitbucket-tag.create` | 	Creating external bitbucket tag |
| `logs.version-benchmark-tfs-tag.create` |	Creating external tfs tag |
| `logs.version-benchmark-gitlab-tag.create` |	Creating external gitlab tag |
| `logs.version-benchmark-tag.create`	 | Creating tag |
| `logs.version-benchmark-tag.update` |	Updating tag |
| `logs.version-benchmark-tag.delete` |	Deleting tag |
| `logs.version-benchmark-tag.list` |	Getting tags |
| `logs.version-benchmark-tag-summary.read` |	Getting tag summary |
| `logs.version-benchmark-tag-alerts.list` |	Getting tag alerts |
| `logs.version-benchmark-tag-error-volume.read` |	Getting tag error volume |
| `logs.version-benchmark-report.view` | Getting benchmark report |
| `logs.version-benchmark-report-private-widget.read` |	Getting private benchmark report |
| `logs.version-benchmark-report-private-widget.create` |	Creating a private benchmark report |
| `logs.version-benchmark-report-private-widget.update` |	Updating a private benchmark report |
| `logs.version-benchmark-report-private-widget.delete` |	Deleting a private benchmark report |
| `logs.version-benchmark-report-private-widget.list` |	Listing private benchmark report |
| `logs.version-benchmark-report-shared-widget.list` |	Listing shared benchmark report |
| `logs.version-benchmark-report-shared-widget.read` |	Getting shared benchmark report |
| `logs.version-benchmark-report-shared-widget.create` |	Creating a shared benchmark report |
| `logs.version-benchmark-report-shared-widget.update` |	Updating a shared benchmark report |
| `logs.version-benchmark-report-shared-widget.delete` |	Deleting a shared benchmark report |
{: caption="Events for benchmarks" caption-side="top"}


## Metrics searching events
{: #at_events_metrics_search}

The following tables lists the metrics searching events that are generated by {{site.data.keyword.logs_full_notm}}:

| Event                                            | Description                |
|---------------------------------------------------|----------------------------|
| `logs.metrics-data-api-high-data.list` | Searching for time series |
| `logs.metrics-data-api-high-data.list` |	Searching for instant values |
| `logs.metrics-data-api-high-data.list` |	Searching for grouped series |
| `logs.metrics-data-api-high-data.list` |	Searching grouped time series |
| `logs.metrics-data-api-high-data.list` |	Searching metrics as events |
| `logs.metrics-data-api-high-data.list` |	Getting the amount of sent metrics |
{: caption="Events for searching metrics data" caption-side="top"}


