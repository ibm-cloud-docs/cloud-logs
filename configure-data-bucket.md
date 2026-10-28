---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-28"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the data bucket for an {{site.data.keyword.logs_full_notm}} instance
{: #configure-data-bucket}

Configure a bucket in {{site.data.keyword.cos_full_notm}} to store your {{site.data.keyword.logs_full_notm}} data for long term storage and search.
{: shortdesc}


## Prereqs
{: #configure-data-bucket-prereqs}

- The {{site.data.keyword.cos_full_notm}} service can be in the same account as your {{site.data.keyword.logs_full_notm}} instance, or can be located in a different account.

- You must have permissions to create a bucket in an {{site.data.keyword.cos_full_notm}} instance or have the details of an existing bucket.

- You must have permissions to configure a service to service authorization between the {{site.data.keyword.cos_full_notm}} service and the {{site.data.keyword.logs_full_notm}} service.


## Data bucket restrictions
{: #cos_databucket_restrictions}



### Storage classes
{: #cos_databucket_storageclasses}

{{site.data.keyword.cos_full_notm}} buckets used by {{site.data.keyword.logs_full_notm}} as data buckets can be configured only with the following [storage classes](/docs/cloud-object-storage?topic=cloud-object-storage-classes):

* Smart Tier
* Standard

The following storage classes are not supported by {{site.data.keyword.logs_full_notm}} as data buckets:

* Vault
* Cold Vault

### Archive rules
{: #cos_databucket_archiverules}

{{site.data.keyword.cos_full_notm}} allows you to define [archive rules](/docs/cloud-object-storage?topic=cloud-object-storage-archive) on buckets that archive objects automatically after the defined time period. Archived objects have a lower cost than regular objects, but need to be restored before they can be read again.

{{site.data.keyword.logs_full_notm}} cannot read archived objects. {{site.data.keyword.logs_full_notm}} searching of archived objects in the [All Logs](/docs/cloud-logs?topic=cloud-logs-query-about&interface=ui) view, or querying in [Archive queries](/docs/cloud-logs?topic=cloud-logs-query-archive-data-bucket), returns an error message.

{{site.data.keyword.cos_full_notm}} buckets used as {{site.data.keyword.logs_full_notm}} data buckets must not define archive rules that immediately archive objects, or archive objects within a few hours.

If you do not need to search logs older than a certain time period, for example, a month, you can define an {{site.data.keyword.cos_full_notm}} archive rule to archive objects older that the time period required for searching. Do not configure archiving for a period of less than 7 days.

By archiving data that you do not need to search, you can retain the log data at a reduced cost. If required, you can [restore archived objects](/docs/cloud-object-storage?topic=cloud-object-storage-archive#archive-restore-cli) if you need to search the data by using {{site.data.keyword.logs_full_notm}} in the future.

### Successful read activity tracking events
{: #cos_databucket_readevents}

{{site.data.keyword.atracker_full_notm}} drops successful `cloud-object-storage.object.read` events that are initiated by {{site.data.keyword.logs_full_notm}} instances because they are not needed. When reviewing activity tracking events related to {{site.data.keyword.logs_full_notm}} activity, you will not see see successful `cloud-object-storage.object.read` events.


## Configure an IAM Service to service authorization
{: #configure-data-bucket-s2s}
{: step}

You must define a service to service (S2S) authorization between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}} to allow {{site.data.keyword.logs_full_notm}} to read and write data into the data bucket.

For more information, see:
- [Creating a S2S authorization to grant access to a bucket when the {{site.data.keyword.logs_full_notm}} instance and the bucket are in the same account](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos).
- [Creating a cross-account S2S authorization to grant access to a bucket when the {{site.data.keyword.logs_full_notm}} instance and the bucket are in different accounts](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos-crossacc).


## Configure the data bucket
{: #configure-data-bucket-attach}
{: step}

Complete the following steps to configure a data bucket for an {{site.data.keyword.logs_full_notm}} instance:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.

3. Select **Logging** &gt; **Instances**. Then, select the instance to which you want to configure a data bucket.

4. In the *Storage* section, select **Connect** in the *Data bucket* section.

5. Choose how to enter the bucket details in the *Select bucket by* section:

    Choose **Instance** and select a COS instance and bucket if your {{site.data.keyword.logs_full_notm}} instance and the bucket are located in the same account.

    Choose **Bucket CRN** and enter the bucket CRN if your {{site.data.keyword.logs_full_notm}} instance and the bucket are located in different accounts.

6. Configure the **direct endpoint** as the bucket endpoint.

    Direct endpoints are used for requests originating from resources within VPCs. Direct endpoints provide better performance over Public endpoints and do not incur charges for any outgoing or incoming bandwidth even if the traffic is cross regions or across data centers. For more information, see [Endpoint Types](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints#advanced-endpoint-types).

7. Click **Save** to save the configuration.

Once a bucket is connected to a {{site.data.keyword.logs_full_notm}} instance, a bucket is always required. It can be changed but not removed.
{: important}
