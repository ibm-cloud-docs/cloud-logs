---

copyright:
  years:  2024, 2026
lastupdated: "2026-03-19"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the metrics bucket for an {{site.data.keyword.logs_full_notm}} instance
{: #configure-metrics-bucket}

Configure a bucket in {{site.data.keyword.cos_full_notm}} to store metrics from logs for long term storage and search.
{: shortdesc}


## Prereqs
{: #configure-metrics-bucket-prereqs}

- The {{site.data.keyword.cos_full_notm}} service can be in the same account as your {{site.data.keyword.logs_full_notm}} instance, or can be located in a different account.

- You must have permissions to create a bucket in an {{site.data.keyword.cos_full_notm}} instance or have the details of an existing bucket.

- You must have permissions to configure a service to service authorization between the {{site.data.keyword.cos_full_notm}} service and the {{site.data.keyword.logs_full_notm}} service.


## Configure an IAM Service to service authorization
{: #configure-metrics-bucket-s2s}
{: step}

You must define a service to service (S2S) authorization between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}} to allow {{site.data.keyword.logs_full_notm}} to read and write data into the metrics bucket.

For more information, see:
- [Creating a S2S authorization to grant access to a bucket when the {{site.data.keyword.logs_full_notm}} instance and the bucket are in the same account](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos).
- [Creating a cross-account S2S authorization to grant access to a bucket when the {{site.data.keyword.logs_full_notm}} instance and the bucket are in different accounts](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos-crossacc).


## Configure the metrics bucket
{: #configure-metrics-bucket-attach}
{: step}

Complete the following steps to configure a metrics bucket for an {{site.data.keyword.logs_full_notm}} instance:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.

3. Select **Logging** &gt; **Instances**. You might need to click the **Cloud Logs** tab to see your {{site.data.keyword.logs_full_notm}} instances.

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
