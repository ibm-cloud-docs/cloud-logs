---

copyright:
  years: 2024
lastupdated: "2024-11-08"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Understanding data portability for {{site.data.keyword.logs_full_notm}}
{: #data-portability}

Data portability involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer's own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, to their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.

For more information about your responsibilities for {{site.data.keyword.logs_full_notm}}, see [Understanding your responsibilities when using {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-shared-responsibilities).

## Dependent services
{: #data-portability-dependencies}

{{site.data.keyword.logs_full_notm}} interacts with the following {{site.data.keyword.cloud_notm}} services. See the documentation for these services for data portability related to these services.

* [{{site.data.keyword.iamlong}}](/docs/account) for access control and service to service authorization.

* [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage) for data and metrics storage.

* [{{site.data.keyword.en_full_notm}}](/docs/event-notifications) for notifications of triggered alerts.

* [{{site.data.keyword.messagehub_full_notm}}](/docs/EventStreams) for streaming {{site.data.keyword.logs_full_notm}} data to other tools.

## Data export procedures
{: #data-portability-procedures}

{{site.data.keyword.logs_full_notm}} has three types of data that can be exported:

* Log data
* Metrics data
* Configuration data

### Log and metrics data
{: #data-portability-logs}

{{site.data.keyword.logs_full_notm}} log and metrics data is stored in two [{{site.data.keyword.cos_full_notm}} buckets.](/docs/cloud-logs?topic=cloud-logs-about-bucket):

* Data bucket (log data)
* Metrics bucket (metrics data)

For information about exporting {{site.data.keyword.cos_full_notm}} bucket data, see the [{{site.data.keyword.cos_full_notm}} documentation](/docs/cloud-object-storage).

If {{site.data.keyword.logs_full_notm}} is not configured with {{site.data.keyword.cos_full_notm}} buckets, then log data is only flowing to the [{{site.data.keyword.frequent-search}} pipeline](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines). In this case, log data cannot be exported. If a metrics bucket is not configured, metrics data cannot be exported.
{: important}

### Configuration data
{: #data-portability-config}

In addition, {{site.data.keyword.logs_full_notm}} provides mechanisms to export settings and configurations that are used to process the customer's content.

| Configuration data | Export using |
|--------------------|--------------|
| Custom dashboards | [UI](/docs/cloud-logs?topic=cloud-logs-create_dashboards#db_export_import) |
| Alerts | [List API](/apidocs/logs-service-api#get-alerts)  \n [Get API](/apidocs/logs-service-api#get-alert) |
| Custom views `[*]` | [List API](/apidocs/logs-service-api#list-views)  \n [Get API](/apidocs/logs-service-api#get-view) |
| Folders (views) | [List API](/apidocs/logs-service-api#list-view-folders)  \n [Get API](/apidocs/logs-service-api#get-view-folder) |
| Webhooks | [List API](/apidocs/logs-service-api#list-outgoing-webhooks)  \n [Get API](/apidocs/logs-service-api#get-outgoing-webhook) |
| Enrichments | [List API](/apidocs/logs-service-api#get-enrichments) |
| TCO policies | [List API](/apidocs/logs-service-api#get-company-policies)  \n [Get API](/apidocs/logs-service-api#get-policy) |
| Parsing rules | [List API](/apidocs/logs-service-api#list-rule-groups)  \n [Get API](/apidocs/logs-service-api#get-rule-group) |
| Events to metrics | [List API](/apidocs/logs-service-api#list-e2m)  \n [Get API](/apidocs/logs-service-api#get-e2m) |
| Data access rules | [List API](/apidocs/logs-service-api#list-data-access-rules) |
| Data usage metrics | [List API](/apidocs/logs-service-api#get-data-usage-metrics-export-status) |
{: caption="Configuration export methods" caption-side="bottom"}

`[*]` - Only public views can be exported.

## Exported data formats
{: #data-portability-data-formats}

The exported data format depends on the type of exported data.

### Log data format
{: #data-portability-logs-format}

{{site.data.keyword.logs_full_notm}} log data is stored in {{site.data.keyword.cos_full_notm}} buckets in parquet format.


### Metrics data format
{: #data-portability-metrics-format}

{{site.data.keyword.logs_full_notm}} metrics data is stored in {{site.data.keyword.cos_full_notm}} buckets as Prometheus index blocks.

### Configuration data format
{: #data-portability-config-format}

{{site.data.keyword.logs_full_notm}} configuration data is exported in JSON format.

## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/terms/?id=Z126-6304_WS).
