---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} dynamic widget
{: #widget_dynamic}

You can create a dynamic widget that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

Use this widget to get suggestions on visualizations that are proposed based on your query data results, and find the best way to present your data results. You can configure Lucene queries, DataPrime queries, and PromQL queries.
{: note}


## How it works
{: #create_dynamic_widget_0}

The dynamic widget analyzes query results and suggests visualizations based on the shape of the data.

By default, the table view is shown when you add the dynamic widget for the first time to the dashboard. Raw data is displayed in JSON format.

Next, you can apply query filters, grouping, or aggregation. The data that is filtered is used to suggest visualizations such as bar charts, pie charts, gauges, line charts and more.

Whenever the query is modified, the dynamic widget re-analyzes the results and updates the list of recommended visualizations.



## Step 1: Enter name and description
{: #create_dynamic_widget_1}

Complete the following steps:

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Dynamic** widget from your side bar.

2. Replace *New dynamic widget* with the **Name** for the widget.

3. Enter a description.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Add description**.


## Step 2: Configure the query to define the data set
{: #create_dynamic_widget_2}

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


## Step 3: Select the visualization widget
{: #create_dynamic_widget_3}

After you enter the query,

1. Click **Suggest Visualizations** to get a list of the valid visualizations.

2. Choose one visualization to display the data in this widget. Then, configure the widget for that visualization. For information on visualization customization, see the information for each visualization type:

    * [Data table](/docs/cloud-logs?topic=cloud-logs-widget_datatable)

    * [Gauge](/docs/cloud-logs?topic=cloud-logs-widget_gauge)

    * [Horizontal bar chart](/docs/cloud-logs?topic=cloud-logs-widget_horizontalbar).

    * [Line chart](/docs/cloud-logs?topic=cloud-logs-widget_linechart).

    * [Pie chart](/docs/cloud-logs?topic=cloud-logs-widget_piechart)

    * [Vertical bar chart](/docs/cloud-logs?topic=cloud-logs-widget_verticalbar)

    * Polystat

## Step 4: Add 1 or more rules
{: #create_dynamic_widget_4}

   Select **Add Rule** to add a new rule with different properties.

    **Thresholds.**: Choose the base **Thresholds**. That is, when the gauge should appear green and red. Add additional thresholds - yellow and orange - if necessary.


## Step 5: Save the widget
{: #create_dynamic_widget_5}

Complete the following steps:

1. [Optional] Set the widget's dashboard time if you want to use a time range that is different from the Dashboard selected one.

2. Click **Save** to save your widget.

3. [Optional] Add a custom action. For more information, see [Using actions to integrate with third-party services](/docs/cloud-logs?topic=cloud-logs-actions).




## Known limitations
{: #create_dynamic_widget_limitations}

- Dynamic Widgets display up to 2,000 records per query result.

    When a query returns more than 2,000 records, the widget shows a **Partial Data** notice. The widget includes only the first 2,000 rows returned.

    To analyze the complete result set, narrow the time range or apply filters to reduce the number of returned records.

- For **table widgets**, the following limitations apply:

    Interactions with the data by using `Filter In` or `Filter Out` are not included in the URL and are not persisted when you share the link.

    When you have a multi-query table with joins such as an outer join, the features to `Filter In` and `Filter Out` are not available.

    You can only filter table widgets with structured columns. Columns that include Text or JSON content display raw data and do not support column-based filtering or filter actions.





