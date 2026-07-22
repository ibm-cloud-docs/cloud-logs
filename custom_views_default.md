---

copyright:
  years:  2024, 2026
lastupdated: "2026-07-22"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a default view per user
{: #custom_views_default}

In {{site.data.keyword.logs_full}}, each user can select a different custom view as their instance default view when they launch *Explorer*.
{: shortdesc}

A user can configure any custom view as their default view. This setting is applicable only to the user's profile in the {{site.data.keyword.logs_full_notm}} instance.
{: note}

If you work with multiple {{site.data.keyword.logs_full_notm}} instances, you set a default view in each instance separately.
{: note}

- The default view opens automatically each time the user navigates to **Explore logs**.
- The user can change the default view at any time by opening a different view and checking **Set as default view** while saving.
- Users with `Manager` or `Writer` role for the {{site.data.keyword.logs_full_notm}} service can create a public custom view with the column layout and filter configurations for ingested data that users can choose to use as their default view.


## Launch the {{site.data.keyword.logs_full_notm}} UI
{: #custom_views_default_step1}
{: step}

[Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

## Create the custom view as default
{: #custom_views_default_step2}
{: step}


To configure a custom view, you can define a query, filter by selected fields, or both.
{: note}

Complete the following steps to create a custom view as a default view:

1. Select the fields to be included in the view. By default you can select *Applications*, *Subsystems*, and log *Severities*.

2. (Optional) Add additional filters click **+ Add Filter** and select and configure additional field and filter values.

3. Select if you want to view only include **Priority Logs** (those in the {{site.data.keyword.frequent-search}} pipeline) or **All Logs**, that is, logs that are stored in {{site.data.keyword.cos_full_notm}}. Logs in {{site.data.keyword.cos_full_notm}} includes logs collected through all the data pipelines.

4. (Optional) Add a Lucene or DataPrime query to further filter your data.

5. Specify the time interval for the view, for example *Last 2 Days*.

6. Configure the columns by clicking the **Column** icon and selecting the fields you want to display.

7. Save your view by clicking the three dots **...**

   1. Enter a name for your view.

   2. If you want to save the query and filter values you configured, check **Save query and filters**.

   3. Check **Set as default view**.

        This sets the view as the default for you as the user. It does not set the view as the default view for the entire account.

        The default view opens automatically each time you navigate to **Explore logs**.

        You can change your default view at any time by opening a different view and checking **Set as default view** while saving.

   4. Set the privacy of your view to **Public**.

        The column configuration, selected view mode (compact or standard), and the existing layout are saved as part of the view. These settings are restored automatically the next time a view is opened.


## Changing a default view
{: #custom_views_default_change}



Complete the following steps to change a default view:

1. Open any view you want to set as default.

2. Click the three dots **...** next to the view name.

3. Click **Save view.**

4. Click **Set as default view**.

5. Click **Save**.
