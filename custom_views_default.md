---

copyright:
  years:  2024, 2026
lastupdated: "2026-07-23"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Managing default views
{: #custom_views_default}

In {{site.data.keyword.logs_full}}, each user can select a different custom view as their instance's default view when they launch *Explorer*.
{: shortdesc}

A user can use any custom view as their default view. This setting is applicable only to the user's profile in the {{site.data.keyword.logs_full_notm}} instance.
{: note}

If you work with multiple {{site.data.keyword.logs_full_notm}} instances, you can set a default view in each instance separately.
{: note}

- A user can set any public view or private view that the user creates as a default view.
- The default view opens automatically each time the user navigates to **Explore logs**.
- The user can change the default view at any time by opening a different view and checking **Set as default view** while saving.



## Creating a custom view as default
{: #custom_views_default_create}


To configure a custom view, you can define a query, filter by selected fields, or both.

Complete the following steps to create a custom view as a default view:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Logs**.

3. Select the fields to be included in the view. By default you can select *Applications*, *Subsystems*, and log *Severities*.

4. (Optional) Add additional filters click **+ Add Filter** and select and configure additional field and filter values.

5. Select if you want to view only include **Priority Logs** (those in the {{site.data.keyword.frequent-search}} pipeline) or **All Logs**, that is, logs that are stored in {{site.data.keyword.cos_full_notm}}. Logs in {{site.data.keyword.cos_full_notm}} includes logs collected through all the data pipelines.

6. (Optional) Add a Lucene or DataPrime query to further filter your data.

7. Specify the time interval for the view, for example *Last 2 Days*.

8. Configure the columns by clicking the **Column** icon and selecting the fields you want to display.

9. Save your view by clicking the three dots **...**

    1. Enter a name for your view.

    2. If you want to save the query and filter values you configured, check **Save query and filters**.

    3. Check **Set as default view**.

        This sets the view as the default for you as the user. It does not set the view as the default view for the entire account.

        The default view opens automatically each time you navigate to **Explore logs**.

        You can change your default view at any time by opening a different view and checking **Set as default view** while saving.

    4. Set the privacy of your view to **Public**.

        The column configuration, selected view mode (compact or standard), and the existing layout are saved as part of the view. These settings are restored automatically the next time a view is opened.


## Changing the default view
{: #custom_views_default_change}

Complete the following steps to change a default view:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Logs**.

3. Open any view you want to set as default.

4. Click the three dots **...** next to the view name.

6. Click **Set as default view**.

7. Click **Save**.
