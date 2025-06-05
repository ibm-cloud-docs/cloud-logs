---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-04"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Sharing URLs
{: #share_url}

Sharing URLs from {{site.data.keyword.logs_full}} lets you collaborate with team members and other stakeholders by providing them access to logs, traces, and visualizations. Whether it’s for troubleshooting, monitoring, or reporting, sharing views by URLs lets everyone have access to the same data and insights.
{: shortdesc}

Use this feature to:

* **Enhance collaboration.** Sharing logs, traces, and queries enables better collaboration across teams. With shared views, multiple team members can monitor and analyze the data at the same time, improving response times and spreading the workload.

* **Eliminate back-and-forth.** Instead of going back and forth over email or messaging to explain a log or create a query, sharing a view allows teams to immediately access the necessary data and collaborate without confusion.

* **Promote transparency and accountability.** Shared views promote transparency, allowing all stakeholders to monitor system performance. This transparency helps increase accountability, as everyone has visibility into the data.

A shared URL can include the following elements:

* Time ranges:

   * Relative: This option lets users share a dashboard that always displays data relative to the current time. For example, selecting `Last 15 minutes` will show data from the most recent 15 minutes, dynamically adjusting based on when the link is accessed. The dashboard will continuously refresh to reflect the latest data.

   * Fixed: This option allows users to share a dashboard view locked to a specific, fixed time period (for example, 23:33:03 to 25:05:15). When the link is opened, the dashboard will display data for the exact start and end time selected at the moment of sharing, ensuring that the view remains consistent regardless of when the link is accessed. This is useful for sharing a snapshot of a particular moment in time.

      If a fixed-time shared URL containing {{site.data.keyword.frequent-search}} logs is accessed after an extended period, the log entries might have been moved to All Logs storage due to retention policies.  To ensure no data is missed, it is recommended to share these URLs with the All Logs option selected.
      {: important}

* Filters and queries:

   * {{site.data.keyword.frequent-search}} or All Logs

   * Filter panel state

   * Lucene or DataPrime queries

* UI layout:

   * Column/row settings

   * Widget and legend states

You can analyze the URL itself to understand what is being shared.

* Unsaved and private views are sent as a temporary links with an ID. For example, `id=041pSG5WuixfglBim2FOc&page=0`.

* Public views are sent as a complete permalink (`permalink=true`) with view ID (`viewId`), time range (`time`), and query syntax type (`querySyntax`). For example, `https://dashboard.au-syd.logs.cloud.ibm.com/b1b01411-be1d-41a8-a0117-c61b7bd194a8/#/query-new/logs?viewId=1924&time=from:now-15m,to:now&page=0&permalink=true`.


## Sharing views as part of shared URLs
{: #share_url_view}

The **Logs** views help organize relevant log information, creating customized snapshots of page elements that help users work more efficiently and access critical data. Here are the 3 types of views available on any **Logs** page.

* A public view is a saved view whose privacy settings have been set to public. Once public, all team members have access to the view in the shared view dropdown.

   * The shared URL of the saved public view includes filters, the query, the time range and view name.

   * The public view might contain unsaved changes. If you choose to share it, you'll be prompted to either save the changes before sharing or share the current view without saving. The shared URL of an unsaved public view includes filters, the query, the time range and the layout.

* A private view is a saved view whose privacy settings have been set to private. This view is only accessible to the user that created it. If you attempt to share a private view, the shared URL acts as an unsaved view with a same parameters and UI layout.

* An unsaved view can be shared. If a user chooses to share an unsaved view, including the full UI layout as part of the query link will keep the link temporary with an expiry of 2 weeks. The shared URL includes filters, the query, the time range and the layout.

If you copy the URL directly from the address bar, the link will be temporary, expiring in 2 weeks. However, if you use the **Share** option to share the link, the expiration period is extended to 3 months. Also, each time the URL is accessed, its expiration period is reset to 3 months from the cache. If the URL is not accessed during this time, it will expire.
{: important}


## Creating a temporary link
{: #share_url_temp}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](/icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Logging**. By default **Instances** are displayed. 

4. Click the **Cloud Logs** tab.

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

   If the instances are not displayed, click **Instances** > **Cloud Logs** to display the list of logging instances.

5. Click **Open dashboard** for your selected instance.

6. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

7. Customize your current view:

   * Select the filtering mode and filtering criteria.

   * Run Lucene or DataPrime queries on your data.

   * Adjust the rows and columns.

   * Display or hide the widgets and configure their legends.

   * Select desired time range.

8. Copy the URL directly from the address bar of your browser.

The URL is ready to be shared and will remain active for 2 weeks.

## Creating an extendable link
{: #share_url_extend}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](/icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Logging**. By default **Instances** are displayed. 

4. Click the **Cloud Logs** tab.

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

   If the instances are not displayed, click **Instances** > **Cloud Logs** to display the list of logging instances.

5. Click **Open dashboard** for your selected instance.

6. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

7. Customize your current view:

   * Select the filtering mode and filtering criteria.

   * Run Lucene or DataPrime queries on your data.

   * Adjust the rows and columns.

   * Display or hide the widgets and configure their legends.

   * Select desired time range.

8. Click **Share** on the screen toolbar or in the **Settings** menu.

9. Click Copy URL.

The URL is ready to be shared and will remain active for 3 months at a time. Each time the URL is accessed, the expiration period is reset to 3 months from the cache. If the URL remains unused during this period, it will expire.


## Creating a shareable query permalink
{: #share_url_perm}

A URL sharing a public view is always permanent and accessible to all of your team members. If you've made changes to a public view, you'll be prompted to either save your changes before sharing or share the current view without saving.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](/icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Logging**. By default **Instances** are displayed. 

4. Click the **Cloud Logs** tab.

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

   If the instances are not displayed, click **Instances** > **Cloud Logs** to display the list of logging instances.

5. Click **Open dashboard** for your selected instance.

6. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

7. Customize your current view:

   * Select the filtering mode and filtering criteria.

   * Run Lucene or DataPrime queries on your data.

   * Adjust the rows and columns.

   * Display or hide the widgets and configure their legends.

   * Select desired time range.

8. Click **Share** on the screen toolbar or in the **Settings** menu.

9. Click Copy URL.

10. For an unsaved public view, choose whether to save the changes before sharing or share the current view without saving.



## Creating a private view
{: #share_url_private}

A private view is a saved view whose privacy settings have been set to private. This view is only accessible to the user that created it. If you attempt to share a private view, it acts as an unsaved view with the same attributes and behavior.

## Example of creating a sharable URL
{: #shared_url_example}

This example creates a customized view of applications with errors (severity `Error`). The apps are grouped alphabetically and aggregated in a descending list, based on data collected over the past hour.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](/icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Logging**. By default **Instances** are displayed. 

4. Click the **Cloud Logs** tab.

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

   If the instances are not displayed, click **Instances** > **Cloud Logs** to display the list of logging instances.

5. Click **Open dashboard** for your selected instance.

6. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

7. Run this DataPrime query.

   ```text
   source logs 
   | filter $m.severity == ERROR 
   | groupby $l.applicationname calculate count() as error_count
   ```
   {: codeblock}

8. In the {{site.data.keyword.logs_full}} UI time picker, select the **Last 1 hour** time range.

9.  Click the ellipsis (…) next to **Unsaved View**.

10. In **Create a New View**:

    * Enter a meaningful view name.
    * Verify that **Save query and filters** is enabled.
    * Set **Privacy settings** to **Public**.

11. Click **Create**.

12. Click **Share** on the **Logs** view toolbar.

13. Click **Copy URL**.

    A URL similar to this will be copied to your clipboard: `https://dashboard.au-syd.logs.cloud.ibm.com/#/query-new/logs?viewId=83918&querySyntax=dataprime&time=from:now-1h,to:now&page=0&permalink=true`. It includes filters, your DataPrime query, the selected time range, and the ID of the view.

14. Share the URL with the intended recipients.
