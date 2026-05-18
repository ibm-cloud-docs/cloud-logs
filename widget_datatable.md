---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-18"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a data table widget
{: #widget_datatable}

You can create a data table widget that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}


## Step 1: Enter name and description
{: #widget_datatable_1}

Complete the following steps:

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Data Table** widget from your side bar.

2. Replace *New data table* with the **Name** for the widget.

3. Enter a description.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Add description**.


## Step 2: Configure the query to define the data set
{: #widget_datatable_2}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. For `Query 1`, complete the following steps:

    Select the **data type**. Valid values are: `Logs`, `Metrics`, and `DataPrime`.

    Select the **source**. Valid options are: `Priority Insights` and `Analyze and Alert`.

    You can rename the query. Select the ![Action icon](/icons/action-menu-icon.svg "Action icon") and then click **Rename query**.

3. Enter the query.

    When the data type is `DataPrime`, enter a Dataprime query in the **Query** field.

    When the data type is `Logs`, enter a Lucene query in the **Query** field. You can apply filters and aggregations.

    When the data type is `Metrics`, specify the metric or desired PromQL in the **Query** field. You can apply filters and aggregations.

## Step 3: Configure the widget
{: #widget_datatable_3}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. Choose the table type in the *Table View* section. Valid values are `Events view` and `Aggregation view`.

    When using logs as the data source, you can choose between the Events view and the Aggregated view. Metrics are automatically generated in aggregated view.

    **Event tables**: Display a table with a list of logs ordered by time by default. You can change this to be sorted by other columns later with additional metadata and labels relevant to those events, similar to the view you see in the Explore screen.

    **Aggregation tables**: Creates a table of values, grouped by a field or fields you specify. Each column represents a different value depending on the chosen group. Values could be a simple count or an average of the values for the specific field, for each of the defined group-by values.

3. Enter the number of **Results per page**. Valid options are: `10 rows`, `20 rows`, `50 rows` and `100 rows`.

4. Choose how to view the log lines. Valid values are: `1 line`, `2 lines`, `condensed`, `JSON`, and `list`.

5. In the columns section, click **Manage** to choose the columns that you want to display, and their order.

## Step 4: Save the widget
{: #widget_datatable_5}

Complete the following steps:

1. [Optional] Set the widget's dashboard time if you want to use a time range that is different from the Dashboard selected one.

2. Click **Save** to save your widget.

3. [Optional] Add a custom action. For more information, see [Using actions to integrate with third-party services](/docs/cloud-logs?topic=cloud-logs-actions).
