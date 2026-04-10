---

copyright:
  years:  2024, 2026
lastupdated: "2026-03-19"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Managing {{site.data.keyword.cos_full_notm}} (COS) buckets
{: #cos}


You must manage the {{site.data.keyword.cos_full_notm}} buckets that you attach to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

## Before you begin
{: #cos_pre_req}

To manage buckets, your user must be granted permissions to work with buckets on the {{site.data.keyword.cos_full_notm}} instance. For more information about roles, see [Identity and Access Management roles](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-with-iam&interface=ui).

For {{site.data.keyword.logs_full_notm}} to access configured {{site.data.keyword.cos_short}} buckets, S2S authorization is required. For more information, see [Creating a S2S authorization to grant access to a bucket](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos&interface=ui).
{: important}

You can choose from any of the following options to create a bucket:

| Action             | More info |
|--------------------|-----------|
| Create a bucket through the {{site.data.keyword.cloud_notm}} UI | [Learn more](/docs/cloud-logs?topic=cloud-logs-cos#cos_create_bucket_ui) |
| Create a bucket through the {{site.data.keyword.cloud_notm}} CLI | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-ic-cos-cli#create-a-new-bucket) |
| Create a bucket by using cURL | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-curl#curl-add-bucket) |
| Create a bucket by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-new-bucket) |
| Create a bucket with a different storage class by using the REST API| [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-storage-class) |
| Create a bucket with Key Protect or Hyper Protect Crypto Services managed encryption keys (SSE-KP) by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-key-protect) |
| Create a bucket by using Terraform | [Learn more](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-template#storage-templates) |
{: caption="Create bucket requests" caption-side="top"}

To create a bucket, your user must have *manager* or *writer* permissions for the {{site.data.keyword.cos_full_notm}} instance where you plan to create the bucket.
{: note}

## Creating a bucket through the {{site.data.keyword.cloud_notm}} UI
{: #cos_create_bucket_ui}

Complete the following steps to create a bucket through the {{site.data.keyword.cloud_notm}} UI:

1. From the Navigation menu, select **Resource List**.

2. Select the {{site.data.keyword.cos_full_notm}} instance where you plan to create the bucket.

3. Select **Buckets**. Then, click **Create Bucket**.

    If you are configuring **archiving in an EU-managed location**, you must configure a bucket that complies with the EU-managed and GDPR regulations. For more information, see [European Union support](/docs/cloud-object-storage?topic=cloud-object-storage-eu).

4. Enter a bucket name for the *Unique bucket name* field.

    **Note:** All buckets in all regions across the globe share a single namespace.

5. Choose the type of resiliency and a location where you would like your data to be physically stored.

    Resiliency refers to the scope and scale of the geographic area across which your data is distributed.

    Cross Region resiliency will spread your data across several metropolitan areas.

    Regional resiliency will spread data across a single metropolitan area.

    A Single Data Center will only distribute data across devices within a single site.

    For more information, see [Select regions and endpoints](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints).

6. Choose the type of *Storage class*.

    You can create buckets with different storage classes. Choose the storage class for your bucket based on your requirements to retrieve data. For more information, see [Use storage classes](/docs/cloud-object-storage?topic=cloud-object-storage-classes).

    It is not possible to change the storage class of a bucket once the bucket is created. If objects need to be reclassified, it is necessary to move the data to another bucket with the wanted storage class.

7. Optionally, add additional encryption to your bucket. For example, configure Key Protect Key in your bucket to encrypt data at rest.

    You can only add additional encryption when you create the bucket.
    {: important}

    All objects are encrypted by default using randomly generated keys and an all-or-nothing-transform. While this default encryption model provides at-rest security, some workloads need to be in possession of the encryption keys used. For more information, see [Manage encryption](/docs/cloud-object-storage?topic=cloud-object-storage-encryption).



## Monitoring activity on {{site.data.keyword.cos_full_notm}} buckets
{: #cos_bucket_audit_events}

You can monitor activity on your {{site.data.keyword.cos_full_notm}} buckets by monitoring auditing events that are generated by the {{site.data.keyword.cos_full_notm}} (COS) service.

To collect auditing events for a bucket, consider the following information:

- Collection of auditing events in your account is optional. You must enable activity tracking events on your bucket at the time of bucket provisioning, or by updating the bucket configuration after bucket creation.

    Enable collection of auditing events after you have configured Activity Tracking in the region where the bucket is located.
    {: tip}

- By default, activity tracking events that report on global actions, such as bucket creation, are collected automatically. You can also collect

    - Management Events that report on requests that are related to managing bucket and object configuration.
    - Read Data Events that report on requests related to object list and read requests.
    - Write Data Events that report on requests related to writing and deleting objects from the bucket.

    To monitor data events, you must select the option **Track data events**. Then, select **read**, **write**, or **read & write** to collect events when an object is uploaded or downloaded from a bucket.

- You must configure each bucket to enable management events, or management and data events. Notice that you cannot enable data events only for a bucket.

For more information, see [Tracking events on your IBM Cloud Object Storage buckets](/docs/cloud-object-storage?topic=cloud-object-storage-at&interface=ui).

To send auditing events thar are generated to report activity on an {{site.data.keyword.cos_full_notm}} buckets, see [Configure Activity Tracking Events on your IBM Cloud Object Storage Bucket](/docs/cloud-object-storage?topic=cloud-object-storage-at&interface=ui#at-configure).


## Monitoring the health of a bucket
{: #cos_bucket_health}

You can use the {{site.data.keyword.mon_full}} service to monitor {{site.data.keyword.cos_short}} (COS) in the {{site.data.keyword.cloud_notm}}.

You can monitor the health and status of your {{site.data.keyword.cos_full_notm}} buckets by monitoring bucket usage metrics and HTTP request metrics. You must enable metrics tracking on your bucket at the time of bucket provisioning or by updating the bucket configuration after bucket creation.

For more information, see [Configure Metrics for IBM Cloud® Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-mm-cos-integration&interface=ui).



## Getting the bucket configuration details through the {{site.data.keyword.cloud_notm}} UI
{: #cos_bucket_details}
{: ui}

When you configure a target, you need the bucket name and the private endpoint.

Complete the following steps to get the bucket configuration details through the {{site.data.keyword.cloud_notm}} UI:

1. From the Navigation menu, select **Resource List**.

2. Select the {{site.data.keyword.cos_full_notm}} instance where you plan to create the bucket.

3. Select **Buckets**. Then, select the bucket that you want to use to collect auditing events.

4. Select **Configuration**. Look for the bucket name and the private endpoint.



## Listing objects in a bucket
{: #cos_bucket_list_objects}

You can choose any of the following methods to list objects in a bucket:
- [List objects in a given bucket by using the CLI](/docs/cloud-object-storage?topic=cloud-object-storage-ic-cos-cli#list-objects).
- [List objects in a given bucket by using the API](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-list-objects-v2)
- List objects in a given bucket through the {{site.data.keyword.cloud_notm}} UI.

### List objects in a given bucket through the {{site.data.keyword.cloud_notm}} UI
{: #cos_bucket_list_objects_ui}
{: ui}

Complete the following steps to list the objects in a bucket through the {{site.data.keyword.cloud_notm}} UI:

1. From the Navigation menu, select **Resource List**.

2. Select the {{site.data.keyword.cos_full_notm}} instance where the bucket is available.

3. Select **Buckets**.

4. Select a bucket. The list of objects is displayed.
