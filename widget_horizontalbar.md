---

copyright:
  years:  2022, 2024
lastupdated: "2024-05-15"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} horizontal bar widget
{: #widget_horizontalbar}

You can create a horizontal bar chart that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

With horizontal bar charts your data is sorted by value, in descending order by default. With [vertical bar charts](/docs/cloud-logs?topic=cloud-logs-widget_verticalbar), data is usually sorted alphabetically by column name.

## Creating a horizontal bar widget
{: #create_horizontal}

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Horizontal Bar Chart** widget from your side bar.

2. Set the definitions for your bar chart in the sidebar.

   **Name & Description**: Enter a name and description.

   **Source**: Select a data source.

   If the **Source** chosen is metrics, specify the metric or desired PromQL in the **Query** field.

   When creating a bar chart with metrics as the data source, the categories specified in the PromQL query appear in the **Group By** field automatically. You can reorder categories in the **Group By** field by dragging and dropping.

   **Add Filter**: (Optional) Add a filter to your bar chart.

   Unlike the dashboard filter in the sidebar which affects the entire dashboard, this filter only affects the widget.

   The widget and dashboard filters operate in parallel to one another and intersect. If they negate one another, dashboard filters override widget filters.

   **Category**: Select the fields to sort your bar chart from the drop-down menu.

   **Aggregation**: Aggregate by **Count**, **Count Distinct**, **Sum**, **Min**, **Max**, or **Average**.

   In Bar charts, changing the aggregation type will change the type of data you see. For example, aggregating by count, might show you the number of people in a country. When aggregating by Average, you would need to provide additional parameters, such as height, which will give you a bar chart displaying the average height by country.

   **Advanced**: You can also specify the following advanced options.

   **Y AXIS View**: Select whether the Y-axis of the chart shows the value or the category.

   **Legend Colors By**: Select whether you want your legend colors to be by aggregation or by category. By default the horizontal bar chart is by aggregation, which means a single color will be shown for all bars.

    **Scale**: Select whether you want the scale of the bar chart to be **Logarithmic** or **Linear**. The default is linear, however if you have large differences between the different values, it can be helpful to show the logarithmic scale instead. For example, if the majority of your values are under 1k and one value is 10k, using the logarithmic scale will show you an easier to read bar chart than the linear scale.

    **Sort By**: Select whether to sort the chart by column name or by value. By default the horizontal bar chart is sorted by value.

    **Max Bars Per Graph**: Select the maximum number of bars you want to show per graph.

    **Group Name** (Optional) Customize the displayed group name.

    **Unit**: (Optional) Select the units used to display in the bar chart.

3. Click **Save** to save your widget.

