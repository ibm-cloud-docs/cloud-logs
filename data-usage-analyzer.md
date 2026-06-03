---

copyright:
  years:  2024, 2026
lastupdated: "2026-06-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Analyzing user data sent
{: #data-usage-analyzer}

In {{site.data.keyword.logs_full_notm}}, you can gain insights into data ingestion volumes by priority in the **Data usage > User Data Sent** tab.
{: shortdesc}

In the *User data sent* tab, you can:
- Identify high-volume logs and metrics
- Understand data ingestion patterns



## Opening the User data sent tab
{: #data-usage-analyzer-launch}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Usage icon](/icons/usage.svg "Usage") > **Data Usage**.

    The *Data Usage* page opens.

    ![Data Usage](/images/data-usage.png "Data Usage"){: caption="Data Usage" caption-side="bottom"}

3. Configure the time selector. You can choose **Quick** to choose a preset or **Custom** to set a custom date and time range to view and compare usage across any timeframe.

    ![Data Usage time selector](/images/data-usage-timepicker-r114.png "Data Usage time selector"){: caption="Data Usage time selector" caption-side="bottom"}

4. Select the **User data sent** tab.


## Filtering options
{: #data-usage-analyzer-filter}

You can filter data by choosing one or more options in **Filtered by**:

- Entity Type: Define the type of data. Valid values are: `Logs` and `Metrics`.
- Priority: Defines the TCO data pipeline associated with the logs and metrics. Valid values are: `High`, `Medium`, `Low` and `Blocked`.
- Pillar: Defines the type of telemetry data. Valid values are: `Logs` and `Metrics`.



## Aggregation options
{: #data-usage-analyzer-agg}

You can aggregate data by choosing one or more options in **Group data by**:
- Entity Type: Define the type of data. Valid values are: `Logs` and `Metrics`.
- Priority: Defines the TCO data pipeline associated with the logs and metrics. Valid values are: `High`, `Medium`, `Low` and `Blocked`.
- Pillar: Defines the type of telemetry data. Valid values are: `Logs` and `Metrics`.

## Viewing data
{: #data-usage-analyzer-data}

You can view information about data ingestion volumes reported in bytes in the following widgets:
- *Current usage*: Average daily usage in the selected period
- *Max daily usage*: Highest daily ingested volume
- *Min daily usage*: Lowest daily ingested volume
- *Avg daily usage*: Average daily ingested volume


In the *Usage breakdown* section, you can monitor volumes of ingested data based on the filtering and group by options selected.

![Usage breakdown](/images/usage-breakdown.png "Usage breakdown"){: caption="Usage breakdown" caption-side="bottom"}
