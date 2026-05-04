---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-04"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Working with the Data Usage dashboard
{: #data-usage-dashboard}

In {{site.data.keyword.logs_full_notm}}, you can get detailed insights into your observability data usage through the *Data Usage dashboard*.
{: shortdesc}


## Prerequisites
{: #data-usage-prereqs}

Complete the following tasks to access the Data Usage dashboard:
1. Attach a metrics bucket to your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Configuring the metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
2. Enable Data Usage metrics. For more information, see [Enabling Data Usage metrics](/docs/cloud-logs?topic=cloud-logs-data-usage-metrics).
3. Install the *System Monitoring* extension. For more information, see [System Monitoring extension](/docs/cloud-logs?topic=cloud-logs-extensions-system-monitoring).

Once enabled, data will be collected and shown in the dashboard.


## Launching the Data Usage dashboard from the Data Usage page
{: #data-usage-dashboard-launch}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Data Usage**.

    The *Data Usage* page opens.

    ![Data Usage](/images/data-usage.png "Data Usage"){: caption="Data Usage" caption-side="bottom"}

3. Select the **Action menu** icon ![Action menu icon](/icons/tasks.png "Action menu") > **View Data Usage dashboard**.

    ![Data Usage dashboard](/images/data-usage-dashboard.png "Data Usage dashboard"){: caption="Data Usage dashboard" caption-side="bottom"}

The Data Usage dashboard opens.


## Launching the Data Usage dashboard from the Custom dashboards page
{: #data-usage-dashboard-launch-dashboards}

You must have the *System Monitoring* extension deployed. For more information, see [System Monitoring extension](/docs/cloud-logs?topic=cloud-logs-extensions-system-monitoring).
{: note}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Dashboards** icon ![Dashboards icon](/icons/dashboards.svg "Dashboards") > **Custom Dashboards**.

3. In the *System Monitoring* folder, select **Data usage**.
