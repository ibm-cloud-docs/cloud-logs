---

copyright:
  years:  2024
lastupdated: "2024-08-20"

keywords:

subcollection: cloud-logs

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQs for {{site.data.keyword.logs_full_notm}}
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


