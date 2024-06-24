---

copyright:
  years:  2024
lastupdated: "2024-05-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Learning about {{site.data.keyword.logs_full_notm}} architecture and workload isolation
{: #compute-isolation}

Review the following sample architecture for {{site.data.keyword.logs_full_notm}}, and learn more about different isolation levels so that you can choose the solution that best meets the requirements of the workloads that you want to run in the cloud.
{: shortdesc}

## {{site.data.keyword.logs_full_notm}} architecture
{: #architecture}

{{site.data.keyword.logs_full_notm}} is a multi-tenant, regional service that is available in {{site.data.keyword.cloud_notm}}. With {{site.data.keyword.logs_full_notm}}, you can analyze, process, store, and query your logs. See [List of supported locations](/docs/cloud-logs?topic=cloud-logs-regions).

![A diagram that shows a sample {{site.data.keyword.logs_full_notm}} architecture.](images/architecture-workload-isolation.drawio.svg "{{site.data.keyword.logs_full_notm}} architecture sample."){: caption="Figure 1. {{site.data.keyword.logs_full_notm}} sample architecture" caption-side="bottom"}

The following sections provide details about specific sections of the architecture.

### Front end
{: #architecture-frontend}

Front end components communicate outside of {{site.data.keyword.logs_full_notm}}.

* `Ingestion`: Audit events, platform logs, and application logs sent to the ingress endpoint of {{site.data.keyword.logs_full_notm}} are forwarded to back end components where they will be processed and stored. For more information, see [Ingress endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_ingress).
* `Web UI`: Launch the {{site.data.keyword.logs_full_notm}} dashboard in your browser to view, monitor, and manage logs. The web UI component uses back end components to implement the dashboard. For more information, see [Navigating to the UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).
* `API`: The {{site.data.keyword.cloud_notm}} Terraform provider as well as the {{site.data.keyword.logs_full_notm}} CLI plug-in uses the {{site.data.keyword.logs_full_notm}} API to configure the service instance as well as query logs. The API component uses back end components to perform the requested actions. For more information, see [API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).

### Back end
{: #architecture-backend}

Back end components operate within {{site.data.keyword.logs_full_notm}}.

* `Management`: Management components are responsible for configuring the {{site.data.keyword.logs_full_notm}} service instance. This includes features such as TCO policies, parsing rules, alerts, dashboards, and so on.
* `Priority insights`, `Analyze and alert`, `Store and search`: The central data processing pipeline of the {{site.data.keyword.logs_full_notm}} service implements features such as log parsing, storing and searching logs in {{site.data.keyword.cos_short}} buckets, transforming logs to metrics, alerting on logs, storing and searching priority logs, and so on.

### Storage
{: #architecture-storage}

Storage components store data used by {{site.data.keyword.logs_full_notm}}.

* `Configuration`: Stores {{site.data.keyword.logs_full_notm}} service instance configuration settings.
* `Priority logs`: Stores logs sent to an {{site.data.keyword.logs_full_notm}} service instance. Logs are indexed for fast query and removed after the chosen retention period has been exceeded.
* `Service data`: Stores data to implement the {{site.data.keyword.logs_full_notm}} service. This data includes metadata such as log templates or caches to improve performance.

## Integration with other {{site.data.keyword.cloud_notm}} services
{: #architecture-integration}

{{site.data.keyword.logs_full_notm}} integrates with other {{site.data.keyword.cloud_notm}} services that process, store, or control your data. {{site.data.keyword.logs_full_notm}} accesses these services through the {{site.data.keyword.cloud_notm}} public or private network.

| Service name | Description |
|------------|-------------------------------------|
| {{site.data.keyword.atracker_full_notm}} | You can use {{site.data.keyword.logs_full_notm}} as a target for audit events. For more information, see [Managing targets in {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-target_v2). |
| {{site.data.keyword.logs_routing_full_notm}} | You can use {{site.data.keyword.logs_full_notm}} as a target for platform and application logs. For more information, see [Creating an {{site.data.keyword.logs_full_notm}} tenant in {{site.data.keyword.logs_routing_full_notm}}](/docs/logs-router?topic=logs-router-onboard-cloud-logs-tenant).  \n. \n You can use the {{site.data.keyword.logs_routing_full_notm}} agent to collect and forward application logs to {{site.data.keyword.logs_full_notm}}.  |
| {{site.data.keyword.cos_full_notm}} | {{site.data.keyword.logs_full_notm}} uses {{site.data.keyword.cos_short}} buckets, owned by you, for long term storage and search of logs and log metrics. You need to attach the {{site.data.keyword.cos_short}} buckets to your {{site.data.keyword.logs_full_notm}} service instance. For more information, see [Configuring buckets for long term storage and search](/docs/cloud-logs?topic=cloud-logs-about-bucket). |
| {{site.data.keyword.messagehub_full}} | You can send logs from {{site.data.keyword.logs_full_notm}} to an {{site.data.keyword.messagehub_full}} topic.  |
| {{site.data.keyword.en_full_notm}} | You can use {{site.data.keyword.en_full_notm}} to notify your operators or other systems about {{site.data.keyword.logs_full_notm}} alerts. For more information, see [Enabling event notifications for {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-event-notifications-events). |
| {{site.data.keyword.iamlong}} | To authenticate requests to the service and authorize user actions, {{site.data.keyword.logs_full_notm}} implements platform and service access roles in {{site.data.keyword.iamshort}} (IAM). For more information about required IAM permissions to work with the service, see [Managing access for {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-iam).  \n. \n {{site.data.keyword.logs_full_notm}} accesses IAM through {{site.data.keyword.cloud_notm}} public network. |
{: caption="Table 1. {{site.data.keyword.logs_full_notm}}  integration with other {{site.data.keyword.cloud_notm}} services." caption-side="top"}
{: summary="The first column is the service. The second column is a description of the service."}

## Workload isolation
{: #workload-isolation}

Each regional deployment serves multiple tenants that are identified by the {{site.data.keyword.logs_full_notm}} service instance GUID.

* There is a single deployment per region that is implementing the {{site.data.keyword.logs_full_notm}} control and data plane shared by all service instances.
* All data - including logs, configuration, and service data - is processed and stored per region and not visible in other regions.
* All service instances share the same network, compute, and memory and storage resources in the control and data planes of the service.
* All data in transit, as well as data at rest, in control and data planes is encrypted using keys provided and managed by IBM.
* All communication within control and data planes is performed on the {{site.data.keyword.cloud_notm}} private network.
* You can use following approaches to access the ingestion and the API endpoints:
    * Public endpoint: Access through the {{site.data.keyword.cloud_notm}} public network.
    * [Cloud Service Endpoint (CSE)](/docs/account?topic=account-service-endpoints-overview): Access through the {{site.data.keyword.cloud_notm}} private network and endpoints shared with all service instances in the region.
    * [Virtual Private Endpoint (VPE)](/docs/vpc?topic=vpc-about-vpe): Access through the {{site.data.keyword.cloud_notm}} private network and endpoints dedicated to the service instance.
* You can access the web UI endpoint through the {{site.data.keyword.cloud_notm}} public network.
* All data processed in the {{site.data.keyword.logs_full_notm}} service is associated with the service instance. Stored data is segmented by service instance.
* {{site.data.keyword.logs_full_notm}} enforces all applicable IAM access and authorization policies on all requested operations related to a service instance. Audit events are created.
* {{site.data.keyword.logs_full_notm}} integrates with other {{site.data.keyword.cloud_notm}} services. When processing data with these services, the workload isolation characteristics of these services apply.
