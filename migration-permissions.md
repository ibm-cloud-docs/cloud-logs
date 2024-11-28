---

copyright:
  years:  2024
lastupdated: "2024-11-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Required IAM permissions to run the {{site.data.keyword.logs_full}} migration tool
{: #migration-permissions}

The {{site.data.keyword.logs_full}} migration tool requires that you have certain {{site.data.keyword.iamlong}} permissions to successfully migrate your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance configuration to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

| Service | Roles |
|-----------|------|
| {{site.data.keyword.at_full_notm}} | `viewer`, `reader` |
| {{site.data.keyword.atracker_full_notm}} | `administrator`, `writer` |
| {{site.data.keyword.la_full_notm}} | `viewer`, `reader` |
| {{site.data.keyword.logs_full_notm}} | `manager`, `administrator`, `sender` |
| {{site.data.keyword.cos_full_notm}} | `writer` `[*]`, `editor`, `service configuration reader`, `manager` `[**]` |
| {{site.data.keyword.keymanagementservicelong_notm}} | `viewer`, `reader` |
| {{site.data.keyword.logs_routing_full_notm}} | `manager` |
| Event Notifications | `manager`, `Event Source Manager` and `Reader` |
{: caption="Required permissions to run the migration tool" caption-side="bottom"}

`[*]` {{site.data.keyword.cos_full_notm}} buckets with {{site.data.keyword.keymanagementservicelong_notm}} configured keys must have the `writer` role (`cloud-object-storage.bucket.list_crk_id`) to read the key name.

`[**]` {{site.data.keyword.cos_full_notm}} buckets with Activity tracker or Monitoring enabled must have the `manager` role (`storage.bucket.put_activity_tracking`,
`cloud-object-storage.bucket.put_metrics_monitoring`) to create the new buckets with the correct configuration.

You must have permissions in the resource groups where you plan to create resources with the Migration tool.
{: note}


When you configure your Logging agent to send logs to {{site.data.keyword.logs_full_notm}}, you will need credentials that include the `sender` role. For more information, see [Setting up IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).
{: tip}

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned.
{: important}
