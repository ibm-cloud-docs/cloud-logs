---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-15"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# TCO policies are configured to route data to the {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}} pipelines, but I can't find my logs. What might be the problem?
{: #ts-no-tco-data}
{: troubleshoot}
{: support}

TCO policies configured to send data to the {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}} pipelines are not sending data to those pipelines.
{: shortdesc}

You configured your TCO policies and policy overrides to process data sent to {{site.data.keyword.logs_full_notm}} into the {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}} pipelines. However, no data is flowing to those pipelines and the data is also not appearing in the {{site.data.keyword.frequent-search}} pipeline.
{: tsSymptoms}


Some issues that can cause data that is received by {{site.data.keyword.logs_full_notm}} to be dropped include:
{: tsCauses}

- No data bucket is configured for the {{site.data.keyword.logs_full_notm}} instance. If the TCO optimizer is configured to send data to the {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}} pipelines, and no data bucket is configured, data that is sent to those pipelines is dropped.
- You configured blocking rules to drop data that is received by {{site.data.keyword.logs_full_notm}}.
- Service to service authorization is not configured correctly between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}}.


Resolve the issue based on the cause:
{: tsResolve}

- [Configure a data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket) for your {{site.data.keyword.logs_full_notm}} instance if one is not configured.
- Review your configured [blocking rules](/docs/cloud-logs?topic=cloud-logs-parse-block-rule&interface=ui) and correct them if configured incorrectly.
- Check that your [service to service authorization](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos&interface=ui) to the {{site.data.keyword.cos_full_notm}} bucket is correctly configured. Update the authorization if it is incorrect.
