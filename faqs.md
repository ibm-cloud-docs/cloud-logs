---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-12"

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

## I use the minus sign in {{site.data.keyword.at_full_notm}} and {{site.data.keyword.la_full_notm}} searches. Why is the minus sign not working in {{site.data.keyword.logs_full_notm}}?
{: #faq_not}
{: faq}

When searching in {{site.data.keyword.at_full_notm}} and {{site.data.keyword.la_full_notm}} you could use the minus sign (`-`) to indicate data to be excluded. Using the minus sign is not supported by {{site.data.keyword.logs_full_notm}}.

When searching in {{site.data.keyword.logs_full_notm}}, the `NOT` operator is required instead.



## How long is data retained by {{site.data.keyword.logs_full_notm}} if {{site.data.keyword.cos_full_notm}} data and metrics buckets have not been configured?
{: #faq_nobucket}
{: faq}

If neither one or separate {{site.data.keyword.cos_full_notm}} data and metrics buckets have been configured, {{site.data.keyword.logs_full_notm}} retains data for the [retention plan](/docs/cloud-logs?topic=cloud-logs-service_plans) selected for the instance.



## Do I need to archive logs separately if a single {{site.data.keyword.cos_full_notm}} bucket is used for both data and metrics?
{: #faq_onebucket}
{: faq}

It is recommended that separate {{site.data.keyword.cos_full_notm}} buckets be used for the {{site.data.keyword.logs_full_notm}} data bucket and the metrics bucket and that you do not combine these two buckets into a single {{site.data.keyword.cos_full_notm}} bucket, even though it is technically feasible to do so.
