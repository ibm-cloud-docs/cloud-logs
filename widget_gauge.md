---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-18"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} gauge widget
{: #widget_gauge}

You can create a gauge widget that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

Use a gauge widget to display a single value within a specified range, often resembling a speedometer or dial. It is typically used to represent key metrics and performance indicators at a glance.
{: note}

## Step 1: Enter name and description
{: #widget_gauge_1}

Complete the following steps:

1. 1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Gauge** widget from your side bar.

2. Replace *New gauge* with the **Name** for the widget.

3. Enter a description.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Add description**.

4. Define where legend values are displayed. Valid values are: `Side`, `Bottom`, `Auto`, and `Hide`.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Leggend Settings**.



## Step 2: Configure the query to define the data set
{: #widget_gauge_2}

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

## Step 3: Configure the widget
{: #widget_gauge_3}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. Choose a *Legend Management* option. Valid values are: `Group` and `Threshold`.

    **Group** organizes the legend based on different data entities, such as servers or applications, displaying each as a separate entry.

    **Threshold** categorizes values based on predefined limits (e.g., normal, warning, critical), helping to visualize whether a metric is within an acceptable range or has crossed into a warning state.

3. In the *Visual management* section, choose how you want to visualize tha data.

    The inner arc displays the actual value for your query.

    The outer arc displays thresholds that you define.

    Enable the *inner arc*, the *outer arc*, or both to display a single value within a specified range, often resembling a speedometer or dial.

    If the *inner arc* and the *outer arc* are disabled, the numerical result of your query will appear as a **STAT widget** without additional visualizations. In this case, you may determine whether the threshold color will be applied to the value or background.

    Threshold color. Set the color/s for the values and background in your visualization.

**Thresholds.**: Choose the base **Thresholds**. That is, when the gauge should appear green and red. Add additional thresholds - yellow and orange - if necessary.

## Step 4: Save the widget
{: #widget_gauge_5}

Complete the following steps:

1. [Optional] Set the widget's dashboard time if you want to use a time range that is different from the Dashboard selected one.

2. Click **Save** to save your widget.

3. [Optional] Share a direct link to the widget. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Share Widget URL**, and copy the URL.

    Anyone with access to the dashboard can open the shared link to view the widget in context.

    Shared widget URLs always reflect the dashboard’s last saved version. If you’ve made changes to the widget or layout, save your dashboard before sharing.{: attention}

4. [Optional] Add a custom action. For more information, see [Using actions to integrate with third-party services](/docs/cloud-logs?topic=cloud-logs-actions).
