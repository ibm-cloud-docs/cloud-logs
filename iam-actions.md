---

copyright:
  years:  2024
lastupdated: "2024-11-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# IAM actions by role
{: #iam-actions}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.cloud_notm}}. Access to {{site.data.keyword.logs_full_notm}} instances for users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Different roles allow for different actions.
{: shortdesc}

## Manager role
{: #iam-actions-manager}

| Action | Description |
|--------|------------|
| `logs.data-usage.read` | View instance data usage metrics. |
| `logs.data-usage.manage` |	Manage instance data usage metrics. |
| `logs.data-usage.export` |	Export data usage. |
| `logs.team-members.read` |	Read the list of users. |
| `logs.data-access-restriction-rule.read` |	Read scopes. |
| `logs.data-access-restriction-rule.manage` |	Manage scopes. |
| `logs.shared-action.read` |	Read shared actions. |
| `logs.shared-action.manage` |	Manage shared actions. |
| `logs.shared-action.execute` |	Run shared actions. |
| `logs.private-action.read` |	Read private actions. |
| `logs.private-action.manage` |	Manage private actions. |
| `logs.private-action.execute` |	Run private actions. |
| `logs.alert-config.read` |	Read alert definitions. |
| `logs.alert-config.manage` |	Manage alert definitions. |
| `logs.alert.snooze` |	Snooze or unsnooze an alert. |
| `logs.logs-alert.read` |	Read logs alerts definitions. |
| `logs.logs-alert.manage` |	Manage logs alerts definitions. |
| `logs.metrics-alert.read` |	Read metrics alerts definitions. |
| `logs.metrics-alert.manage` |	Define and modify metrics alerts settings. |
| `logs.alerts-map.read` |	View visualized alerts in alerts map. |
| `logs.shared-view.read` |	Read shared views. |
| `logs.shared-view.manage` |	Manage shared views. |
| `logs.private-view.read` |	Read private views. |
| `logs.private-view.manage` |	Manage private views. |
| `logs.shared-dashboard.read` |	View custom shared dashboard widgets. |
| `logs.shared-dashboard.manage` |	Manage custom shared dashboard widgets. |
| `logs.private-dashboard.read` |	View custom private dashboard widgets. |
| `logs.private-dashboard.manage` |	Manage custom private dashboard widgets. |
| `logs.data-map.read` |	Read DataMap configurations. |
| `logs.data-map.manage` |	Manage DataMap configurations. |
| `logs.logs-tco-policy.read` |	View existing logs TCO policies. |
| `logs.logs-tco-policy.manage` |	View and modify existing logs TCO policies and create new ones. |
| `logs.geo-enrichment.read` |	Read geo-enrichment configuration. |
| `logs.geo-enrichment.manage` |	Manage geo-enrichment configuration. |
| `logs.security-enrichment.read` |	Read security enrichment configuration. |
| `logs.security-enrichment.manage` |	Manage security enrichment configuration. |
| `logs.custom-enrichment.read` |	Read custom enrichment configuration. |
| `logs.custom-enrichment.manage` |	Manage custom enrichment configuration. |
| `logs.custom-enrichment-data.read` |	Read data for custom enrichment configuration. |
| `logs.custom-enrichment-data.manage` |	Manage data for custom enrichment configuration. |
| `logs.incident.read` |	View events in triggered alerts. |
| `logs.incident.acknowledge` |	Acknowledge events in triggered alerts. |
| `logs.incident.snooze` |	Snooze events in triggered alerts. |
| `logs.incident.assign` |	Assign an event in triggered alerts. |
| `logs.incident.close` |	Manually resolve events in triggered alerts. |
| `logs.extension.read` |	View extension packages. |
| `logs.extension.manage` |	Deploy, undeploy, and update extension packages. |
| `logs.livetail.read` |	Read livetail data. |
| `logs.logs-data-analytics-high.read` |	Read analytics data for logs in high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.logs-data-analytics-low.read` |	Read analytics data for logs in low-tier ({{site.data.keyword.compliance}}). |
| `logs.metrics-data-analytics-high.read` |	Read analytics of metrics in the form of mapping statistics in the high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.metrics-data-analytics-low.read` |	Read analytics of metrics in the form of mapping statistics in the low-tier ({{site.data.keyword.compliance}}). |
| `logs.logs-data-api-high.read` |	Query logs in the high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.logs-data-api-low.read` |	Query logs in the low-tier ({{site.data.keyword.compliance}}). |
| `logs.metrics-data-api-high.read` |	Query metrics in the high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.metrics-data-api-low.read` |	Query metrics in the low-tier ({{site.data.keyword.compliance}}). |
| `logs.data-ingress.send` |	Send logs data. |
| `logs.parsing-rule.read` |	Read parsing rules. |
| `logs.parsing-rule.manage` |	Create, modify, and remove parsing rules. |
| `logs.events2metrics.read` |	View Events to Metrics configuration when the source input is logs. |
| `logs.events2metrics.manage` |	Configure or modify the configuration for Events to Metrics, when the source input is logs. |
| `logs.version-benchmark-tags.manage` |	Manage version benchmark tags. |
| `logs.version-benchmark-tags.read` |	Read version benchmark tags. |
| `logs.version-benchmark-report.read` |	Read version benchmark reports. |
| `logs.suppression-rule.read` |	Read suppression rules. |
| `logs.suppression-rule.manage` |	Manage suppression rules. |
| `logs.webhook.read` |	View generic outbound webhooks configuration. |
| `logs.webhook.manage` |	Create and modify the configuration for outbound webhooks. |
| `logs.legacy-archive-query.execute` |	Query data from the archive. |
| `logs.legacy-archive-query.reindex` |	Re-index archive queries. |
{: caption="IAM actions available for the Manager role" caption-side="top"}


## Writer role
{: #iam-actions-writer}

| Action | Description |
|--------|------------|
| `logs.data-usage.read` | View instance data usage metrics. |
| `logs.data-usage.export` |	Export data usage. |
| `logs.data-access-restriction-rule.read` |	Read scopes. |
| `logs.shared-action.read` |	Read shared actions. |
| `logs.shared-action.manage` |	Manage shared actions. |
| `logs.shared-action.execute` |	Run shared actions. |
| `logs.private-action.read` |	Read private actions. |
| `logs.private-action.manage` |	Manage private actions. |
| `logs.private-action.execute` |	Run private actions. |
| `logs.alert-config.read` |	Read alert definitions. |
| `logs.alert-config.manage` |	Manage alert definitions. |
| `logs.alert.snooze` |	Snooze or unsnooze an alert. |
| `logs.logs-alert.read` |	Read logs alerts definitions. |
| `logs.logs-alert.manage` |	Manage logs alerts definitions. |
| `logs.metrics-alert.read` |	Read metrics alerts definitions. |
| `logs.metrics-alert.manage` |	Define and modify metrics alerts settings. |
| `logs.alerts-map.read` |	View visualized alerts in alerts map. |
| `logs.shared-view.read` |	Read shared views. |
| `logs.shared-view.manage` |	Manage shared views. |
| `logs.private-view.read` |	Read private views. |
| `logs.private-view.manage` |	Manage private views. |
| `logs.shared-dashboard.read` |	View custom shared dashboard widgets. |
| `logs.shared-dashboard.manage` |	Manage custom shared dashboard widgets. |
| `logs.private-dashboard.read` |	View custom private dashboard widgets. |
| `logs.private-dashboard.manage` |	Manage custom private dashboard widgets. |
| `logs.data-map.read` |	Read DataMap configurations. |
| `logs.data-map.manage` |	Manage DataMap configurations. |
| `logs.logs-tco-policy.read` |	View existing logs TCO policies. |
| `logs.geo-enrichment.read` |	Read geo-enrichment configuration. |
| `logs.security-enrichment.read` |	Read security enrichment configuration. |
| `logs.custom-enrichment.read` |	Read custom enrichment configuration. |
| `logs.custom-enrichment.manage` |	Manage custom enrichment configuration. |
| `logs.custom-enrichment-data.read` |	Read data for custom enrichment configuration. |
| `logs.custom-enrichment-data.manage` |	Manage data for custom enrichment configuration. |
| `logs.incident.read` |	View events in triggered alerts. |
| `logs.incident.acknowledge` |	Acknowledge events in triggered alerts. |
| `logs.incident.snooze` |	Snooze events in triggered alerts. |
| `logs.incident.assign` |	Assign an event in triggered alerts. |
| `logs.incident.close` |	Manually resolve events in triggered alerts. |
| `logs.extension.read` |	View extension packages. |
| `logs.extension.manage` |	Deploy, undeploy, and update extension packages. |
| `logs.livetail.read` |	Read livetail data. |
| `logs.logs-data-analytics-high.read` |	Read analytics data for logs in high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.logs-data-analytics-low.read` |	Read analytics data for logs in low-tier ({{site.data.keyword.compliance}}). |
| `logs.metrics-data-analytics-high.read` |	Read analytics of metrics in the form of mapping statistics in the high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.metrics-data-analytics-low.read` |	Read analytics of metrics in the form of mapping statistics in the low-tier ({{site.data.keyword.compliance}}). |
| `logs.logs-data-api-high.read` |	Query logs in the high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.logs-data-api-low.read` |	Query logs in the low-tier ({{site.data.keyword.compliance}}). |
| `logs.metrics-data-api-high.read` |	Query metrics in the high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.metrics-data-api-low.read` |	Query metrics in the low-tier ({{site.data.keyword.compliance}}). |
| `logs.data-ingress.send` |	Send logs data. |
| `logs.parsing-rule.read` |	Read parsing rules. |
| `logs.parsing-rule.manage` |	Create, modify, and remove parsing rules. |
| `logs.events2metrics.read` |	View Events to Metrics configuration when the source input is logs. |
| `logs.version-benchmark-tags.read` |	Read version benchmark tags. |
| `logs.version-benchmark-report.read` |	Read version benchmark reports. |
| `logs.suppression-rule.read` |	Read suppression rules. |
| `logs.suppression-rule.manage` |	Manage suppression rules. |
| `logs.webhook.read` |	View generic outbound webhooks configuration. |
| `logs.webhook.manage` |	Create and modify the configuration for outbound webhooks. |
| `logs.legacy-archive-query.execute` |	Query data from the archive. |
| `logs.legacy-archive-query.reindex` |	Re-index archive queries. |
{: caption="IAM actions available for the Writer role" caption-side="top"}

## Reader role
{: #iam-actions-reader}

| Action | Description |
|--------|------------|
| `logs.data-usage.read` | View instance data usage metrics. |
| `logs.shared-action.read` |	Read shared actions. |
| `logs.shared-action.execute` |	Run shared actions. |
| `logs.alert-config.read` |	Read alert definitions. |
| `logs.logs-alert.read` |	Read logs alerts definitions. |
| `logs.metrics-alert.read` |	Read metrics alerts definitions. |
| `logs.alerts-map.read` |	View visualized alerts in alerts map. |
| `logs.shared-view.read` |	Read shared views. |
| `logs.shared-dashboard.read` |	View custom shared dashboard widgets. |
| `logs.data-map.read` |	Read DataMap configurations. |
| `logs.custom-enrichment-data.read` |	Read data for custom enrichment configuration. |
| `logs.incident.read` |	View events in triggered alerts. |
| `logs.livetail.read` |	Read livetail data. |
| `logs.logs-data-api-high.read` |	Query logs in the high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.logs-data-api-low.read` |	Query logs in the low-tier ({{site.data.keyword.compliance}}). |
| `logs.metrics-data-api-high.read` |	Query metrics in the high-tier ({{site.data.keyword.frequent-search}}). |
| `logs.metrics-data-api-low.read` |	Query metrics in the low-tier ({{site.data.keyword.compliance}}). |
| `logs.version-benchmark-tags.read` |	Read version benchmark tags. |
| `logs.version-benchmark-report.read` |	Read version benchmark reports. |
| `logs.suppression-rule.read` |	Read suppression rules. |
| `logs.webhook.read` |	View generic outbound webhooks configuration. |
| `logs.legacy-archive-query.execute` |	Query data from the archive. |
{: caption="IAM actions available for the Reader role" caption-side="top"}


## Sender role
{: #iam-actions-sender}

| Action | Description |
|--------|------------|
| `logs.data-ingress.send` |	Send logs data. |
{: caption="IAM actions available for the Sender role" caption-side="top"}


##  Data Access Reader role
{: #iam-actions-DataAccessRestrictionReader}

| Action | Description |
|--------|------------|
| `logs.data-access-restriction.read` |	Access the scope. |
{: caption="IAM actions available for the DataAccessRestrictionReader role" caption-side="top"}
