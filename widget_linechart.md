---

copyright:
  years:  2022, 2024
lastupdated: "2024-05-15"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} line chart widget
{: #widget_linechart}

You can create a line chart widget that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

## Create a Line Chart
{: #create_linechart}

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Line Chart** widget from your side bar.

2. Set the definitions for your line chart in the sidebar.

   **Name & Description**: Enter a name and description for your line chart.

   **Source**: Select a data type.

   If the data type chosen is metrics, specify the metric or desired PromQL in the **Query** field.
    
   If the data type chosen is logs or spans, you will need to configure the following fields:

   - **Aggregation**: Aggregate by Count, Count Distinct, Sum, Min, Max, or Average.
        
   - **Group By**: Select any field from the dropdown menu

   **Add Filter**: (Optional) Add a widget filter.

   Unlike the dashboard filter in the sidebar which affects the entire dashboard, this filter only affects the widget.

   The widget and dashboard filters operate in parallel to one another and intersect. If they negate one another, dashboard filters override widget filters.

   **Tooltip**: Select whether to see all time series when hovering over them, or to see only the single time series you hover over.

   **Advanced**: Create a series name and customize values to be displayed in your legend: Min, Max, Sum, Avg, Last. You have the option to limit the series shown.

3. In the Query bar, add a Lucene or PromQL query to query specific information.

4. Click **Save** to save your widget.

