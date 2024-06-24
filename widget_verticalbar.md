---

copyright:
  years:  2022, 2024
lastupdated: "2023-05-15"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} vertical bar widget
{: #widget_verticalbar}

You can create a vertical bar chart that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

Vertical bar charts sort your data alphabetically by default by column namet. In [horizontal bar charts](/docs/cloud-logs?topic=cloud-logs-widget_horizontalbar), data is usually sorted by value.

## Creating a vertical bar chart
{: #create_verticalbar}

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Vertical Bar Chart** widget from your side bar.

2. Set the definitions for your Bar Chart in the sidebar.

   **Name & Description**: Enter a name and description.

   **Source**. Select a data type.

   If the data type chosen is metrics, specify the metric or desired PromQL in the **Query** field.

   When creating a bar chart with metrics as the data type, the categories specified in the PromQL q uery appear in the **Group By** field automatically. You can reorder categories in the **Group By** field by dragging and dropping. Drag and drop categories from the **Category** field into the **Stacking** field, to stack by a particular category.

   **Add Filter**: (Optional) Add a filter to your bar chart.

   Unlike the dashboard filter in sidebar which affects the entire dashboard, this filter only affects the widget.

   The widget and dashboard filters operate in parallel to one another and intersect. If they negate one another, dashboard filters override widget filters.

   **Group By**: Select the fields to group by from the dropdown menu.

   **X AXIS.** Select whether the X axis of the chart should be by value or by time.

   If you select **Value**, enter the value to show (for example, Country).

   If you select **Time**, select Auto or Manual time buckets, and if Manual, the length of the time bucket.

   **Aggregation**: Aggregate by **Count**, **Count Distinct**, **Sum**, **Min**, **Max**, or **Average**.

   In Bar charts, changing the aggregation type will change the type of data you see. For example, aggregating by count, might show you the number of people in a country. When aggregating by Average, you would need to provide additional parameters, such as height, which will give you a bar chart displaying the average height by country.

   **Stack By**: (Optional) Select a field to stack the chart. This shows you a second layer of data on the chart.

   **Advanced**: Select from the following advanced options.

   **Legend Colors By:** Select whether you want your legend colors to be by group or by stack.

   **Scale**: Select whether you want the scale of the bar chart to be **Logarithmic** or **Linear**. The default setting is linear, however if you have large differences between the different values, it can be helpful to show the logarithmic scale instead. For example, if the majority of your values are under 1k and one value is 10k, using the logarithmic scale will show you an easier to read bar chart than the linear scale.

   **Sort By**: Select whether to sort the chart by column name or by value. By default the vertical bar chart is sorted alphabetically by name.

   **Max Bars Per Graph**: Select the maximum number of bars you want to show per graph.

   **Group Name**: Enter the displayed group name.

   **Unit**: Select the unit type to use in your bar chart.

3. Click **Save** to save your widget.

