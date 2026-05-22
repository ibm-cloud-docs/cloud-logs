---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-22"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} line chart widget
{: #widget_linechart}

You can create a line chart widget that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

The line chart displays values as a series of data points.


## Step 1: Enter name and description
{: #widget_linechart_1}

Complete the following steps:

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Line Chart** widget from your side bar.

2. Replace *New line chart* with the **Name** for the widget.

3. Enter a description.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Add description**.

4. Define where legend values are displayed. Valid values are: `Side`, `Bottom`, `Auto`, and `Hide`.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Legend Settings**.


## Step 2: Configure the query to define the data set
{: #widget_linechart_2}

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
{: #widget_linechart_3}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. Choose a *Tooltip* option. Valid values are: `Show all series` and `Single View`.

    Select whether to see all time series when hovering over them, or to see only the single time series you hover over.

3. In the *Visual management* section, choose how you want to visualize tha data. Options are **Absolute** and   **Relative**.

    `Absolute` displays specific numbers as the value whereas `Relative` values that are relative to the minimum or maximum value.

4.  In the *Time Bucket* section, choose how you want to group data points. You can decide to group data automatically or choose the exact time interval, manually.

    You can enter a value that should be shown as data points inside each time bucket.

5. In the *Series Management* section, configure the `Scale` option.

    A scale refers to how values are displayed along the x-axis and y-axis.

    Valid options are: `linear` that defines how values increases proportionally and `logarithmic` wherein value is defined by logarithms instead of equal linear intervals.

    By default, setting is linear. If however you have large differences between the different values, it can be helful to show the logarithmic scale instead. For example, if the majority of your values are under 1k and one value is 10k, using the logarithmic scale will show you an easier to read bar chart than linear scale.
   {: note}


## Step 4: Save the widget
{: #widget_linechart_4}

Complete the following steps:

1. [Optional] Set the widget's dashboard time if you want to use a time range that is different from the Dashboard selected one.

2. Click **Save** to save your widget.

3. [Optional] Share a direct link to the widget. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Share Widget URL**, and copy the URL.

    Anyone with access to the dashboard can open the shared link to view the widget in context.

    Shared widget URLs always reflect the dashboard’s last saved version. If you’ve made changes to the widget or layout, save your dashboard before sharing.

4. [Optional] Add a custom action. For more information, see [Using actions to integrate with third-party services](/docs/cloud-logs?topic=cloud-logs-actions).
