---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-25"

keywords:

subcollection: cloud-logs



---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when using {{site.data.keyword.logs_full_notm}}
{: #shared-responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.logs_full_notm}}. For a high-level view of the service types in {{site.data.keyword.cloud_notm}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.logs_full_notm}}. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).


## Configuration
{: #sr-configuration}

| Task              | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|-------------------|-------------------------------------------------|-----------------------|
| [Configuration of an {{site.data.keyword.logs_full_notm}} data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket) | None | [TCO policies](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) sending data to the {{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}} pipelines require a data bucket to be configured. If a data bucket is not configured for these policy types, there is a potential for data to be dropped.  \n  \n Without a data bucket, data will not be retained beyond the selected [service plan](/docs/cloud-logs?topic=cloud-logs-service_plans).|
| Configuration of the {{site.data.keyword.agent}} | Provides the ability to configure the {{site.data.keyword.agent}}. | [Configure the {{site.data.keyword.agent}} for your environment to meet your needs.](/docs/cloud-logs?group=sending-data-to-a-cloud-logs-instance)  \n  \n Prior to configuring the {{site.data.keyword.agent}}, review  [Considerations when you configure the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-configuration-considerations) to understand how the {{site.data.keyword.agent}} configuration affects processing of log data. |
{: caption="Responsibilities for service configuration" caption-side="top"}



## Incident and operations management
{: #incident-and-ops}

| Task              | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|-------------------|-------------------------------------------------|-----------------------|
| Incident and operations management | Maintain service instances and infrastructure workloads. | Maintain incident and operations management of your data. |
| Monitor incidents  | Provide notifications for planned maintenance, security bulletins, or unplanned outages. | * Set preferences to [receive emails about platform notifications](/docs/account?topic=account-email-prefs#setting-platform-notifications).  \n * Monitor the [IBM Cloud status page](https://{DomainName}/status?selected=announcement) for general announcements. |
| Maintain {{site.data.keyword.cloud_notm}} high availability SLA for {{site.data.keyword.logs_full_notm}}   | * Provide {{site.data.keyword.logs_full_notm}} functionality across availability zones in a Multi-Zone Region (MZR).  \n * Provide replication, fail-over features, and infrastructure maintenance and updates. | * Back up your {{site.data.keyword.logs_full_notm}} configuration. For example, keep the configuration in a version control system so that you can reconfigure a region if needed.   \n * Comply with [Operational responsibilities when using {{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-responsibilities).  \n * Comply with [Operational responsibilities when using {{site.data.keyword.en_full_notm}}](/docs/event-notifications?topic=event-notifications-en-responsibilities). |
{: caption="Responsibilities for incident and operations" caption-side="top"}


## Change management
{: #change-management}

| Task                                                    | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|---------------------------------------------------------|-----------------------|--------|
| Updates to {{site.data.keyword.logs_full_notm}} | * Provide major, minor, and patch version updates for {{site.data.keyword.logs_full_notm}} interfaces.  \n * Document changes in the [IBM Cloud Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external} | Apply changes to keep up to the latest versions and functionality. |
{: caption="Responsibilities for change management" caption-side="top"}



## Identity and access management
{: #iam-responsibilities}


| Task                           | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|--------------------------------|-------------------------------------------------|-----------------------|
| Manage permissions for {{site.data.keyword.logs_full_notm}}. | Provide the ability to restrict access to resources.  \n  \n {{site.data.keyword.IBM_notm}} is responsible for the security and compliance of the {{site.data.keyword.logs_full_notm}} service. | * Restrict access to {{site.data.keyword.logs_full_notm}}, {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.en_full_notm}} resources by defining Cloud IAM access policies and authorizations.  \n * Define IAM policies to control data access.  \n * [Learn more about controlling access through IAM](/docs/cloud-logs?topic=cloud-logs-iam).|
| Create service to service authorizations to grant authorizations between services. |  Provide the ability to restrict access to resources.  \n  \n {{site.data.keyword.IBM_notm}} is responsible for the security and compliance of the {{site.data.keyword.logs_full_notm}} service. | You must configure service to service authorizations so dependant services can communicate with one another. For more information see [Managing authorizations to grant access between services](/docs/cloud-logs?topic=cloud-logs-iam-service-auth). |
| Use Service ID API keys or Trusted Profiles in production environments | None | While {{site.data.keyword.logs_full_notm}} allows the use of individual user API keys, production environments should be configured using [Service ID API keys](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key) or [Trusted Profiles](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-trusted-profile).  \n  \n If individual user API keys are used, the authorization granted by those keys will be removed if the user creating those API keys is no longer an authorized IBM Cloud user.  \n  \n Individual user API keys should only be used in non-production environments. |
{: caption="Responsibilities for identity and access management" caption-side="top"}



## Security and regulation compliance
{: #security-compliance}


| Task                                       | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|--------------------------------------------|-------------------------------------------------|-----------------------|
| Meet security and compliance objectives  | Maintain controls that are commensurate to various industry compliance standards.  | * Set up and maintain security and regulation compliance for your apps and data.  \n * When using {{site.data.keyword.cos_full_notm}}, ensure you comply with [Data security](/docs/cloud-object-storage?topic=cloud-object-storage-security) and [Compliance](/docs/cloud-object-storage?topic=cloud-object-storage-compliance).  \n * When using {{site.data.keyword.en_full_notm}}, ensure you comply with [Data security and compliance](/docs/event-notifications?topic=event-notifications-en-data-security-and-compliance).  |
{: caption="Responsibilities for security and regulation compliance" caption-side="top"}


## Disaster recovery
{: #disaster-recovery}

Disaster recovery includes tasks such as:

* Providing dependencies on disaster recovery sites.
* Provisioning disaster recovery environments.
* Backing up data and configuration information.
* Replicating data and configuration information to the disaster recovery environment.
* Failover on disaster events.

| Task                                                            | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|-----------------------------------------------------------------|-------------------------------------------------|-----------------------|
| Restore functionality for {{site.data.keyword.logs_full_notm}}  | Recover and restart {{site.data.keyword.logs_full_notm}} components after any disaster event. `[*]` |  [Complete the disaster recovery (DR) steps for {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-cloud-logs-ha-dr). |
| Backup {{site.data.keyword.logs_full_notm}} components   | Ensure that backup of {{site.data.keyword.logs_full_notm}} metadata is in place and properly working according to defined policies. | * Follow the {{site.data.keyword.cos_full_notm}} disaster revovery strategy guidance. For more information, see [Data security](/docs/cloud-object-storage?topic=cloud-object-storage-security), [Create a Secure Content Store](/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store), and [Using replication for business continuity and disaster recovery](/docs/cloud-object-storage?topic=cloud-object-storage-replication-overview#replication-bcdr).  \n * Ensure that log files in the {{site.data.keyword.cos_full_notm}} bucket are retained according to the desired policy.  \n * Follow the {{site.data.keyword.en_full_notm}} service disaster revovery strategy guidance. For more information, see [Securing your data in {{site.data.keyword.en_full_notm}}](/docs/event-notifications?topic=event-notifications-en-mng-data) and [Disaster recovery](/docs/event-notifications?topic=event-notifications-en-responsibilities#en-disaster-recovery).|
{: caption="Responsibilities for disaster recovery" caption-side="top"}


`[*]` Recovered and restarted service components will not have customer's configurations or data reloaded.
{: note}
