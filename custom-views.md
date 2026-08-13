---

copyright:
  years:  2024, 2026
lastupdated: "2026-08-10"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Managing custom views in {{site.data.keyword.logs_full_notm}}
{: #custom_views}

In {{site.data.keyword.logs_full}}, you can use custom views to monitor logs that match a specific querying criteria.
{: shortdesc}


## About views
{: #custom_views_ov}

- Views can be public or private.

- Users with `Manager` or `Writer` role for the {{site.data.keyword.logs_full_notm}} service can create and modify custom views.

- To configure a custom view, you can define a query, filter by selected fields, or both.

- Views including column configurations are stored as per instance. If you work with multiple {{site.data.keyword.logs_full_notm}} instances, you must configure and save views in each instance separately.

- You can save column configurations, view mode and layout settings as part of each view and restore automatically when the view is reopened.

- Views can be grouped into folders. The folder order cannot be changed.

- View names must be unique within a folder. 

- The following preferences are saved within saved views. They are restored automatically the next time you open a view:

    Column configuration: The set of fields displayed as columns and their order.

    View mode: Depends on whether the view was last used in standard mode or compact mode. The mode that was active when you last saved the view is restored when you reopen it.

    Query and filters: These are saved only when **Save query and filters** is selected when you save a view. If not selected, the view opens without any pre applied query or filter.

    Time interval: The time range you selected at the time you save is stored with the view and applied when the view is opened.


## Launching views
{: #custom_views_launch}

Complete the following steps to see all views:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs").

3. Click **Logs**. 


## Creating a custom view
{: #custom_views_create}

To configure a custom view, you can define a query, filter by selected fields, or both.
{: note}

Complete the following steps to create a custom view:

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

   3. If you want your view to be the default view, check **Set as default view**.

        This sets the view as the default for you as the user. It does not set the view as the default view for the entire account. 

        You can change your default view at any time by opening a different view and checking **Set as default view** while saving.

   4. Set the privacy of your view. Private views can only be seen by you. You can set a view as **Private** or **Public**.

        The column configuration, selected view mode (compact or standard), and the existing layout are saved as part of the view. These settings are restored automatically the next time a view is opened.


## Editing existing views columns
{: #custom_views_update}

You can update the column layout of any saved view. The column configurations are saved as part of the view.

Complete the following steps to edit the columns of an existing view:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Logs**.

3. Click **All Views** and select the view whose columns you want to change.

4. Click the **Columns** icon.

    A panel opens listing all the available fields.

5. Select the fields you want to display as columns. Deselect any fields you want to delete.

6. (Optional) Reorder columns by dragging the fields to your preferred position.

7. Save the updated column layout by clicking the three dots **...** next to the view name. Select **Save query and filters**. Then, click **Save**.


The new column layout is saved as part of the view and is applied the next time the view is opened. 


## Creating folders
{: #custom_views_folders_create}

The order of the folders cannot be changed.
{: note}

Complete the following steps to create a folder and add saved views to the folder:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Logs**.

3. Click **All Views**.

4. To create a new folder, click the folder icon. Enter a folder name, and click **Create**.


## Orginizing views in folders
{: #custom_views_folders_views}

After you create 1 or more view folders, you can orginize views to folders by dragging them to the folder.



## Deleting views
{: #custom_views_delete}

Complete the following steps to delete a view:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Logs**.

3. Click **All Views**.

4. Select the view you want to delete.

5. Click the delete icon.

6. Confirm that you want to delete the view by clicking **Delete**.


## Deleting folders
{: #custom_views_folder_delete}

Folders must be empty before a folder can be deleted.
{: note}

Complete the following steps to delete a folder:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Logs**.

3. Click **All Views**.

4. Click the folder you want to delete.

5. Click the delete icon.
