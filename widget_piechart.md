---

copyright:
  years:  2022, 2024
lastupdated: "2024-05-15"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} pie chart widget
{: #widget_piechart}

You can create a pie chart widget that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

## Creating a pie chart
{: #create_piechart}

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Pie Chart** widget from your side bar.

2. Set the definitions for your pie chart in the sidebar.

   **Name & Description**: Enter a name and description.

   **Source**: Select a data type.

   If the data type chosen is metrics, specify the metric or desired PromQL in the **Query** field.

   When creating a pie chart with metrics as the data type, the categories specified in the PromQL query appear in the **Group By** field automatically.  You can reorder categories in the **Group By** field by dragging and dropping.

   Drag and drop categories from the **Category** field into the **Stacking** field, to stack by a particular category.

   If the data type chosen is logs or spans, you will need to select an **Aggregation.**

   **Add Filter**: (Optional) Add a filter to your pie chart.

   Unlike the dashboard filter in sidebar which affects the entire dashboard, this filter only affects the widget.

   The widget and dashboard filters operate in parallel to one another and intersect. If they negate one another, dashboard filters override widget filters.

   **Group By**: Select up to two fields from the dropdown menu.

   **Stack By**: (Optional) Select a field to stack the chart. This shows you a second layer of data on the chart.

   **Advanced**: Select the maximum number of slices to show in the chart, select the minimum percentage to display a slice, the units to display, select whether or not to show labels and which labels to show, customize the group name, and select whether or not to show the legend.

3. Click **Save** to save your widget.

