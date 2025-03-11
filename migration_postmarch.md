---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-11"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Considerations after 30 March 2025 for {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} customers
{: #migration_postmarch}

Beginning 31 March 2025 any {{site.data.keyword.la_full}} and {{site.data.keyword.at_full_notm}} instances that are still provisioned in the IBM Cloud will be removed by IBM. If you have {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instances that are removed by IBM, you need to know how that removal affects your environment and any additional steps that you might need to take.
{: shortdesc}

## Actions taken by IBM
{: #migration_postmarch_ibm}

Beginning 31 March 2025 IBM will remove any provisioned {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instances in your account. As part of this removal, IBM removes all service configuration information and data within those instances.

When the instances are removed, the instances are not listed in the IBM Cloud resource list or in the Observability UI.

The instances might still display in the resource list and Observability UI during the removal process, but opening the {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} dashboard displays an error. The error is expected during the removal process. After the removal process completes, the instances will no longer be listed in the resource list or Observability UI.
{: note}

Data that is archived in {{site.data.keyword.cos_full_notm}} buckets is not affected. You can continue to manage the data in those buckets according to your compliance and operations requirements.

## Customer actions required
{: #migration_postmarch_customer}

After your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instances are removed, either by yourself or IBM, there are still some steps that you need to do too fully clean up your environment. These steps includes:

* Removing {{site.data.keyword.iamshort}} (IAM) permissions and policies.

* Removing {{site.data.keyword.logs_routing_full_notm}} configurations to {{site.data.keyword.la_full_notm}} instance targets.

* Removing {{site.data.keyword.atracker_full_notm}} routing and target configurations to {{site.data.keyword.at_full_notm}} instances that were removed. 

* Removing or updating any agents, apps, or configurations (for example by Rsyslog) sending data to {{site.data.keyword.la_full_notm}} instances.

* Removing any alert configurations or integrations (for example, PagerDuty) between the removed instances and the destination service.

If you are sending data to {{site.data.keyword.la_full_notm}} by using agents, the REST API, or other configurations, logging reporting connection errors are returned since the {{site.data.keyword.la_full_notm}} ingestion endpoints are also removed.
{: attention}

For more information about these removal steps, see:

* [Removing deprecated {{site.data.keyword.at_full_notm}} instances](/docs/cloud-logs?topic=cloud-logs-migration-remove-at)
* [Removing deprecated {{site.data.keyword.la_full_notm}} instances](/docs/cloud-logs?topic=cloud-logs-migration-remove-la)
* [Removing deprecated {{site.data.keyword.la_full_notm}} instances with platform logs enabled](/docs/cloud-logs?topic=cloud-logs-migration-remove-plat)




