---

copyright:
  years:  2024
lastupdated: "2024-11-26"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# I am getting an error when applying {{site.data.keyword.en_full_notm}} resources using Terraform
{: #ts-mig-en}
{: troubleshoot}
{: support}

When accesing the directory containing the {{site.data.keyword.en_full}} configuration created by the {{site.data.keyword.logs_full_notm}} migration tool and using Terraform to apply the {{site.data.keyword.en_full_notm}} configuration to the {{site.data.keyword.logs_full_notm}} instance, an error is returned.
{: shortdesc}

You get an error message similar to the following:
{: tsSymptoms}

```text
Error: CreateTopicWithContext failed Your plan restricts additional topics to be added. Please upgrade the plan.
{
    "StatusCode": 403,
    "Headers": {
```
{: screen}


Your {{site.data.keyword.en_full_notm}} instance is configured using the `Lite` plan. Your {{site.data.keyword.en_full_notm}} instance must have the `Standard` plan to be configured for use with {{site.data.keyword.logs_full_notm}}.
{: tsCauses}

Upgrade your {{site.data.keyword.en_full_notm}} instance to the `Standard` plan and rerun the Terraform to apply the migrated configuration.
{: tsResolve}

