---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-22"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} polystat widget
{: #widget_polystat}

You can create polystat widget that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}


## Step 1: Enter name and description
{: #widget_polystat_1}

Complete the following steps:

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Polystat** widget from your side bar.

2. Replace *New polystat* with the **Name** for the widget.

3. Enter a description.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Add description**.

4. Define where legend values are displayed. Valid values are: `Side`, `Bottom`, `Auto`, and `Hide`.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Leggend Settings**.



## Step 2: Configure the query to define the data set
{: #widget_polystat_2}

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


4. [Optional] Add one or more filters specific to the widget to narrow down the data that is displayed in your gauge.

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
{: #widget_polystat_3}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. Choose a *Legend Management* option. Valid values are: `Group` and `Threshold`.

    **Group** organizes the legend based on different data entities, such as servers or applications, displaying each as a separate entry.

    **Threshold** categorizes values based on predefined limits such as normal, warning, critical, helping to visualize whether a metric is within an acceptable range or has crossed into a warning state.

3. Configure the *Thresholds* section.

    A threshold is a value you set, that when met or exceeded, changes the visualization's appearance based on the query results. You may choose between percentage or absolute numbers as values.

    Choose the *Threshold type*. Valid options are: `absolute` to define specific numbers as the value and `relative` to define values that are relative to the minimum or maximum value.

    You can change the color of a threshold value.

    You can set the values for a threshold and add labels that describe it.

    You can add additional thresholds.


## Step 4: Save the widget
{: #widget_polystat_4}

Complete the following steps:

1. [Optional] Set the widget's dashboard time if you want to use a time range that is different from the Dashboard selected one.

2. Click **Save** to save your widget.

3. [Optional] Share a direct link to the widget. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Share Widget URL**, and copy the URL.

    Anyone with access to the dashboard can open the shared link to view the widget in context.

    Shared widget URLs always reflect the dashboard’s last saved version. If you’ve made changes to the widget or layout, save your dashboard before sharing.{: attention}

4. [Optional] Add a custom action. For more information, see [Using actions to integrate with third-party services](/docs/cloud-logs?topic=cloud-logs-actions).
