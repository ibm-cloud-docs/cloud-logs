---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} heatmap
{: #widget_heatmap}

You can create a heatmap that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

Use the heatmap widget to visualize distribution or data intensity across two dimensions and quickly identify high-activity areas or trends, quickly catch hotspots, trends, and anomalies over time or by category, or drill from events directly into logs, or metrics for deeper analysis.
{: note}


## Before you begin
{: #widget_heatmap_prereqs}

A heatmap displays the intensity of data values using color. Each cell represents the aggregated value of data at the intersection of 2 dimensions such as time - service, endpoint - latency, or region - status code. This makes it easy to identify spikes and patterns that might be hard to see in a line or bar chart.

Consider the following information when configuring the Heatmap:
- Keep under 2,000 data rows the total number of X×Y combinations that are returned by the query.

- If your query returns more than 2000 records, increase the time range or reduce the number of *Group By* fields.

- Use no more than 5 grouping fields per widget.  Additional fields might affect readability and performance.

- Avoid grouping by high-cardinality labels like user_id.

- Limit grouping fields to avoid overcrowded visualization results.

## Step 1: Enter name and description
{: #widget_heatmap_1}

Complete the following steps:

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Heatmap** widget from your side bar.

2. Replace *New heatmap* with the **Name** for the widget.

3. Enter a description.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Add description**.


## Step 2: Configure the query to define the data set
{: #widget_heatmap_2}

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

5. Add a function to group and aggregate your data for the heatmap.

    Select an aggregation function such as `Count`, `Sum`, or `Average` to calculate the value that is represented by color intensity.

    Select *Group by* fields. These fields are used for heatmap axes. These fields must be of type string, timestamp, or severity. If a field is numeric, such as status_code, you can cast it to a string in a DataPrime query before grouping. For example, you can use in your query: `status_code:string`

## Step 3: Configure the widget
{: #widget_heatmap_3}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. In the *Visual Management* section, select up to 5 categories or fields you want to appear on the X and Y axes.

    To control which field appears on the X-axis and which on the Y-axis, drag and drop fields between the `Y-axis` and the `X-axis`.

    When a timestamp field appears on the X-axis, select how time labels are displayed. The default is `Auto`, which adjusts the format based on the selected time range. The following formats are available:

    | Format	| Example |
    |---------|---------|
    | Auto  |	Adjusts automatically |
    | DD/MM	| 25/04 |
    | MM/DD | 04/25 |
    | HH:mm	| 14:30 |
    | DD/MM HH:mm	| 25/04 14:30 |
    | HH:mm DD/MM	| 14:30 25/04 |
    | MM/DD HH:mm	| 04/25 14:30 |
    | HH:mm MM/DD	| 14:30 04/25 |
    {: caption="Formats for timestamp fields" caption-side="top"}

3. Show cell values. Toggle to overlay numeric values inside each cell. This is useful where cells are larger and readable.

4. Select a predefined color palette to represent data intensity. You can reverse the color order (light → dark or dark → light).

    Select the color scheme using the legend configuration. It maps values from light → dark by default. Use Min and Max thresholds to control the color scale range and improve readability for data with wide or uneven distributions.

5. Choose the scale type. Valid values are `Linear` (default) where colors change evenly across values or `Logarithmic` where the color applies globally to the Z-access (color-intensity bar) for datasets with wide value ranges.

6. In the *Tooltip management* section, customize what information appears when you hover over a point or cluster on the map. Add the message and select which labels or attributes to include in the tooltip.

    Add the message or value that is displayed when hovering over a point or cluster. You can reference dynamic fields, such as the aggregated value, using `{{ }}` syntax.

    When a referenced field resolves to multiple distinct values within a cluster, the tooltip displays a generic label such as “multiple” instead of a specific value. This indicates that the cluster contains mixed values and encourages drilling down for more detail.

    Select which labels or attributes to include in the tooltip, such as service, application, or country.

## Step 5: Save the widget
{: #widget_heatmap_5}

Complete the following steps:

1. [Optional] Set the widget's dashboard time if you want to use a time range that is different from the Dashboard selected one.

2. Click **Save** to save your widget.

3. [Optional] Add a custom action. For more information, see [Using actions to integrate with third-party services](/docs/cloud-logs?topic=cloud-logs-actions).


## Actions on a map
{: #widget_heatmap_next}

Use quick actions to investigate data directly from the hetamap.

When you select a point or cluster, a context menu provides the following actions:

- `Open Explore`: Opens the logs in the Explore view, pre-filtered using the selected location and cluster context.

- `Filter in`: Adds the selected location and value context to the dashboard query.

- `Filter out`: Excludes the selected location and value context from the dashboard query.

- `Copy name`: Copies the location label or key=value pair associated with the selected point or cluster.
