---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-15"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why is the **All Logs** option not available?
{: #ts-no-all-logs}
{: troubleshoot}
{: support}

In {{site.data.keyword.logs_full}}, when viewing logs, you cannot select the **All Logs** option.
{: shortdesc}


The **All Logs** option is disabled and you cannot select it. You can select only {{site.data.keyword.frequent-search}}.
{: tsSymptoms}


Some issues that can cause data that is received by {{site.data.keyword.logs_full_notm}} to be only available in {{site.data.keyword.frequent-search}} include:
{: tsCauses}

- No data bucket is configured for the {{site.data.keyword.logs_full_notm}} instance. Data is only maintained for the retention period for the {{site.data.keyword.logs_full_notm}} instance [service plan](docs/cloud-logs?topic=cloud-logs-service_plans). After the retention period, the data is dropped.

   A data bucket is required for data to be configured to be sent by TCO policies to the {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}} pipelines. A data bucket is also required for data that is received by {{site.data.keyword.logs_full_notm}} to be automatically archived and accessible using **All Logs**.
- Service to service authorization is not configured correctly between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}}.


Resolve the issue based on the cause:
{: tsResolve}

- [Configure a data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket) for your {{site.data.keyword.logs_full_notm}} instance, if one is not configured.
- Check that your [service to service authorization](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos&interface=ui) to the {{site.data.keyword.cos_full_notm}} bucket is correctly configured. Update the authorization if it is incorrect.
