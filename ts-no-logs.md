---

copyright:
  years:  2024
lastupdated: "2024-11-25"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why can't I see {{site.data.keyword.cloud_notm}} platform logs in the {{site.data.keyword.logs_full_notm}} UI?
{: #ts-no-logs}
{: troubleshoot}
{: support}

{{site.data.keyword.logs_routing_full}} is configured to send platform logs to {{site.data.keyword.logs_full_notm}}, but you cannot see the platform logs in the {{site.data.keyword.logs_full_notm}} UI.
{: shortdesc}

No platform logs are displayed in the {{site.data.keyword.logs_full_notm}} UI.
{: tsSymptoms}

Service to service authorization is not configured correctly.
{: tsCauses}

Make sure your [service to service authorization](/docs/logs-router?topic=logs-router-iam-service-auth-logs-routing&interface=ui) for {{site.data.keyword.logs_routing_full_notm}} is configured with the `sender` role. Check that the user who created the authorization has the `sender` role to send data to {{site.data.keyword.logs_full_notm}} from {{site.data.keyword.logs_routing_full_notm}}. If the user who created the authorization doesn't have the `sender` role or higher, add the `sender` role to the user and have the user create the service to service authorization again.
{: tsResolve}


