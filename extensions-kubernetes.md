---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-20"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.containerlong_notm}} extension
{: #extensions-kubernetes}

In {{site.data.keyword.logs_full_notm}}, you can use the {{site.data.keyword.containerlong_notm}} extension to gain insights into logs that are generated in an {{site.data.keyword.cloud_notm}} account.
{: shortdesc}


## Before you begin
{: #extensions-kubernetes-overview}

With this extension, you can create a dashboard designed to visualize and analyze logs from the {{site.data.keyword.containerlong_notm}} service. The dashboard provides an in-depth analysis of the {{site.data.keyword.containerlong_notm}} service, offering a comprehensive view of cluster performance, node activity, pod logs, and error analysis. It enables quick issue identification, trend analysis, and efficient Kubernetes monitoring.

In {{site.data.keyword.logs_full_notm}}, logs that are generated by {{site.data.keyword.cloud_notm}} services (known as platform logs) include metadata fields that you can use to enhance searches and analyze the data.
- `applicationName`: The application name is the environment that produces and sends logs to {{site.data.keyword.logs_full_notm}}. It is set to `kubernetes.namespace_name`.
- `subsystemName`: The subsystem name is the service or application that produces and sends logs to {{site.data.keyword.logs_full_notm}}. It is set to `kubernetes.container_name:<container>` where `<container>` is the {{site.data.keyword.containerlong_notm}} container name.

In {{site.data.keyword.cloud_notm}}, you must configure {{site.data.keyword.logs_routing_full_notm}} to route logs to the {{site.data.keyword.logs_full_notm}} service.

Before you can monitor logs that are generated in an {{site.data.keyword.cloud_notm}} account, you must configure the {{site.data.keyword.logs_routing_full_notm}} service in the account to define the destination where you want to monitor the logs.

- You can configure 1 or more {{site.data.keyword.logs_full_notm}} instances in the account.
- Platform logs generated in the region are routed to the {{site.data.keyword.logs_full_notm}} instance configured in {{site.data.keyword.logs_routing_full_notm}}. The {{site.data.keyword.logs_full_notm}} instance can be in the same region, or in a different region, in the account.
- You must define a service to service authorization between {{site.data.keyword.logs_routing_full_notm}} and {{site.data.keyword.logs_full_notm}} to grant permissions to the {{site.data.keyword.logs_routing_full_notm}} service to send logs to the {{site.data.keyword.logs_full_notm}} service.

For more information, see:
- [Getting started with {{site.data.keyword.logs_routing_full_notm}}](/docs/logs-router?topic=logs-router-getting-started)
- [{{site.data.keyword.containerlong_notm}} logging](/docs/containers?topic=containers-health)

## What this extension deploys
{: #extensions-kubernetes-deploys}

This extension includes one or more items.

| Includes | Number |
|----------|--------|
| [Alerts](/docs/cloud-logs?topic=cloud-logs-alerts) | 5 |
| [Dashboards](/docs/cloud-logs?topic=cloud-logs-about_dashboards) | 1 |
| [Enrichments](/docs/cloud-logs?topic=cloud-logs-enriching-data) | 0 |
| [Events to metrics](/docs/cloud-logs?topic=cloud-logs-configure-event2metrics) | 0 |
| [Rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) | 0 |
| [Views](/docs/cloud-logs?topic=cloud-logs-custom_views) | 0  |
{: caption="Items included when extension is deployed" caption-side="bottom"}

Before deploying this extension, make sure that deploying the extension will not cause you to exceed [limits for your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-limits). If deploying the extension results in limits being exceeded, the deployment will fail.
{: tip}

## Deploying the extension
{: #extensions-kubernetes-deploy}

You can deploy this extension in any {{site.data.keyword.logs_full_notm}} instance that collects {{site.data.keyword.containerlong_notm}} logs. This extension includes a set of pre-configured resources such as dashboards, views, and alerts that help you monitor critical metrics, identify anomalies, and optimize your system's performance.

For more information about deploying the extension, see [Deploying, managing, and removing {{site.data.keyword.logs_full_notm}} extensions](/docs/cloud-logs?topic=cloud-logs-extensions-mgmt).


{{/_include-segments/extensions-validate.md}}

## Dashboard
{: #extensions-kubernetes-dashboards}

One dashboard is provided providing data about {{site.data.keyword.containerlong_notm}} logs including:

* Count of clusters
* Count of nodes
* Count of pods
* Count of containers
* List of the node hosts
* The node hosts with the most logs
* The trend of node event logs

## Alerts
{: #extensions-kubernetes-alerts}

You can deploy any of the following alert:

* `No logs from service`: No logs have been received from the kubernetes service, indicating potential issues with logging configuration, service downtime, or connectivity problems affecting log transmission.
* `More than 5 erroneous cluster logs within 15 minutes`: Over 5 error logs have been recorded at the cluster level within a 15-minute window indicating potential issues affecting the Kubernetes cluster's overall health or configuration.
* `More than 5 erroneous pod logs within 15 minutes`: More than 5 error logs have been detected in pod-level operations within 15 minutes, suggesting issues with workloads or pod-level configurations.
* `Host change`: A host change event has been detected which might indicate a node replacement, scaling operation, or unexpected infrastructure changes.
* `Permission denied`: A permission denial has occurred during a Kubernetes operation possibly caused by misconfigured access controls or insufficient permissions for the requested action.
