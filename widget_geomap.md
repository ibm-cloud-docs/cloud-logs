---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating an {{site.data.keyword.logs_full_notm}} Geomap widget
{: #widget_geo_map}

You can create a geo map that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

Use the Geomap widget to visualize geographically the data at different levels of detail to identify regional patterns, hotspots, and anomalies.
{: note}



## Before you begin
{: #widget_geo_map_prereqs}

To configure the Geomap widget, you need location information in your data. The location can be provided as geographic coordinates or as a supported location identifier.

You can pass location information by using any of the following options:

- Option 1: Include latitude and longitude fields in each record

    You can use latitude and longitude fields directly to configure the Geomap widget.

    The fields must contain valid numeric coordinate values.

- Option 2: Include a field that contains an IP address value and use the Geo enrichment feature

    You must configure geo enrichment on the relevant IP field. Geo enrichment derives numeric latitude and longitude values from IP addresses and provides a consistent source of location data for Geomap. For more information, see [Configuring geo enrichments](/docs/cloud-logs?topic=cloud-logs-enrich-geo).


To configure the widget, the latitude and longitude fields must comply with any of the supported formats:

| Format	                      | Example	              | Supported |
|-------------------------------|-----------------------|---------------|
| Decimal degrees (numeric)	    | 32.0853, 34.7818	    | [Yes]{: tag-green} |
| Signed numeric values         | -33.8688, 151.2093	  | [Yes]{: tag-green} |
| Numeric values as strings	    | "34.7818"	            | [No]{: tag-red} |
| Degrees–minutes–seconds (DMS)	| 32°05′07″N	          | [No]{: tag-red} |
{: caption="Formats for latitude and longitude values" caption-side="top"}


The data that is visualized through a Geomap widget is grouped by latitude and longitude coordinates into clusters. Think of a cluster as a virtual bucket of data that have in common latitude and longitude.

The query that you configure in a Geomap widget evaluates only the most recent 2,000 log records in the selected time range. If some of those log records do not contain geographic fields, they are excluded from the map, which can result in an empty or sparsely populated view. To ensure the evaluated records contain geographic data, you must explicitly filter for non-null location fields in the widget's query builder.
{: important}

For example, you can use a dataprime query that filters out log records that do not include geographic fields:

```text
source logs
| filter $d.latitude != null
| filter $d.longitude != null
xxxxx
```
{: codeblock}


Consider the following information when interacting with the map:
- Zooming in and out changes the level of geographic aggregation, allowing you to move from high-level regional patterns to more granular locations.
- Hovering over points or clusters displays a tooltip with contextual information based on the current configuration.
- Clicking a cluster drills down into smaller geographic groupings, making it easier to investigate areas with mixed or aggregated values.

## Step 1: Enter name and description
{: #widget_geo_map_1}

Complete the following steps:

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Geomap** widget from your side bar.

2. Replace *New Geomap* with the **Name** for the widget.

3. Enter a description.

    Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Add description**.


## Step 2: Configure the query to define the data set
{: #widget_geo_map_2}

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

5. Add a function to group and aggregate your data for the Geomap.

## Step 3: Configure the widget
{: #widget_geo_map_3}

Complete the following steps:

1. Click **Action icon** ![Action icon](/images/action-three-dots-horizontal.png "Action icon"). Then, select **Edit mode**.

2. In the *Location management > Coordinates* section, select the fields to use that contain the latitude and longitude information.

    Fields containing latitude and longitude values **cannot** be of type string.

    You can only configure 1 field to provide the latitude information, and 1 field to provide the longitude information per widget.

    If your geographical data is available through different fields in different records, use parsing rules to consolidate the data into a single one.

    The Geomap widget does not automatically detect or infer location fields. You must explicitly select the fields used for location resolution.

3. In the *Location management > Cluster value calculation*, select how values are calculated for each geographic cluster. If you select a numeric calculation, `Sum`, `Average`, `Minimum` or `Maximum`, you must select a numeric field in *By field* that will be used to calculate the data that goes into a cluster group.

    Valid values are: `Count`, `Sum`, `Average`, `Minimum` or `Maximum`.

    Values are recalculated for a cluster dynamically as you zoom in and out of the map.

    Zooming in increases granularity, revealing smaller clusters or individual points.

    Zooming out aggregates nearby clusters into higher-level groupings.

    Volume-based calculations, using `Count`or `Sum`, accumulate values as clusters merge.

    Value-based calculations, using `Average`, `Minimum` or `Maximum`, are recalculated from the underlying data.

    Numeric aggregation calculations, using `Sum`, `Average`, `Minimum` or `Maximum`, require a numeric field to be present in the query results.

    Results without a valid numeric value are excluded from aggregation.

    If a numeric value is stored as a string in your data, you may need to cast it to a numeric type in the query or parse it at ingestion before using it with numeric aggregations. This ensures the value can be included in `Sum`, `Average`, `Minimum` or `Maximum` calculations.

    Query results that cannot be resolved to a geographic location are excluded.

    `Count` counts the number of events within each geographic cluster. You can use `count` to identify hotspots, traffic concentration, or regions with elevated error volumes. When zooming out, counts are added together from smaller clusters.

    `Sum` adds the values of a numeric field for all events in each cluster. You can use it for cumulative metrics such as total bytes, total requests, or total cost. When zooming out, sums are added together across clusters.

    `Average` calculates the average value of a numeric field per cluster. You can use it for performance metrics such as latency or duration. When zooming out, averages are recalculated from underlying clusters, not summed.

    `Minimum` or `Maximum` displays the lowest or highest value observed within each cluster. You can use these options to identify the best-case and the worst-case values, outliers, or spikes. When zooming out, the minimum or maximum is recalculated across merged clusters.

4. In the *Tooltip management* section, customize what information appears when you hover over a point or cluster on the map. Add the message and select which labels or attributes to include in the tooltip.

    Add the message or value that is displayed when hovering over a point or cluster. You can reference dynamic fields, such as the aggregated value, using `{{ }}` syntax.

    When a referenced field resolves to multiple distinct values within a cluster, the tooltip displays a generic label such as “multiple” instead of a specific value. This indicates that the cluster contains mixed values and encourages drilling down for more detail.

    Select which labels or attributes to include in the tooltip, such as service, application, or country.

5. In the *Visual management* section, define how values are represented on the map.

    Valid options are `Size` and `Color range`.

    Choose **Size** for volume-based analysis where volume and concentration are the primary signals.

    Choose **Color range** for performance-focused analysis. You can select a color palette and control how values map to colors. You can define thresholds to control how cluster values translate into colors. Thresholds are evaluated against the selected cluster value calculation and update dynamically as cluster values change.


## Step 4: Save the widget
{: #widget_geo_map_4}

Complete the following steps:

1. [Optional] Set the widget's dashboard time if you want to use a time range that is different from the Dashboard selected one.

2. Click **Save** to save your widget.

3. [Optional] Add a custom action. For more information, see [Using actions to integrate with third-party services](/docs/cloud-logs?topic=cloud-logs-actions).


## Actions on a map
{: #widget_geo_map_next}

Use quick actions to investigate data directly from the map.

When you select a point or cluster, a context menu provides the following actions:

- `Open Explore`: Opens the logs in the Explore view, pre-filtered using the selected location and cluster context.

- `Filter in`: Adds the selected location and value context to the dashboard query.

- `Filter out`: Excludes the selected location and value context from the dashboard query.

- `Copy name`: Copies the location label or key=value pair associated with the selected point or cluster.
