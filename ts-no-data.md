---

copyright:
  years:  2024
lastupdated: "2024-12-20"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why am I receiving a message that no data exists in my COS bucket?
{: #ts-no-data}
{: troubleshoot}
{: support}

When using the {{site.data.keyword.logs_full}} UI I'm seeing a message that no data exists in my COS bucket.
{: shortdesc}

When using the `All Logs` view in the {{site.data.keyword.logs_full_notm}} UI, the message `Archive issue No data exists in your COS bucket for the given timeframe` is displayed.
{: tsSymptoms}

Data might exist in the {{site.data.keyword.cos_full_notm}} (COS) bucket, but permissions to the bucket are configured incorrectly.
{: tsCauses}

Check the bucket and permissions. If authorization is not properly configured, data is not uploaded to the bucket and is dropped.
{: tsResolve}

1. Use the {{site.data.keyword.cos_full_notm}} UI to view the data bucket attached to your {{site.data.keyword.logs_full_notm}} instance to determine if data exists in the bucket.

2. Check that the correct permissions are set between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}}. For more information, see [IAM Service to service authorization](/docs/cloud-logs?topic=cloud-logs-about-bucket#about-bucket-s2s).

3. Ensure that the user setting the permissions has the [authorization](/docs/cloud-logs?topic=cloud-logs-iam&interface=ui) to send logs between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}}.

   If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned. 
   {: important}
