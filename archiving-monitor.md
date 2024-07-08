---

copyright:
  years:  2024
lastupdated: "2024-04-01"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring archiving by using {{site.data.keyword.mon_full_notm}} (WIP)
{: #archiving-monitor}

{{site.data.keyword.cos_full_notm}} is integrated with the {{site.data.keyword.mon_short}} service. {{site.data.keyword.mon_short}} provides a default template that you can customize to monitor the bucket that you configure to store data for long term from an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}


Complete the following steps to monitor the {{site.data.keyword.messagehub}} instance:

1. Check that you have an instance of the {{site.data.keyword.mon_short}} in the same region as your {{site.data.keyword.cos_full_notm}} instance. This instance must be configured to collect platform metrics. For more information, see [Enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).

2. [Launch the {{site.data.keyword.mon_short}} UI](/docs/monitoring?topic=monitoring-launch).

3. In the **Dashboards** section, go to **Dashboard templates** and select the template **IBM** > **IBM COS Bucket**.

4. Create a copy of the template by clicking **Create custom dashboard**.

    Select **2W** resolution.

    You can use the metric *ibm_cos_bucket_used_bytes* to see the used space in bytes.

    You can use the metric *ibm_cos_bucket_object_count* to see how many objects are uploaded into the bucket.

5. (Optional) Edit each panel to view data by bucket name and storage class.

    ![Edit panel.](images/archive-monitor-1.png "Edit panel"){: caption="Edit panel" caption-side="bottom"}

    Then, customize the metric to see data per storage class.

    ![Customize metric.](images/archive-monitor-2.png "Customize metric"){: caption="Customize metric" caption-side="bottom"}

    Check that the resolution is set to **10M**.


For more information, see [Using {{site.data.keyword.mon_short}} with {{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-mm-cos-integration).
