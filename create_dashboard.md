---

copyright:
  years:  2024
lastupdated: "2024-06-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} custom dashboard
{: #create_dashboards}

You can create custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

## Dashboard widgets
{: #dashboard_widgets}

Custom dashboard are comprosed of widgets. You can create the widgets you want to use in the dashboard.

* [Data table](/docs/cloud-logs?topic=cloud-logs-widget_datatable)
* [Gauge](/docs/cloud-logs?topic=cloud-logs-widget_gauge)
* [Horizontal bar chart](/docs/cloud-logs?topic=cloud-logs-widget_horizontalbar).
* [Line chart](/docs/cloud-logs?topic=cloud-logs-widget_linechart).
* [Pie chart](/docs/cloud-logs?topic=cloud-logs-widget_piechart)
* [Vertical bar chart](/docs/cloud-logs?topic=cloud-logs-widget_verticalbar)
* [Markdown](/docs/cloud-logs?topic=cloud-logs-widget_markdown)
* [DataPrime creator](/docs/cloud-logs?topic=cloud-logs-widget_dataprime)

## Creating a custom dashboard
{: #custom_dashboard}

Do the following to create a custom dashboard.

1. Click the **Dashboard** icon ![Dashboards icon](/icons/dashboards.svg "Dashboards") > **Custom dashboards**.

2. Create a new dashboard by clicking **New** > **Create New Dashboard**.

3. Drag a widget into your new dashboard.

4. Hover over **Save**, then click **Save As Name**.

5. Enter a name for your new dashboard and click **Save**.

6. In the dashboards panel, hover over your new dashboard and click the three dots. Click what you would like to do with your dashboard: **Favorite**, **Set As Default**, **Rename**, **Delete**, **Save As**, **Export**, or **Copy URL**.

    **Favorite** and **Set As Default** settings are unique for each user. All other settings apply across all team members.
    {: note}

## Creating sections
{: #create_sections}

Widgets can be organized into sections. Sections within a dashboard can be collapsed, expanded, and reordered.

When you save your dashboard, the dashboard is saved with the sections collapsed or expanded as you last displayed them. Widgets in expanded sections are loaded first when the dashboard is displayed.
{: note}

1. Click the **Dashboard** icon ![Dashboards icon](/icons/dashboards.svg "Dashboards") > **Custom dashboards**.

2. In the side bar, view all available dashboards.

3. Click the dashboard you want to view or modify as desired.

4. Drag and drop **Section** to create a section in your dashboard.

5. Name your section by clicking on **New Section** and typing a section name.

6. Drag and drop widgets into the section.

7. Repeat the steps to create new sections and widgets.

5. Once you have made changes, click **Save** or **Save as**. This saves the entire dashboard. Click **Revert** to revert your changes and view the previously saved dashboard.

6. In the dashboards panel, hover over your new dashboard and click the three dots. Click what you would like to do with your dashboard: **Favorite**, **Set As Default**, **Rename**, **Delete**, **Save As**, **Export**, or **Copy URL**.

    **Favorite** and **Set As Default** settings are unique for each user. All other settings apply across all team members.
    {: note}

## Specifying the dashboard timeframe
{: #dashboard_timeframe}

By default, custom dashboards show data from the last 15 minutes. This can be modified using the timeframe dropdown in the dashboard.

You can choose between different timeframes either by selecting one of the quick timeframes, or by using the **Custom** tab and selecting two dates between which you want to show data.

{{site.data.keyword.logs_full}} supports selecting a timeframe of up to 90 days for your custom dashboards. This enables you to view metric widgets with long retention periods easily within your custom dashboards.
{: tip}

Timeframe limitations apply depending on the data source and the data origin. When selecting more than a 7-day time period, the results will appear based on the specific settings of each data source, similar to the Explore screen time limitation.

For example, if your logs in the Explore logs screen are limited by the up to 8 days timeframe, this will also be the case for the custom dashboard. Log data will appear for only the last eight days, as opposed to metrics, which can show up to 90 days of data in the same dashboard.

The query range and retention period are each marked with an annotation line. Hovering over the line shows an explanation.

If the retention period is, for example, 21 days, the user will be able to see that limit on the time series widget, and selecting an older 7-day time query within those 21 days will still return results.


## Modifying a custom dashboard
{: #modify_dashboard}

Widgets are always in edit mode when displayed in a dashboard and can be edited at any time.
{: note}

1. Click the **Dashboard** icon ![Dashboards icon](/icons/dashboards.svg "Dashboards") > **Custom dashboards**.

2. In the side bar, view all available dashboards.

3. Click on the dashboard you want to view or modify as desired.

    When you hover over **Save** on the dropdown menu, you will have the option to select either **Save** or **Save As**. **Save** makes changes to your current dashboard. **Save As** creates a new copy of your dashboard and saves the changes, while maintaining the original as is.

    If you choose to **Save As**, a popup will appear requiring that you name your new dashboard.

4. Modify dashboard widgets as desired.

    To expand a specific widget within a dashboard, click on the Expand icon in the corner of the widget. This temporarily expands the widget to fill the entire dashboard.

    Three dots can be found in the corner of every widget. Click the three dots and select from the menu options: **Edit**, **Delete**, **Clone**, **Create Alert** and **Create Metric**. For line charts, you also have the option to **Hide Legend**.

    Right clicking a value in the legend of a Line chart opens a context menu with the following options:

    **Exclude**: Exclude this value from the current filter.

    **Include**: Include this value in the filter.

    **Copy Name**: Lets you copy the name of the time series for use in queries or searches.

5. Once you have made changes to a widget, click **Save** or **Save as**. This saves the entire dashboard. Click **Revert** to revert your changes and view the previously saved dashboard.

6. In the dashboards panel, hover over your new dashboard and click the three dots. Click what you would like to do with your dashboard: **Favorite**, **Set As Default**, **Rename**, **Delete**, **Save As**, **Export**, or **Copy URL**.

    **Favorite** and **Set As Default** settings are unique for each user. All other settings apply across all team members.
    {: note}


## Creating variables
{: #create_variable}

From your dashboard you can create variables that can be used in the widgets query language.

1. Click the Add Variable icon **[x]** in the corner of your dashboard.

2. Define your variable by defining **Variable type**, **Field**, **Variable name**, and **Display Name**.

3. Click **Save**.

4. View the variables for each **Field** in the corner of your screen.

You can now use the variable name in the widget query language.

Input the value in the Lucene or DataPrime query. When the value is changed, all widgets are affected.
{: note}


## Creating filters
{: #create_filter}

Application and subsystem filters are created by default. You have the option of creating additional filters.

When a filter is enabled, only log-based widgets are filtered.

Disable a filter by clicking on the toggle next to the filter name.

1. Click the **Manage Filters** ![Manage Filters icon](/icons/Filter.svg "Manage Filters") in the sidebar.

2. Click **+ New Filter**.

3. Define the parameters of your Filter: **Source**, **Field**, and **Operator**.

4. Click **SAVE**.


## Notes for custom dashboards use
{: #custom_dashboard_notes}

* Users will have access to all dashboards. Those with editing permissions can edit all dashboards.

* Log filters are applied to log-based widgets.

* Variables defined on a dashboard are accessible from all widgets.

* When editing a widget, the widget you are currently editing is highlighted and all other widgets are faded.

For more information about the different widget types and explanations of their definitions, see the following:

* [Data table](/docs/cloud-logs?topic=cloud-logs-widget_datatable)
* [Gauge](/docs/cloud-logs?topic=cloud-logs-widget_gauge)
* [Horizontal bar chart](/docs/cloud-logs?topic=cloud-logs-widget_horizontalbar).
* [Line chart](/docs/cloud-logs?topic=cloud-logs-widget_linechart).
* [Pie chart](/docs/cloud-logs?topic=cloud-logs-widget_piechart)
* [Vertical bar chart](/docs/cloud-logs?topic=cloud-logs-widget_verticalbar)
* [Markdown](/docs/cloud-logs?topic=cloud-logs-widget_markdown)
* [DataPrime creator](/docs/cloud-logs?topic=cloud-logs-widget_dataprime)
