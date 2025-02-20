---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-20"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring buckets for long term storage and search
{: #about-bucket}

Configure a data bucket and a metrics bucket in {{site.data.keyword.cos_full}} to store your {{site.data.keyword.logs_full_notm}} data for long term storage and search.
{: shortdesc}

You can configure the same bucket for data and metrics. However, notice that the {{site.data.keyword.logs_full_notm}} service needs deletion permission on metrics files. Therefore, if you need to configure your bucket with lifecycle policies to manage log data files in the bucket, you must use different buckets to store your log data and your metrics data.
{: important}

{{site.data.keyword.logs_full_notm}} does not support {{site.data.keyword.cos_full}} buckets configured with [retention policies](/docs/cloud-object-storage?topic=cloud-object-storage-immutable), [object lock policies](/docs/cloud-object-storage?topic=cloud-object-storage-ol-overview), or with [public access enabled](/docs/cloud-object-storage?topic=cloud-object-storage-iam-public-access).
{: restriction}

For production environments, consider using different buckets for data and for metrics.
{: tip}

You should create a bucket with _Cross Region_ resiliency to store and access data across multiple geographical regions to ensure high availability, durability, and disaster recovery capabilities. See [Creating and modifying {{site.data.keyword.cos_full_notm}} buckets](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints#endpoints-geo).
{: important}


## About buckets
{: #about-bucket-ov}

{{site.data.keyword.cos_full_notm}} is a highly available, durable, and secure platform for storing unstructured data. The files that are uploaded into {{site.data.keyword.cos_full_notm}} are called objects. Objects can be anywhere from a few bytes up to 10TB. They are organized into buckets that serve as containers for objects, and which can be configured independently from one another in terms of locations, resiliency, billing rates, security, and object lifecycle. For more information, see [What is {{site.data.keyword.cos_full_notm}}?](/docs/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage).

To manage buckets, your user must be granted permissions to work with buckets on the {{site.data.keyword.cos_full_notm}} instance. For more information about roles, see [Identity and Access Management roles](/docs/cloud-object-storage?topic=cloud-object-storage-iam).

To create a bucket, you can choose 1 of the following options:

| Action             | More info |
|--------------------|-----------|
| Create a bucket through the {{site.data.keyword.cloud_notm}} UI | [Learn more](/docs/atracker?topic=atracker-cos#cos_create_bucket_ui) |
| Create a bucket through the {{site.data.keyword.cloud_notm}} CLI | [Learn more](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-create-bucket) |
| Create a bucket by using cURL | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-curl#curl-add-bucket) |
| Create a bucket by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-new-bucket) |
| Create a bucket with a different storage class by using the REST API| [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-storage-class) |
| Create a bucket with Key Protect or Hyper Protect Crypto Services managed encryption keys (SSE-KP) by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-key-protect) |
| Create a bucket by using Terraform | [Learn more](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-template#storage-templates) |
{: caption="Create bucket requests" caption-side="top"}

For more information, see [Getting started with {{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).



## IAM Service to service authorization
{: #about-bucket-s2s}

You must define a service to service (S2S) authorization between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}} to allow {{site.data.keyword.logs_full_notm}} to read and write data into the buckets. For more information, see [Creating a S2S authorization to grant access to a bucket](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos).


## Data bucket
{: #about-bucket-data}

You can configure a data bucket for a {{site.data.keyword.logs_full_notm}} instance.

- The data bucket stores and retains logs for as long as you need them.

- You can configure a data bucket in the same region where the {{site.data.keyword.logs_full_notm}} instance is provisioned.

    If you have regulatory and compliance requirements, check the location where you can create the bucket. Then, if performance is critical, consider creating the bucket in the same region where the {{site.data.keyword.logs_full_notm}} instance is provisioned.

- You are responsible for the maintenance of the data bucket.

For more information, see [Configuring the data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket).


{{_include-segments/data-bucket-restrictions.md}}

## Metrics bucket
{: #about-bucket-metrics}

You can configure a metrics bucket for a {{site.data.keyword.logs_full_notm}} instance.

- The metrics bucket stores and retains metrics from your events in a long-term index for as long as you need them.

    When you enable metrics, you can generate metrics from logs. These metrics are stored in the metrics bucket as [Prometheus index blocks](https://github.com/prometheus/prometheus/blob/main/tsdb/docs/format/index.md){: external}.

- You can configure a metrics bucket in the same region where the {{site.data.keyword.logs_full_notm}} instance is provisioned.

- You are responsible for the maintenance of the metrics bucket.

    If you have regulatory and compliance requirements, check the location where you can create the bucket. Then, if performance is critical, consider creating the bucket in the same region where the {{site.data.keyword.logs_full_notm}} instance is provisioned.

For more information, see [Configuring the metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
