---

copyright:
  years:  2024
lastupdated: "2024-08-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Managing custom views in {{site.data.keyword.logs_full_notm}}
{: #custom_views}

{{site.data.keyword.logs_full}} custom views feature helps organize specific, relevant log information, as well as create views that help other users work and retrieve important data more efficiently. You can define private and shared views.
{: shortdesc}

## About views
{: #custom_views_ov}

- You can configure views to see logs that match a specific filtering criteria.
- Views can be shared (public) or private.
- To configure a custom view, you can define a query, filter by selected fields, or both.
- Views can be grouped into folders.
- View names must be unique within a folder.
- You can configure {{site.data.keyword.iamlong}} to manage the permissions that you grant users to work with private and shared views in an {{site.data.keyword.logs_full_notm}} instance. [Granting permissions to work with views](/docs/cloud-logs?topic=cloud-logs-iam-views).


## Accessing views
{: #access_view}

In the left-hand navigation, click **Explore logs** > **Logs**.

The last view you had opened will be displayed. If no view was previously open, all views will be displayed.


## Creating a custom view
{: #create_view}

To configure a custom view, you can define a query, filter by selected fields, or both.
{: note}

Do the following to create a custom view.

1. Select the fields to be included in the view. By default you can select *Applications*, *Subsystems*, and log *Severities*.

2. (Optional) Add additional filters click **+ Add Filter** and select and configure additional field and filter values.

3. Select if you want you view to only include **Priority Logs** (those in the {{site.data.keyword.frequent-search}} pipeline) or **All Logs**, that is, logs that are stored in {{site.data.keyword.cos_full_notm}}. Logs in {{site.data.keyword.cos_full_notm}} includes logs collected through all the data pipelines.

4. (Optional) Add a Lucene or DataPrime query to further filter your data.

5. Specify the time interval for the view, for example *Last 2 Days*.

6. Save your view by clicking the three dots **...**

   1. Enter a name for your view.

   2. If you want to save the query and filter values you configured, check **Save query and filters**.

   3. If you want your view to be the default view, check **Set as default view**.

   4. Set the privacy of your view. Private views can only be seen by you. You can set a view as **Private** or **Shared**.



## Organizing views in folders
{: #folders_views}

Do the following to create a folder and add saved views to the folder.

1. Click **All Views**.

2. To create a new folder, click the folder icon. Enter a folder name, and click **Create**.

3. Move views to folders by dragging them to the folder.


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
