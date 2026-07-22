---

copyright:
  years:  2024, 2026
lastupdated: "2026-07-22"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Managing custom views in {{site.data.keyword.logs_full_notm}}
{: #custom_views}

{{site.data.keyword.logs_full}} custom views feature helps save a specific column layout, organize specific, relevant log information, as well as create views that help other users work and retrieve important data more efficiently. You can define private and public views.
{: shortdesc}

## About views
{: #custom_views_ov}

You can configure views to see logs that match a specific filtering criteria.

- Views can be public or private.
- To configure a custom view, you can define a query, filter by selected fields, or both.
- You can save column configurations, view mode and layout settings as part of each view and restore automatically when the view is reopened.
- Views can be grouped into folders. The folder order cannot be changed.
- View names must be unique within a folder.
- You can configure {{site.data.keyword.iamlong}} to manage the permissions that you grant users to work with private and public views in an {{site.data.keyword.logs_full_notm}} instance. [Granting permissions to work with views](/docs/cloud-logs?topic=cloud-logs-iam-views).
- Each user can configure a custom view as their default view. The user's default view opens automatically when the user launches **Explore Logs**.
- You can create a public custom view with the column layout and filter configurations for your data that users can choose to use as their default view.

Views including column configurations are stored as per instance. If you work with multiple instances, you must configure and save views in each instance separately
{: note}


The following preferences are saved within saved views. They are restored automatically the next time you open a view:

* Column configuration

    The set of fields displayed as columns and their order.

* View mode

    Depends on whether the view was last used in standard mode or compact mode. The mode that was active when you last saved the view is restored when you reopen it.

* Query and filters

    These are saved only when **Save query and filters** is selected when you save a view. If not selected, the view opens without any pre applied query or filter.

* Time interval

    The time range you selected at the time you save is stored with the view and applied when the view is opened.


## Accessing views
{: #access_view}

In the left navigation within a dashboard, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

The last view you had opened will be displayed. If no view was previously open, all views will be displayed.


## Creating a custom view
{: #create_view}

To configure a custom view, you can define a query, filter by selected fields, or both.
{: note}

Do the following to create a custom view.

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Select the fields to be included in the view. By default you can select *Applications*, *Subsystems*, and log *Severities*.

3. (Optional) Add additional filters click **+ Add Filter** and select and configure additional field and filter values.

4. Select if you want to view only include **Priority Logs** (those in the {{site.data.keyword.frequent-search}} pipeline) or **All Logs**, that is, logs that are stored in {{site.data.keyword.cos_full_notm}}. Logs in {{site.data.keyword.cos_full_notm}} includes logs collected through all the data pipelines.

5. (Optional) Add a Lucene or DataPrime query to further filter your data.

6. Specify the time interval for the view, for example *Last 2 Days*.

7. Configure the columns by clicking the **Column** icon and selecting the fields you want to display.

8. Save your view by clicking the three dots **...**

   1. Enter a name for your view.

   2. If you want to save the query and filter values you configured, check **Save query and filters**.

   3. If you want your view to be the default view, check **Set as default view**.

        This sets the view as the default for you as the user. It does not set the view as the default view for the entire account.

        The default view opens automatically each time you navigate to **Explore logs**.

        You can change your default view at any time by opening a different view and checking **Set as default view** while saving.

   4. Set the privacy of your view. Private views can only be seen by you. You can set a view as **Private** or **Public**.

        The column configuration, selected view mode (compact or standard), and the existing layout are saved as part of the view. These settings are restored automatically the next time a view is opened.


## Editing existing views columns
{: #existing_view_editing}

You can update the column layout of any saved view. The column configurations are saved as part of the view.

Do the following to edit the columns of an existing view:

1. In the left navigation within a dashboard, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

2. Click **All Views** and select the view whose columns you want to change.

3. Click the **Columns** icon.

A panel opens listing all the available fields.

4. Select the fields you want to display as columns. Deselect any fields you want to delete.

5. (Optional) Reorder columns by dragging the fields to your preferred position.

6. Save the updated column layout by clicking the three dots **...** next to the view name.

   1. Click **Save view**.

   2. Confirm that the **Save query and filters** option display your intent.

   3. Click **Save**.

The new column layout is saved as part of the view and is applied the next time the view is opened.



## Organizing views in folders
{: #folders_views}

Do the following to create a folder and add saved views to the folder.

1. Click **All Views**.

2. To create a new folder, click the folder icon. Enter a folder name, and click **Create**.

3. Move views to folders by dragging them to the folder.

   The order of the folders cannot be changed.
   {: note}


## Deleting views
{: #delete_view}

Do the following to delete a view

1. Click **All Views**.

2. Click the view you want to delete.

3. Click the delete icon.

4. Confirm that you want to delete the view by clicking **Delete**.

## Deleting folders
{: #delete_folder}

Folders must be empty before a folder can be deleted.
{: note}

Do the following to delete a folder.

1. Click **All Views**.

2. Click the folder you want to delete.

3. Click the delete icon.
