---

copyright:
  years:  2024
lastupdated: "2024-10-03"

keywords:

subcollection: cloud-logs

content-type: conref

---

{{site.data.keyword.attribute-definition-list}}


# Conrefs
{: #conrefs}



## Accessing Explore
{: #query-ui}

You can query logs from the Explore screen:

1. [Launch the {{site.data.keyword.logs_full_notm}} UI.](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)
{: #launch-ui}

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

3. (Optional) If you want to explore archived data from the [{{site.data.keyword.monitoring}} or {{site.data.keyword.compliance}} pipelines](/docs/cloud-logs?topic=cloud-logs-tco-optimizer), click **Archive**. To switch back to data currently maintained in the [{{site.data.keyword.frequent-search}} pipeline](/docs/cloud-logs?topic=cloud-logs-tco-optimizer) click **Priority Logs**.



## Resetting filters and search queries
{: #query-reset}

You can clear all filters and queries by clicking **Reset**.



## Saving a view
{: #save-view}

Once you have your view with the log records you want to see by using filters or searches, you can save the view for future use.

To save a view:

1. Click **Unsaved View**.

2. Enter the name for your view.

3. Optionally indicate if you want to save the query and filters as part of the view.

4. Optionally indicate if you want the view set as your default view when opening {{site.data.keyword.logs_full_notm}}

5. Select if you want the view to be private to you or shared with other users.

6. Click **SAVE** to save your view.








## Prereqs
{: #alerts-config-prereqs}

- Learn about alerts in {{site.data.keyword.logs_full_notm}}. For more information, see [Alerting](/docs/cloud-logs?topic=cloud-logs-alerts).
- Check that you have an [{{site.data.keyword.en_short}} instance](/catalog/services/event-notifications){: external} that is in the same account as your {{site.data.keyword.logs_full_notm}} instance and permisions to configure resources in the {{site.data.keyword.en_short}} instance.
- Check that the outbound integration between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_short}} instance is configured. For more information, see [Configuring an outbound integration to connect](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure).



## Choose the type of alert
{: #alerts-config-1}
{: step}

Complete the following steps:

1. In the console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Resource list**.
2. Select your instance of {{site.data.keyword.logs_full_notm}}.
3. In the {{site.data.keyword.logs_full_notm}} navigation, click the **Alerts** icon ![Alerts icon](../icons/alerts.svg "Alerts") > **Alerts Management**.
4. Click **New alert**.
