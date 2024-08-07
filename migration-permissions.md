---

copyright:
  years:  2024
lastupdated: "2024-07-23"

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
| {{site.data.keyword.logs_full_notm}} | `manager`, `editor` |
| {{site.data.keyword.cos_full_notm}} | `writer` `[*]`, `editor`, `service configuration reader` |
| {{site.data.keyword.keymanagementservicelong_notm}} | `viewer`, `reader` |
{: caption="Required permissions to run the migration tool" caption-side="bottom"}

`[*]` {{site.data.keyword.cos_full_notm}} buckets with {{site.data.keyword.keymanagementservicelong_notm}} configured keys must have the `writer` role (`cloud-object-storage.bucket.list_crk_id`) to read the key name.
