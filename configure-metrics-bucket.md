---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-24"

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

- You must have an {{site.data.keyword.cos_full_notm}} instance in the same account where your {{site.data.keyword.logs_full_notm}} instance is provisioned.
- You must have permissions to create a bucket in the {{site.data.keyword.cos_full_notm}} instance or have the details of an existing bucket.


## Configure an IAM Service to service authorization
{: #configure-metrics-bucket-s2s}
{: step}

You must define a service to service (S2S) authorization between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}} to allow {{site.data.keyword.logs_full_notm}} to read and write data into the data bucket. For more information, see [Creating a S2S authorization to grant access to a bucket](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-cos).


## Configure the metrics bucket
{: #configure-metrics-bucket-attach}
{: step}

Complete the following steps to configure a metrics bucket for an {{site.data.keyword.logs_full_notm}} instance:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.

3. Select **Logging** &gt; **Instances**. You might need to click the **Cloud Logs** tab to see your {{site.data.keyword.logs_full_notm}} instances.

4. Select the instance to which you want to configure a metrics bucket.

5. In the *Storage* section, select **Edit**.

6. In the **Events to metrics data** section, configure the *Bucket CRN*, and the *Bucket endpoint*.

    Select **Insert CRN from search** to get the list of buckets in your account. You can choose a CRN from the list.

    Select **View endpoints in docs** to find the endpoints per location. Choose the endpoint based on your bucket configuration.

7. Click **Save** to save the configuration.
