---

copyright:
  years:  2024
lastupdated: "2024-09-25"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Managing {{site.data.keyword.cos_full_notm}} (COS) buckets
{: #cos}


Buckets are a way to organize your data in an {{site.data.keyword.cos_full_notm}} instance.
{: shortdesc}


To manage buckets, your user must be granted permissions to work with buckets on the {{site.data.keyword.cos_full_notm}} instance. For more information about roles, see [Identity and Access Management roles](/docs/cloud-object-storage?topic=cloud-object-storage-iam).



## Creating a bucket
{: #cos_create_bucket}

Choose 1 of the following options to create a bucket:

| Action             | More info |
|--------------------|-----------|
| Create a bucket through the {{site.data.keyword.cloud_notm}} UI | [Learn more](/docs/atracker?topic=atracker-cos#cos_create_bucket_ui) |
| Create a bucket through the {{site.data.keyword.cloud_notm}} CLI | [Learn more](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-create-bucket) |
| Create a bucket by using cURL | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-curl#curl-add-bucket) |
| Create a bucket by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-new-bucket) |
| Create a bucket with a different storage class by using the REST API| [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-storage-class) |
| Create a bucket with Key Protect or Hyper Protect Crypto Services managed encryption keys (SSE-KP) by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-key-protect) |
| Create a bucket by using Terraform | [Learn more](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-template#storage-templates) |
{: caption="Table 1. Create bucket requests" caption-side="top"}


To create a bucket, your user must have manager or writer permissions for the {{site.data.keyword.cos_full_notm}} instance where you plan to create the bucket.
{: note}

### Creating a bucket through the {{site.data.keyword.cloud_notm}} UI
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





## Getting the bucket configuration details through the {{site.data.keyword.cloud_notm}} UI
{: #cos_bucket_details}

When you configure a target, you need the bucket name and the private endpoint.

Complete the following steps to get the bucket configuration details through the {{site.data.keyword.cloud_notm}} UI:

1. From the Navigation menu, select **Resource List**.

2. Select the {{site.data.keyword.cos_full_notm}} instance where you plan to create the bucket.

3. Select **Buckets**. Then, select the bucket that you want to use to collect auditing events.

4. Select **Configuration**. Look for the bucket name and the private endpoint.





## Collecting auditing events for a bucket
{: #cos_bucket_audit_events}

You can use the {{site.data.keyword.at_full_notm}} service to track how users and applications interact with {{site.data.keyword.cos_full_notm}} (COS). For more information about the auditing events that are generated for a bucket and its objects, see [Activity Tracker events](/docs/cloud-object-storage?topic=cloud-object-storage-at-events).

To collect auditing events for a bucket, consider the following information:
* Collection of auditing events in your account is optional.
* You must configure each bucket to enable management events, or management and data events. Notice that you cannot enable data events only for a bucket.
* To monitor management events, you must configure a bucket and specify the {{site.data.keyword.at_full_notm}} hosted event search instance where those events will be collected and forwarded.
* To monitor data events, you must select the option **Track data events**. Then, select **read**, **write**, or **read & write** to collect events when an object is uploaded or downloaded from a bucket.

Enable collection of auditing events after you have configured Activity Tracking in the region where the bucket is located.
{: important}


## Listing objects in a bucket
{: #cos_bucket_list_objects}

You can choose any of the following methods to list objects in a bucket:
- [List objects in a given bucket by using the CLI](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-list-objects).
- [List objects in a given bucket by using the API](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-list-objects-v2)
- List objects in a given bucket through the {{site.data.keyword.cloud_notm}} UI.

### List objects in a given bucket through the {{site.data.keyword.cloud_notm}} UI
{: #cos_bucket_list_objects_ui}

Complete the following steps to list the objects in a bucket through the {{site.data.keyword.cloud_notm}} UI:

1. From the Navigation menu, select **Resource List**.

2. Select the {{site.data.keyword.cos_full_notm}} instance where the bucket is available.

3. Select **Buckets**.

4. Select a bucket. The list of objects is displayed.



## Managing access to a bucket
{: #cos_bucket_manage_access}

Access to work with the {{site.data.keyword.cos_short}} service is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).

Every user or service ID that accesses the {{site.data.keyword.cos_short}} service in your account must be assigned an access policy with an IAM role defined. That policy determines what actions the user or service ID can perform within the context of the service or instance you select. The allowable actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM roles.

To define a policy, first you must set the scope. You can define a policy to grant access in any of the following contexts:
* Across all instances of the service in your account
* For an individual service instance in your account
* For a specific bucket within an instance
* For all IAM-enabled services in your account

After you define the scope of the access policy, you must assign a role.
- For more information about what actions are allowed per role within the {{site.data.keyword.cos_short}} service, see [COS Identity and Access Management roles](/docs/cloud-object-storage?topic=cloud-object-storage-iam#iam-roles).
- For more information about bucket permissions per role, see [Bucket permissions](/docs/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions).
- For information about assigning roles, see [Managing IAM access](/docs/account?topic=account-assign-access-resources).

IAM policies are enforced hierarchically, from greatest level of access to most restricted. Conflicts are resolved to the more permissive policy. For example, if a user has both the `Writer` and `Reader` service access role on a bucket, the policy granting the `Reader` role is ignored. This is also applicable to service instance and bucket level policies, for example:
- If a user has a policy granting the `Writer` role on a service instance and the `Reader` role on a single bucket, the bucket-level policy is ignored.
- If a user has a policy granting the `Reader` role on a service instance and the `Writer` role on a single bucket, both policies are enforced and the more permissive `Writer` role will take precedence for the individual bucket.

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned. 
{: important}

To restrict access to a single bucket, ensure that the user or Service ID doesn't have any instance level policies.
{: tip}

For {{site.data.keyword.logs_full_notm}} to access configured {{site.data.keyword.cos_short}} buckets, S2S authorization is required. For more information, see [Creating a S2S authorization to grant access to a bucket](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos&interface=ui).
{: important}



## Monitoring the health of a bucket
{: #cos_bucket_health}

You can use the {{site.data.keyword.mon_full}} service to monitor {{site.data.keyword.cos_short}} (COS) in the {{site.data.keyword.cloud_notm}}. [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-mm-cos-integration).

## CLI commands to manage buckets
{: #cos_bucket_tips}

The following commands might be useful when you work with buckets:

### Check if a bucket exists in your account through the CLI
{: #cos_bucket_tip_1}

Run the following command to determine if a bucket exists in an {{site.data.keyword.cos_full_notm}} instance in your account:

```text
ibmcloud cos bucket-head --bucket BUCKET_NAME
```
{: codeblock}

Where `BUCKET_NAME` is the name of the bucket.
