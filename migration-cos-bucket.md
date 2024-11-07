---

copyright:
  years:  2024
lastupdated: "2024-11-07"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Migrating instances with archiving configured
{: #migration-cos-bucket}

You can use the Migration tool to migrate the archiving configuration of an {{site.data.keyword.at_full_notm}} instance or {{site.data.keyword.la_full_notm}} instance.
{: shortdesc}



## Before you begin
{: #migration-cos-bucket-prereqs}

- Learn about migration. For more information, see [Migrating {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-migration-intro).

- Learn about the Migration tool. For more information, see [Migrating tool](/docs/cloud-logs?topic=cloud-logs-migration-tool).

- Learn about the {{site.data.keyword.cos_full_notm}} buckets that you can configure with an {{site.data.keyword.logs_full_notm}} instance. For more information, see [Configuring buckets](/docs/cloud-logs?topic=cloud-logs-about-bucket).


### Buckets in {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}}
{: #migration-cos-bucket-bucket-1}

When you configure archiving on an {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} instance, consider the following information:
- Buckets are optional. You only need a bucket to store data for long term retention.
- Only logs that are ingested and available for search are saved into the bucket.
- Data stored in the bucket is compressed.
- The data cannot be queried through the UI.
- You must use service ID credentials to allow your {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} instance to write data into the bucket.


The following figure shows the high level view of an {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} instance and the {{site.data.keyword.cos_full_notm}} buckets that you might configure:

![High-level view of an {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} instance and the {{site.data.keyword.cos_full_notm}} buckets](/images/migration-bucket-logdna.svg "Account overview of handling activity tracking events."){: caption="High-level view of an {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} instance and the {{site.data.keyword.cos_full_notm}} buckets" caption-side="bottom"}


### Buckets in {{site.data.keyword.logs_full_notm}}
{: #migration-cos-bucket-bucket-2}

When you attach buckets to an {{site.data.keyword.logs_full_notm}} instance, consider the following information:

- Buckets are optional when you configure your {{site.data.keyword.logs_full_notm}} instance.

    Features such as TCO policy optimizer, querying archive data, and collecting logs from metrics require access to the data bucket or the metrics bucket depending on the feature.{: note}

- All logs that are ingested and not blocked are saved into the bucket.

- Data is compressed at different levels and formatted for easy search based on the TCO pipeline.

- Authorization between the {{site.data.keyword.logs_full_notm}} instance and the buckets is done by using service to service authorizations.

- You can query data stored in the data bucket through the UI.


The following figure shows the high level view of an {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.cos_full_notm}} buckets that you might configure:

![High-level view of an {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.cos_full_notm}} buckets](/images/migration-bucket-logs.svg "Account overview of handling activity tracking events."){: caption="High-level view of an {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.cos_full_notm}} buckets" caption-side="bottom"}

## Migrating the archiving configuration
{: #migration-archive-config}

The archiving configuration is migrated when you migrate an instance.
{: note}



## Known issues
{: #migration-cos-issues}

- You cannot use as your metrics bucket a bucket with lifecycle policies where data is retained and cannot be deleted.

## Known Migration tool limitations
{: #migration-cos-limitations}

- Lifecycle policies are not migrated through the Migration tool.
