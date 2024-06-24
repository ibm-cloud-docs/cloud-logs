---

copyright:
  years:  2022, 2024
lastupdated: "2024-05-15"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} data table widget
{: #widget_datatable}

You can create a data table widget that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

The Data Table widget has two possible views. The **Events** view is supported for logs and spans, and the **Aggregated** view is supported for logs, spans and metrics.

In the **Aggregated** view, for metrics, the data is auto-generated from within the metric, and for logs and spans, you need to select a column by which you want to aggregate the data, then select which columns you want to see.

## Creating a data table
{: #create_datatable}

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Data Table** widget from your side bar.

2. Set the definitions for your data table in the sidebar.

    **Name & Description**: Create a name and description for your data table.

    **Source**: Select a data source. Metrics, logs and spans are supported as the data source for the data table widget. The metrics data source provides you with the ability to easily investigate any metric even with a high volume of data. It enables you to view all the permutations of each label for a given query. Each permutation gives you the values for the selected timespan including Last, Min, Max, Avg and Sum. It includes a view that lets you see the values at any given time in the selected timespan.

    If the **Source** chosen is metrics, specify the metric or desired PromQL in the **Query** field.

    **Table Type**: When using logs or spans as the data source, you can choose between the Events view and the Aggregated view. Metrics are automatically generated in aggregated view.

    **Event tables**: Display a table with a list of logs or spans ordered by time by default. You can change this to be sorted by other columns later) with additional metadata and labels relevant to those events, similar to the view you see in the Explore screen.

    **Aggregation tables**: creates a table of values, grouped by a field or fields you specify. Each column represents a different value depending on the chosen group. Values could be a simple count or an average of the values for the specific field, for each of the defined group-by values.

    You can add and edit columns and filters for the aggregation table using the side bar.

    Traces are limited to a single aggregation column per table widget.
    {: note}

    **Columns**: Manage columns by selecting one or more relevant fields.

    **Advanced**: Select the number of results to be displayed per page.

4. In the Query bar, add a Lucene or PromQL query to filter specific information.

5. Click **Save** to save your dashboard with the new widget.
