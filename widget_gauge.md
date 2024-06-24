---

copyright:
  years:  2022, 2024
lastupdated: "2024-05-15"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a {{site.data.keyword.logs_full_notm}} gauge widget
{: #widget_gauge}

You can create a gauge widget that can be included in custom {{site.data.keyword.logs_full}} dashboards.
{: shortdesc}

The gauge widget works on a **single** time series.
{: important}

## Creating a gauge
{: #create_gauge}

1. In a [custom dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards), click **Add Widget** ![Add Widget icon](/icons/Plus.svg "Add Widget") and drag and drop the **Gauge** widget from your side bar.

2. Set the definitions for your gauge in the sidebar.

   **Name & Description**: Create a name and description.

   **Source**: Select a data type.

   If the data type chosen is metrics, specify the metric or desired PromQL in the **Query** field.

   **Calculation**: Determines the values for your gauge. Possible parameters are **Instant**, **Last**, **Avg**, **Sum**, **Min** and **Max**.

   Selecting the parameter **Last** will provide the last data point in a time series within the selected time frame, while **Instant** will provide the final value at the end of the time frame. **Avg**, **Sum**, **Min**, and **Max** calculate the value by applying the selected aggregation function to the time series data points within the time frame.

   For example, if the time is 03:25:00, fetching the time series with hour steps returns 00:00:00 - 1, 01:00:00 - 3, 02:00:00 - 15, 03:00:00 - 60, the **Last** value would be 60. However, if we get the value for the exact time of 03:25:00 using **Instant**, the value returned will be taken from the exact time in the timeline, resulting in a value of 120.

   If you choose a data type of logs or spans, you will be directed to select an **Aggregation.**

   **Add Filter:**  (Optional) Add a filter to your gauge.

   Unlike the dashboard filter in the sidebar which affects the entire dashboard, this filter only affects the widget.

   The widget and dashboard filters operate in parallel to one another and intersect. If they negate one another, dashboard filters override widget filters.

   **Visuality**: Indicate how you want the data displayed.

   Select **Unit** to display a % symbol with your results.

    Enable or disable the **Inner arc** and **Outer arc**. The inner arc will show the actual value. The outer arc will show the thresholds. If you choose not to enable either arc, only a number will be displayed in your gauge.

    **Thresholds.**: Choose the base **Thresholds**. That is, when the gauge should appear green and red. Add additional thresholds - yellow and orange - if necessary.

3. Click **Save** to save your widget.



