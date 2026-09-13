---

copyright:
  years:  2025, 2026
lastupdated: "2026-09-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Securing your data in {{site.data.keyword.logs_full_notm}}
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.logs_full_notm}}, it is important to know exactly what data is stored and encrypted and how you can delete it.
{: shortdesc}

## How is data stored and encrypted when using {{site.data.keyword.logs_full_notm}}
{: #data-storage}

{{site.data.keyword.logs_full_notm}} manages two types of data on behalf of customers: configuration data, also known as metadata, and log data.

### Configuration data
{: #data-storage-1}

Configuration data includes the following information:

- Instance level preferences information

    For more information, see [Configuring your account preferences](/docs/cloud-logs?topic=cloud-logs-account_preferences).

- User preferences information

- Configuration data of features such as view, alerts, parsing rules, dashboards, and TCO policies.

Configuration data is encrypted using service-managed encryption.

### Log data
{: #data-storage-2}

Log data can come from many sources: agents, {{site.data.keyword.cloud_notm}} services, APIs, and so on.

{{site.data.keyword.logs_full_notm}} is not designed for the storage or transmission of sensitive or confidential information. Personal data, credentials, or any sensitive content should not be included in data sent to {{site.data.keyword.logs_full_notm}}.
{: important}

Users can configure [TCO policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) to manage how their log data is processed in an {{site.data.keyword.logs_full_notm}} instance.

- Logs configured to the {{site.data.keyword.frequent-search}} data pipeline are retained by {{site.data.keyword.logs_full_notm}}  for a limited duration that is determined by the [instance plan level](/docs/cloud-logs?topic=cloud-logs-service_plans) and protected using a service-managed encryption key .

    If the instance has a {{site.data.keyword.cos_full}} (COS) bucket attached, all of the data which is sent to {{site.data.keyword.frequent-search}} is also stored in the COS bucket. The retention or deletion of the data in the bucket is controlled by the COS bucket configuration that you define.

- Logs configured to the {{site.data.keyword.monitoring}} or the {{site.data.keyword.compliance}} data pipeline store the data in the COS bucket that is attached to the instance. The retention or deletion of the data in the bucket is controlled by the COS bucket configuration that you define.

Users can control the data that is ingested and is available for search in {{site.data.keyword.logs_full_notm}} by using any of the following methods:

- Configuring the logging agent to include and exclude information that is sent to an {{site.data.keyword.logs_full_notm}} instance.

    For more information, see [Configuring what logs are included or excluded in an orchestrated environment](/docs/cloud-logs?topic=cloud-logs-configure-include-exclude) and [Configuring what logs are included or excluded in a Linux environment](/docs/cloud-logs?topic=cloud-logs-agent-linux#agent-linux-deploy-step5).

- [Controlling data ingested for search in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-control-data).

    Users can drop data during ingestion by using TCO policies or by using parsing rules.



## Protecting log data in {{site.data.keyword.logs_full_notm}}
{: #data-encryption}

The type of encryption that is used with log data depends on how {{site.data.keyword.logs_full_notm}} is configured to process the data.

- Data processed in motion by {{site.data.keyword.logs_full_notm}} is done using service-managed encryption.

- Data stored at rest with {{site.data.keyword.frequent-search}} is managed with service-managed encryption.

- Data stored at rest in an {{site.data.keyword.cos_full}} (COS) bucket can be managed with customer-managed encryption.

    Data stored in {{site.data.keyword.cos_full}} is a copy of the data in {{site.data.keyword.frequent-search}} and the data retained in {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}}.

    {{site.data.keyword.logs_full_notm}} supports server-side encryption (SSE) per bucket.{: important}

    For more information, see [Server-Side Encryption with IBM Key Protect (SSE-KP)](/docs/cloud-object-storage?topic=cloud-object-storage-kp).

Log data managed in an {{site.data.keyword.cos_full}} (COS) bucket supports the bring your own key method  allowing you to meet the data control requirements if you need this level of assurance. Follow {{site.data.keyword.cos_full}} (COS) bucket configuration guidance. For more information, see:
- [Data security](/docs/cloud-object-storage?topic=cloud-object-storage-security)
- [Encrypting your data in {{site.data.keyword.cos_full}} (COS)](/docs/cloud-object-storage?topic=cloud-object-storage-encryption)
- [Does {{site.data.keyword.cos_full}} (COS) provide encryption at rest and in motion?](/docs/cloud-object-storage?topic=cloud-object-storage-faq-encryption#faq-encrypt-basics)
- [FAQ - Encryption](/docs/cloud-object-storage?topic=cloud-object-storage-faq-encryption)

If your data must be protected by using a customer-managed encryption key, configure [TCO policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) to exclusively process data through the {{site.data.keyword.monitoring}} or {{site.data.keyword.compliance}} data pipelines. For more information, see [Configuring the TCO Optimizer](/docs/cloud-logs?topic=cloud-logs-tco-optimizer).
{: important}



## Deleting your data in {{site.data.keyword.logs_full_notm}}
{: #data-delete}

When you delete your {{site.data.keyword.logs_full_notm}} instance, all of the user data that is associated with the instance is also deleted. When the instance is deleted, a 7-day reclamation period begins. During that time, you are able to restore the instance and all of its associated user data. However, if the instance and data are permanently deleted, it can no longer be restored.

## Deleting the {{site.data.keyword.logs_full_notm}} instance
{: #service-delete}

If you no longer need an instance of {{site.data.keyword.logs_full_notm}}, you can delete the instance and any data that is stored. Once the instance is deleted, you will no longer have access to it. The instance will remain in the pending reclamation phase for 7 days. If you choose to reclaim the instance within this period, the reclamation process can be initiated and will complete successfully. See [Removing an instance](/docs/cloud-logs?topic=cloud-logs-instance-remove&interface=cli) for the steps to delete an instance.

## Restoring deleted data for {{site.data.keyword.logs_full_notm}}
{: #data-restore}

When an {{site.data.keyword.logs_full_notm}} instance is deleted, it is put in a suspend state for 7 days after which its removed from the {{site.data.keyword.cloud_notm}}. If the instance is reclaimed and re-enabled, you can regain access to it. Any previously stored data will be available and accessible again. If the instance is not reclaimed within the 7-day pending reclamation period, the data will be permanently deleted within 90 days. See [Recovering a deleted instance](/docs/cloud-logs?topic=cloud-logs-instance-reclaim&interface=ui) for the steps to recover an {{site.data.keyword.logs_full_notm}} instance.

Data retention in {{site.data.keyword.frequent-search}} depends on the [service plan](/docs/cloud-logs?topic=cloud-logs-service_plans) configured for the instance.
{: important}
