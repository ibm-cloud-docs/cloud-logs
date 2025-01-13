---

copyright:
  years: 2024, 2025
lastupdated: "2025-01-13"

keywords: HA for Cloud Logs, DR for Cloud Logs, Cloud Logs recovery time objective, Cloud Logs recovery point objective

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability and disaster recovery for {{site.data.keyword.logs_full_notm}}
{: #cloud-logs-ha-dr}

[High availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible in the presence of unexpected failures. [Disaster recovery](#x2113280){: term} is the process of recovering the service instance to a working state.
{: shortdesc}

## Responsibilities
{: #ha-responsibilities}

To find out more about responsibility ownership for using {{site.data.keyword.cloud}} products between {{site.data.keyword.IBM_notm}} and the customer, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} products](/docs/overview?topic=overview-shared-responsibilities).

To find out more about responsibility ownership for using {{site.data.keyword.logs_full_notm}}, see [Your responsibilities with using {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-shared-responsibilities&interface=ui).

## What level of availability do I need?
{: #ha-level}

You can achieve high availability on different levels in your IT infrastructure and within different components of your architecture. The level of availability that you need depends on several factors, such as your business requirements, the service level agreements (SLAs) that you have with your customers, and the resources that you want to expend.

## What level of availability does {{site.data.keyword.cloud_notm}} offer?
{: #ha-service}

Service level objectives (SLOs) describe the design points that the {{site.data.keyword.cloud_notm}} services are engineered to meet. {{site.data.keyword.logs_full_notm}} is designed to achieve the following availability target.

| Availability target | Target Value   |
|---|---|
|  Availability % | 99.99%  |
{: caption="SLO for {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}

The SLO is not a warranty and {{site.data.keyword.IBM_notm}} will not issue credits for failure to meet an objective. Refer to the SLAs for commitments and credits that are issued for failure to meet any committed SLAs. For a summary of all SLOs, see [{{site.data.keyword.cloud_notm}} service level objectives](/docs/overview?topic=overview-slo).
{: note}


## Locations
{: #ha-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).


## Disaster recovery strategy
{: #bc-dr-strategy}

{{site.data.keyword.cloud_notm}} has [business continuity](#x3026801){: term} plans in place to provide for the recovery of services within hours if a disaster occurs. You are responsible for your data backup and associated recovery of your content.

{{site.data.keyword.logs_full_notm}} provides ways to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [recovery point objective](#x3429911){: term} (RPO) and [recovery time objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets for {{site.data.keyword.logs_full_notm}}.

| Disaster recovery objective | Target Value   |
|---|---|
|  RPO |  Within 4 hours |
|  RTO |  Within 24 hours |
{: caption="RPO and RTO for {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}

{{site.data.keyword.logs_full_notm}} regularly backups the metadata in each region as follows:

- Daily full backups with a retention period of 30 days.
- Continuous incremental backups are taken to ensure point-in-time recovery (PITR) for the last 7 days.

{{site.data.keyword.logs_full_notm}} data is replicated across multiple regions. Regular backups are stored across multiple regions and can be restored to other regions.

{{site.data.keyword.logs_full_notm}} does not back up the data in your {{site.data.keyword.cos_full_notm}} buckets. For more information about the disaster recovery strategy for {{site.data.keyword.cos_full_notm}}, see [Cross-Region Endpoints](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints#endpoints-geo), [Data security](/docs/cloud-object-storage?topic=cloud-object-storage-security), [Create a Secure Content Store](/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store), and [Using replication for business continuity and disaster recovery](/docs/cloud-object-storage?topic=cloud-object-storage-replication-overview#replication-bcdr).

{{site.data.keyword.logs_full_notm}} does not back up the data in your {{site.data.keyword.en_full_notm}} instance. For more information about the disaster recovery strategy for {{site.data.keyword.en_full_notm}}, see [Securing your data in {{site.data.keyword.en_full_notm}}](/docs/event-notifications?topic=event-notifications-en-mng-data) and [Disaster recovery](/docs/event-notifications?topic=event-notifications-en-responsibilities#en-disaster-recovery).

## Disaster Recovery of an {{site.data.keyword.logs_full_notm}} instance
{: #bc-dr-disaster}

In a major regional disaster, such as an earthquake, flood, or tornado, an entire region might be impacted.

To recover an {{site.data.keyword.logs_full_notm}} instance, you must provision a new {{site.data.keyword.logs_full_notm}} instance and recreate resources. You must also have a DR strategy for the buckets that are associated with the instance, and the {{site.data.keyword.en_full_notm}} instance that you might have configured to trigger notification alerts.

To ensure that your workloads are resilient to such events, complete the following steps:

1. Define the regional strategy where you can restore the configuration that is down.

    Check your data locality and compliance requirements when choosing the recovery region.
    {: note}

    For more information on locations, see:

    * [{{site.data.keyword.logs_full_notm}} supported regions](/docs/cloud-logs?topic=cloud-logs-regions)
    * [{{site.data.keyword.cos_full_notm}} supported regions](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints)
    * [{{site.data.keyword.en_full_notm}} supported regions](/docs/event-notifications?topic=event-notifications-en-regions-endpoints). {{site.data.keyword.en_full_notm}} is not supported in all the regions where {{site.data.keyword.logs_full_notm}} is supported.

2. If you have configurations that do not use Terraform, backup your current configurations by using the API. If you use Terraform, save your Terraform scripts to help you recreate the region that is down. Consider using a version control system to store the backup files or terraform scripts.

    You can use Terraform to create {{site.data.keyword.logs_full_notm}} instances. See [Resource management Terraform resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/resource_instance){: external}.

    You can use Terraform to create the {{site.data.keyword.logs_full_notm}} resources. See [{{site.data.keyword.logs_full_notm}} Terraform resources](https://registry.Terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/logs_alert){: external}.

    You can use Terraform to create your data bucket, your metrics bucket, or both, with _Cross Region_ resiliency to store and access data across multiple geographical regions and ensure high availability, durability, and disaster recovery capabilities. See [{{site.data.keyword.cos_full_notm}} Terraform resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cos_replication).

    You can use Terraform to create your {{site.data.keyword.en_full_notm}} resources. See [{{site.data.keyword.en_full_notm}} Terraform resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/en_sources).

    You can use Terraform to create your IAM authorizations and permissions. See [IAM Terraform resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/policy_assignment).

    Always test that you can restore the backup configuration into an alternative region.{: important}


## Disaster recovery (DR) in a region
{: #bc-dr-recovery}

In the case of a regional disaster, you must complete the following steps to recover your instance in a new region:

1. Identify an alternate region where to restore the {{site.data.keyword.logs_full_notm}} instance.

2. Create the new {{site.data.keyword.logs_full_notm}} instance. For more information, see [Provisioning an instance](/docs/cloud-logs?topic=cloud-logs-instance-provision&interface=ui).

3. If your instance has buckets configured, complete the following steps:

    * If your {{site.data.keyword.logs_full_notm}} instance in the the disaster region was using a _Cross Region_ COS bucket, you can attach the same bucket to the new {{site.data.keyword.logs_full_notm}} instance, but you cannot query data created over the {{site.data.keyword.logs_full_notm}} instance in the disaster region using the new {{site.data.keyword.logs_full_notm}} instance's dashboards or CLI. You will only be able to query data that is ingested in the new region. You can download and view existing data from the region that is down. For more information about the archive data structure, see [Querying data directly from the archive](/docs/cloud-logs?topic=cloud-logs-query-archive-data-bucket).

    * If you need to access the logs from the {{site.data.keyword.logs_full_notm}} instance in the disaster area using the newly created {{site.data.keyword.logs_full_notm}} instance's dashboard or CLI, [contact IBM Support](/docs/account?topic=account-using-avatar&interface=ui). For more information about the disaster recovery strategy for {{site.data.keyword.cos_full_notm}}, see [Cross-Region Endpoints](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints#endpoints-geo), [Data security](/docs/cloud-object-storage?topic=cloud-object-storage-security), [Create a Secure Content Store](/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store), and [Using replication for business continuity and disaster recovery](/docs/cloud-object-storage?topic=cloud-object-storage-replication-overview#replication-bcdr).

    * If you were using local or regional buckets from the affected region, create new buckets. Attach the buckets to the new {{site.data.keyword.logs_full_notm}} instance. For more information, see [Configuring the data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket&interface=ui) and [Configuring the metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket&interface=ui).

    * Define IAM authorizations between the {{site.data.keyword.logs_full_notm}} instance and the buckets. For more information, see [Creating a S2S authorization to grant access to a bucket](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos&interface=ui).

    If your instance in the disaster affected region was not configured with buckets, the logs and metrics data will be lost.
    {: note}

4. If your instance has alerts configured, complete the following steps:

    * Create a new {{site.data.keyword.en_full_notm}} instance or use an existing one that you might have available in a different region, always making sure it meets your compliance and data locality requirements. For more information, see [Provisioning an instance](/docs/event-notifications?topic=event-notifications-en-create-en-instance). For more information about the disaster recovery strategy for {{site.data.keyword.en_full_notm}}, see [Securing your data in {{site.data.keyword.en_full_notm}}](/docs/event-notifications?topic=event-notifications-en-mng-data) and [Disaster recovery](/docs/event-notifications?topic=event-notifications-en-responsibilities#en-disaster-recovery).

    * Define IAM authorizations between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance. For more information, see [Creating a S2S authorization to work with the {{site.data.keyword.en_full_notm}} service](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-en&interface=ui).

    * Configure {{site.data.keyword.en_full_notm}} as an outbound integration. For more information, see [Configure routing of events to destinations in {{site.data.keyword.en_full_notm}}](/docs/cloud-logs?topic=cloud-logs-event-notifications-alerts).

5. Recreate the resources in the new {{site.data.keyword.logs_full_notm}} instance.

    Create views.

    Create dashboards.

    Create alerts.

    Create TCO policies.

    Create parsing rules.

    Create events to metrics.

    Enable data usage.

    Configure data rules.

    Configure data enrichment policies.


To make it easier to recover an {{site.data.keyword.logs_full_notm}} instance, use Terraform to manage your instances, configurations and IAM access. Using Terraform will eliminate the need for manual steps when configuring instances in another region.
{: tip}


After you recover the instance, you must reconfigure your data sources to send logs to the new instance:

1. If the new region has an {{site.data.keyword.logs_routing_full_notm}} tenant configured, you must use the current target associated for that region to view and monitor platform logs. If the new region does not have an {{site.data.keyword.logs_routing_full_notm}} tenant configured, create an {{site.data.keyword.logs_routing_full_notm}} tenant that references your new {{site.data.keyword.logs_full_notm}} instance. See [Creating an {{site.data.keyword.logs_routing_full_notm}} tenant](/docs/logs-router?topic=logs-router-tenant-create&interface=ui) and [Understanding business continuity and disaster recovery for {{site.data.keyword.logs_routing_full_notm}}](/docs/logs-router?topic=logs-router-bc-dr).

2. If the new region has an {{site.data.keyword.atracker_full_notm}} configuration that collects events from the region that is down, you can use the existing configuration to view and manage events. If the new region does not have an {{site.data.keyword.atracker_full_notm}} configuration that collects events from the region that is down, you must add a rule to indicate where and how you want to collect events. For more information, see [Creating a routing configuration resilient to a regional disaster](/docs/atracker?topic=atracker-dr_config).

3. Reconfigure your {{site.data.keyword.agent}} to point to the [ingestion endpoint](/docs/logs-router?topic=logs-router-endpoints) of the {{site.data.keyword.logs_full_notm}} recovery region.
