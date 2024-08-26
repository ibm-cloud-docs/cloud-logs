---

copyright:
  years:  2024
lastupdated: "2024-08-26"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Learning about {{site.data.keyword.logs_full_notm}} dashboards
{: #about_dashboards}

In {{site.data.keyword.logs_full}}, you can use dashboards to monitor related data through different types of data visualizations, also known as widgets.
{: shortdesc}


With {{site.data.keyword.logs_full}} you can create unlimited, personalized **custom dashboards** and group them in folders.

## Home dashboard
{: #about_dashboard_home}

The **Home dashboard** is a prefedined dashboard that includes the following information in the timeframe selected for the dashboard.
- The trend of high severity logs and their percentage of total logs.
- The trend of metric ingestion.
- List of triggered alerts grouped by severity.
- List of anomalies grouped by type.
- The applications and subsystems that generated the highest volume of errors and their template distributions.
- The logs volumes grouped by severity.
- The top 3 errors that occurred at above their usual occurrence rates or occurred for the first time within the last 7 days.
- Information on the application and subsystem combinations with the highest error rates.

By default the timeframe is set to 24 hours, and the information included covers logs and metrics.

When you launch the UI, the home dashboard opens.


## Custom dashboards
{: #about_dashboard_custom}

Dashboards can be created to meet your specific observability needs by adding visualization widgets.

Custom dashboard are comprised of widgets. You can add one or more widgets to a dashboard. Each widget supports different data types: logs or metrics. The timeframe configured for the dashboard is applied to all the widgets.

You can then query your data by using the **Filter** and **Variable** capabilities.

Dashboards can include one or more of the following visualizations:

* [Data table](#about_datatable)
* [Line chart](#about_linechart)
* [Gauge](#about_gauge)
* [Pie chart](#about_piechart)
* [Vertical bar chart](#about_verticalbar)
* [Horizontal bar chart](#about_horizontalbar)
* [Markdown](#about_markdown)
* [DataPrime creator](#about_dataprime)


## Widgets
{: #about_dashboard_widgets}

Custom dashboard are comprised of widgets.
- You can add one or more widgets to a dashboard.
- Each widget supports different data types: logs or metrics.
- The timeframe configured for the dashboard is applied to all the widgets that are included in that dashboard.

### Data table
{: #about_datatable}

A data table represents the selected data in tabular format. For more information, see [Data table](/docs/cloud-logs?topic=cloud-logs-widget_datatable).

### Line chart
{: #about_linechart}

A line chart represents the selected data as a line graph over time. For more information, see [Line chart](/docs/cloud-logs?topic=cloud-logs-widget_linechart).

### Gauge
{: #about_gauge}

A gauge represents the current value of a single data point. For more information, see [Gauge](/docs/cloud-logs?topic=cloud-logs-widget_gauge).

### Pie chart
{: #about_piechart}

A pie chart represents different values for a single data source type allowing you to see the proportional relationships to those values. For more information, see [Pie chart](/docs/cloud-logs?topic=cloud-logs-widget_piechart).

### Vertical bar chart
{: #about_verticalbar}

A vertical bar chart represents different values from one or more data sources as vertical bars. This visualization allows you to see relationships between values for the same data types originating from different data sources. By default data is presented alphabetically by data column name. For more information, see [Vertical bar chart](/docs/cloud-logs?topic=cloud-logs-widget_verticalbar).

### Horizontal bar chart
{: #about_horizontalbar}

Horizontal bar charts represent values from one or more data sources as horizontal bars.  By default the data is presented in decending order of the value. For more information, see [Horizontal bar chart](/docs/cloud-logs?topic=cloud-logs-widget_horizontalbar).


### Markdown
{: #about_markdown}

Markdown widgets can be used to add tables, lists, reference guides, links, code snippets, images, and more to customize, contextualize, and optimize your dashboards. For more information, see [Markdown](/docs/cloud-logs?topic=cloud-logs-widget_markdown).

### DataPrime creator
{: #about_dataprime}

The DataPrime creator widget lets you harness the capabilities of DataPrime queries. As your query evolves, this feature automatically lets you select optimal visualizations to display your data and suggests modifying your query for additional visualizations. For more information, see [DataPrime creator](/docs/cloud-logs?topic=cloud-logs-widget_dataprime)
