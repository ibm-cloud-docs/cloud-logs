---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-10"

keywords:

subcollection: cloud-logs

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for {{site.data.keyword.logs_full_notm}}
{: #faq}

Frequently asked questions about {{site.data.keyword.logs_full}}.
{: shortdesc}

## Is there a recommended log message batch size and maximum size limit for log messages that are sent by using the API?
{: #faq_apisize}
{: faq}

The API is limited to a message size of 2 MB, which is approximately 3000 medium-sized logs.





## How long is data retained by {{site.data.keyword.logs_full_notm}} if {{site.data.keyword.cos_full_notm}} data and metrics buckets have not been configured?
{: #faq_nobucket}
{: faq}

If neither one or separate {{site.data.keyword.cos_full_notm}} data and metrics buckets have been configured, {{site.data.keyword.logs_full_notm}} retains data for the [retention plan](/docs/cloud-logs?topic=cloud-logs-service_plans) selected for the instance. If no data bucket is  configured, logs will only be viewable through {{site.data.keyword.frequent-search}} for the length of the retention plan.



## Do I need to archive logs separately if a single {{site.data.keyword.cos_full_notm}} bucket is used for both data and metrics?
{: #faq_onebucket}
{: faq}

It is recommended that separate {{site.data.keyword.cos_full_notm}} buckets be used for the {{site.data.keyword.logs_full_notm}} data bucket and the metrics bucket and that you do not combine these two buckets into a single {{site.data.keyword.cos_full_notm}} bucket, even though it is technically feasible to do so.





## Are charges related to {{site.data.keyword.cos_full}} use by {{site.data.keyword.logs_full_notm}} separate from {{site.data.keyword.logs_full_notm}} billed charges?
{: #faq_cos_cost}
{: faq}

Yes, usage of the {{site.data.keyword.cos_full}} service is a separate cost from {{site.data.keyword.logs_full_notm}}.

In the {{site.data.keyword.cos_full}} pricing model, {{site.data.keyword.logs_full_notm}} requests for data storage are ‘Class A’ requests, and {{site.data.keyword.logs_full_notm}} requests for data retrieval during queries are ‘Class B’ requests. For more information, see [request classes](/docs/cloud-object-storage?topic=cloud-object-storage-billing#billing-request-classes).

The {{site.data.keyword.logs_full_notm}} plan cost applies to the [data pipeline](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines) processing the data in {{site.data.keyword.logs_full_notm}}. You can adjust the data pipelines by using the [TCO Optimizer](/docs/cloud-logs?topic=cloud-logs-tco-optimizer).

For more information about {{site.data.keyword.logs_full_notm}} pricing, see [service plans and pricing](/docs/cloud-logs?topic=cloud-logs-service_plans). For more information about {{site.data.keyword.logs_full_notm}} cost management, see [controlling cost](/docs/cloud-logs?topic=cloud-logs-controlling-cost).
