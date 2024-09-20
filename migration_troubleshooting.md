---

copyright:
  years:  2024
lastupdated: "2024-09-20"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Troubleshooting migration from {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} 
{: #migration_troubleshooting}

You might encounter some known issues when you migrate your {{site.data.keyword.la_full}} or {{site.data.keyword.at_full_notm}} instance configuration to {{site.data.keyword.logs_full_notm}}. This information helps troubleshoot and resolve these known issues.
{: shortdesc}

## Unable to find logs routed to {{site.data.keyword.la_full}}
{: #ts_mig_host}

While running your {{site.data.keyword.la_full_notm}} and {{site.data.keyword.logs_full_notm}} instances in parallel to validate your migration, you find that you can no longer find logs routed by {{site.data.keyword.logs_routing_full_notm}} to {{site.data.keyword.la_full_notm}} in the {{site.data.keyword.la_full_notm}} UI.

To find logs routed by {{site.data.keyword.logs_routing_full_notm}} to {{site.data.keyword.la_full_notm}}, you will need to [change your {{site.data.keyword.la_full_notm}} query](/docs/logs-router?topic=logs-router-ts-hostvalue).
