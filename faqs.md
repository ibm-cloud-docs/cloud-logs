---

copyright:
  years:  2024, 2025
lastupdated: "2025-04-16"

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
