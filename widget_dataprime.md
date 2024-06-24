---

copyright:
  years:  2022, 2024
lastupdated: "2023-05-15"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} DataPrime creator widget
{: #widget_dataprime}

You can create the optimum visualization for your data based on your DataPrime query that can then be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

The [DataPrime language](/docs/cloud-logs?topic=cloud-logs-dataprime-ref) can be used to query your data and transform it through operations tailored to your specific needs. This includes calculation, extraction, and aggregation.

In a custom dashboard, the DataPrime creator widget lets you harness the capabilities of DataPrime queries. As your query evolves, this feature automatically lets you select optimal visualizations to display your data and suggests modifying your query for additional visualizations.


## Creating a DataPrime creator widget
{: #create_dataprime_creator}

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **DataPrime creator** widget from your side bar.

   A data table will be displayed as the top panel and the DataPrime query in the bottom panel.

2. In the bottom panel construct your DataPrime query. 

   As you create your query you can select from the visualization in the right-hand column. If your query results do not support a visualization, that visualization can't be selected. You can hover over visualizations that you can't select to get suggestions on how to change your query so the visuzlzation can be used.

2. Set the definitions for your widget in the sidebar.

    **Name** and **Description**: Create a name and description for your widget.

    **Load Data From**: Select the data source. You can select data from the {{site.data.keyword.frequent-search}} or {{site.data.keyword.monitoring}} {{site.data.keyword.tco-optimizer}} pipelines.

    **Add Filter**: (Optional) Add a filter to your bar chart.

    Unlike the dashboard filter in sidebar which affects the entire dashboard, this filter only affects the widget.

    The widget and dashboard filters operate in parallel to one another and intersect. If they negate one another, dashboard filters override widget filters.

    **Columns**: Manage columns by selecting one or more relevant fields.

    **Advanced**: Select the number of results to be displayed per page.

4. In the sidebar you will also be able to customize the visualization depending on the visualization selected. For information on visualization customization, see the information for each visualization type.

   * [Data table](/docs/cloud-logs?topic=cloud-logs-widget_datatable)
   * [Gauge](/docs/cloud-logs?topic=cloud-logs-widget_gauge)
   * [Horizontal bar chart](/docs/cloud-logs?topic=cloud-logs-widget_horizontalbar).
   * [Line chart](/docs/cloud-logs?topic=cloud-logs-widget_linechart).
   * [Pie chart](/docs/cloud-logs?topic=cloud-logs-widget_piechart)
   * [Vertical bar chart](/docs/cloud-logs?topic=cloud-logs-widget_verticalbar)

5. Click **Save** to save your dashboard with the new widget.


