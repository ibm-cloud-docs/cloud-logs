---

copyright:
  years:  2025, 2025
lastupdated: "2025-06-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Securing your data in {{site.data.keyword.logs_full_notm}}
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.logs_full_notm}}, it is important to know exactly what data is stored and encrypted and how you can delete it.
{: shortdesc}

## How your data is stored and encrypted in {{site.data.keyword.logs_full_notm}}
{: #data-storage}

{{site.data.keyword.logs_full_notm}} manages two types of data on behalf of customers: service configuration data and log data.

Information about managing configuration data is available in [Configuring your account preferences](/docs/cloud-logs?topic=cloud-logs-account_preferences). Configuration data is considered 'metadata'. Additional types of metadata includes alerts, parsing rules, TCO policies and similar configuration data. Configuration metadata is encrypted using service provider key management.

Log data can come from many sources: agents, {{site.data.keyword.cloud_notm}} services, APIs, and so on. Log data is processed by {{site.data.keyword.logs_full_notm}}. You can control data that is ingested, and is available for search in {{site.data.keyword.logs_full_notm}}. For more information, see [Controlling data ingested for search in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-control-data).



The type of encryption used with log data depends on how {{site.data.keyword.logs_full_notm}} is configured to process the data. Users configure [TCO policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) to manage how their log data is processed.

* Data processed in motion by {{site.data.keyword.logs_full_notm}} is done using service-managed encryption.

* Data stored at rest with {{site.data.keyword.frequent-search}} is managed with service-managed encryption.

* Data stored at rest in an {{site.data.keyword.cos_full}} (COS) bucket can be managed with customer-managed encryption.

Data stored in {{site.data.keyword.cos_full}} is a copy of data in {{site.data.keyword.frequent-search}} and the data retained in {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}}.

If the data must be protected by a customer-managed encryption, then [TCO policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) need to be configured to exclusively process data with {{site.data.keyword.monitoring}} or {{site.data.keyword.compliance}}.  For more information, see [Configuring the TCO Optimizer](/docs/cloud-logs?topic=cloud-logs-tco-optimizer).

## Protecting your sensitive data in {{site.data.keyword.logs_full_notm}}
{: #data-encryption}



Log data managed in an {{site.data.keyword.cos_full}} (COS) bucket supports the bring your own key method or keep your own key method, allowing you to meet the data control requirements if you need this level of assurance. For more information, see [Data security](/docs/cloud-object-storage?topic=cloud-object-storage-security).

Two key management options often selected are:

* [Key Protect](/docs/key-protect) – a full-service encryption solution that allows data to be secured and stored in {{site.data.keyword.cloud_notm}} using the latest encryption techniques that leverages FIPS 140-2 Level 3 certified cloud-based hardware security modules.

* [Hyper Protect Crypto Services](/docs/hs-crypto) – a dedicated key management services and hardware security module (HSM) based on {{site.data.keyword.cloud_notm}}.

Follow {{site.data.keyword.cos_full}} (COS) bucket configuration guidance from each of these services’ configuration.  No unique {{site.data.keyword.logs_full_notm}} configuration is required beyond connecting your {{site.data.keyword.logs_full_notm}} instance to a COS bucket.

## Deleting your data in {{site.data.keyword.logs_full_notm}}
{: #data-delete}

When you delete your {{site.data.keyword.logs_full_notm}} instance, all of the user data that is associated with the instance is also deleted. When the instance is deleted, a 7-day reclamation period begins. During that time, you are able to restore the instance and all of its associated user data. However, if the instance and data are permanently deleted, it can no longer be restored.

### Deleting the {{site.data.keyword.logs_full_notm}} instance
{: #service-delete}

If you no longer need an instance of {{site.data.keyword.logs_full_notm}}, you can delete the instance and any data that is stored. Once the instance is deleted, you will no longer have access to it. The instance will remain in the pending reclamation phase for 7 days. If you choose to reclaim the instance within this period, the reclamation process can be initiated and will complete successfully. See [Removing an instance](/docs/cloud-logs?topic=cloud-logs-instance-remove&interface=cli) for the steps to delete an instance.

### Restoring deleted data for {{site.data.keyword.logs_full_notm}}
{: #data-restore}

When an {{site.data.keyword.logs_full_notm}} instance is deleted, it is put in a suspend state for 7 days after which its removed from the {{site.data.keyword.cloud_notm}}. If the instance is reclaimed and re-enabled, you can regain access to it. Any previously stored data will be available and accessible again. If the instance is not reclaimed within the 7-day pending reclamation period, the data will be permanently deleted within 90 days. See [Recovering a deleted instance](/docs/cloud-logs?topic=cloud-logs-instance-reclaim&interface=ui) for the steps to recover an {{site.data.keyword.logs_full_notm}} instance.

Data retention in {{site.data.keyword.frequent-search}} depends on the [service plan](/docs/cloud-logs?topic=cloud-logs-service_plans) configured for the instance.
{: important}
