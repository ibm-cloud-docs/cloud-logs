---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-22"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} vertical bar widget
{: #widget_verticalbar}

You can create a vertical bar chart that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

Use a vertical bar charts to sort your data alphabetically by default by column name. In [horizontal bar charts](/docs/cloud-logs?topic=cloud-logs-widget_horizontalbar), data is usually sorted by value.



## Step 1: Enter name and description
{: #widget_verticalbar_1}

Complete the following steps:

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Vertical Bar Chart** widget from your side bar.

2. Replace *New vertical bar chart* with the **Name** for the widget.

3. Enter a description.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Add description**.

4. Define where legend values are displayed. Valid values are: `Side`, `Bottom`, `Auto`, and `Hide`.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Legend Settings**.


## Step 2: Configure the query to define the data set
{: #widget_verticalbar_2}

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

    When creating a bar chart with metrics as the data type, the categories specified in the PromQL query appear in the Group By field automatically. You can reorder categories in the Group By field by dragging and dropping. Drag and drop categories from the Category field into the Stacking field, to stack by a particular category.

4. [Optional] Add one or more filters specific to the widget to narrow down the data that is displayed.

    Select a label and its corresponding value.

    Filters are applied at the widget level and work alongside dashboard filters. If there is a conflict, the dashboard filters take precedence over widget filters.

5. Add a function.

    For a query where the data type is `Logs`, you can show an aggregated value using one of the following functions:

    | Aggregation      | Description |
    |------------------|-------------|
    | Count	           | The total number of logs within the selected time range. |
    | Count Distinct   | The number of unique logs within the selected time range. |
    | Sum	             | The sum of all logs within the selected time range. |
    | Min	             | The smallest value among the logs within the selected time range. |
    | Max	             | The largest value among the logs within the selected time range. |
    | Average	         | The average value of all logs within the selected time range. |
    | Percentile XX	   | Represents the value below which XX% of the logs fall. For example, Percentile 95 is the value below which 95% of logs fall. |
    {: caption="Aggregation option when building a query when the data type is Logs" caption-side="top"}

    For a query where the data type is `Metrics`, you can show a calculated value using one of the following functions:

    | Calculation      | Description |
    |------------------|-------------|
    | Instant	         | The value at the current point in time. |
    | Last	           | The most recent value within the selected time range. |
    | Min	             | The smallest value within the selected time range. |
    | Max	             | The largest value within the selected time range. |
    | Avg	             | The average value of all data points within the selected time range. |
    | Sum	             | The total sum of all data points within the selected time range. |
    | None	           | No calculation is applied. Raw data is used. |
    {: caption="Calculations option when building a query when the data type is Metrics" caption-side="top"}



## Step 3: Configure the widget
{: #widget_verticalbar_3}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. Choose a *Legend Management* option. Valid values are: `Group` and `Stack`.

    **Group** organizes the legend based on different data entities, such as servers or applications, displaying each as a separate entry.

    **Stack** displays how multiple data entries are grouped and layered together on the same horizontal bar. The data sets of the same stack are grouped into a single horizontal bar chart divided into segments. This shows you a second layer of data on the chart.

    **Legend Colour Scheme** : Select whether you want your legend colours to be by group, stack, or aggregation. By default, the horizontal bar chart is by aggregation, which means a single colour will be shown for all bars.

3. In the *Visual management* section, choose how you want to visualize tha data.

    The max bar by graph displays the maximum number of individual bars in a single chart view according to your query.

    The max slices per bar displays the maximum number of segments within a single bar.

    Enable the *max bar by graph*, the *max slices per bar*, or both to display a single value within a specified range.

4. Configure the *Scale* section.

    A scale refers to how values are displayed along the x-axis and y-axis. You may choose between linear or logarithmic as values.

    Choose the *Scale type*. Valid options are: `Linear` that defines how values increases proportionally and `Logarithmic` wherein value is defined by logarithms instead of equal linear intervals.

    You can change the color of a threshold value.

    By default, setting is linear. If however you have large differences between the different values, it can be helful to show the logarithmic scale instead. For example, if the majority of your values are under 1k and one value is 10k, using the logarithmic scale will show you an easier to read bar chart than linear scale.



## Step 4: Save the widget
{: #widget_verticalbar_4}

Complete the following steps:

1. [Optional] Set the widget's dashboard time if you want to use a time range that is different from the Dashboard selected one.

2. Click **Save** to save your widget.

3. [Optional] Share a direct link to the widget. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Share Widget URL**, and copy the URL.

    Anyone with access to the dashboard can open the shared link to view the widget in context.

    Shared widget URLs always reflect the dashboard’s last saved version. If you’ve made changes to the widget or layout, save your dashboard before sharing.{: attention}

4. [Optional] Add a custom action. For more information, see [Using actions to integrate with third-party services](/docs/cloud-logs?topic=cloud-logs-actions).
