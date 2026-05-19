---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-19"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} DataPrime creator widget
{: #widget_dataprime}

You can create the optimum visualization for your data based on your DataPrime query that can then be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

The [DataPrime language](/docs/cloud-logs?group=dataprime) can be used to query your data and transform it through operations tailored to your specific needs. This includes calculation, extraction, and aggregation.

Use this widget to get suggestions on visualizations that are proposed based on your DataPrime query data results, and find the best way to present your data results.
{: note}


## Step 1: Enter name and description
{: #widget_dataprime_1}

Complete the following steps:

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **DataPrime creator** widget from your side bar.

2. Replace *DataPrime* with the **Name** for the widget.

3. Enter a description.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Add description**.


## Step 2: Configure the query to define the data set
{: #widget_dataprime_2}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. For `Query 1`, complete the following steps:

    Select the **data type** `DataPrime`.

    Select the **source**. Valid options are: `Priority Insights` and `Analyze and Alert`.

    You can rename the query. Select the ![Action icon](/icons/action-menu-icon.svg "Action icon") and then click **Rename query**.

3. Enter the Dataprime query.

    For more information, see [Querying data by using DataPrime](/docs/cloud-logs?topic=cloud-logs-query-data-dataprime).



## Step 3: Configure the widget
{: #widget_dataprime_3}

As you create your query, you can select from the visualization in the right-hand column. If your query results do not support a visualization, that visualization can't be selected. You can hover over visualizations that you can't select to get suggestions on how to change your query so the visualization can be used.
{: note}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. Choose a visualization. Then, configure the widget for that visualization. For information on visualization customization, see the information for each visualization type:

   * [Data table](/docs/cloud-logs?topic=cloud-logs-widget_datatable)

   * [Gauge](/docs/cloud-logs?topic=cloud-logs-widget_gauge)

   * [Horizontal bar chart](/docs/cloud-logs?topic=cloud-logs-widget_horizontalbar).

   * [Line chart](/docs/cloud-logs?topic=cloud-logs-widget_linechart).

   * [Pie chart](/docs/cloud-logs?topic=cloud-logs-widget_piechart)

   * [Vertical bar chart](/docs/cloud-logs?topic=cloud-logs-widget_verticalbar)

   * Polystat


## Step 4: Save the widget
{: #widget_dataprime_5}

Complete the following steps:

1. [Optional] Set the widget's dashboard time if you want to use a time range that is different from the Dashboard selected one.

2. Click **Save** to save your widget.

3. [Optional] Add a custom action. For more information, see [Using actions to integrate with third-party services](/docs/cloud-logs?topic=cloud-logs-actions).
