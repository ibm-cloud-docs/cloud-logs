---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Using the Data Usage Analyzer
{: #data-usage-analyzer}

In {{site.data.keyword.logs_full_notm}}, you can use the *Data Usage Analyzer* to gain insights into log ingestion volumes by prioriy.
{: shortdesc}

In the *Data Usage Analyzer*, you can monitor logs to:
- Identify high-volume logs
- Understand data ingestion patterns
in the *User data sent* tab.


## Launching the Data Usage Analyzer
{: #data-usage-analyzer-launch}

Complete the following steps:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Usage icon](/icons/usage.svg "Usage") > **Data Usage**.

    The *Data Usage* page opens.

    ![Data Usage](/images/data-usage.png "Data Usage"){: caption="Data Usage" caption-side="bottom"}

3. Configure the time selector. You can choose **Quick** to choose a preset or **Custom** to set a custom date and time range to view and compare usage across any timeframe.

    ![Data Usage time selector](/images/data-usage-timepicker.png "Data Usage time selector"){: caption="Data Usage time selector" caption-side="bottom"}

4. Select the **User data sent** tab.


## Filtering options
{: #data-usage-analyzer-filter}

You can filter data by choosing one or more options in **Filtered by**:

- Entity Type: Define the type of data. Valid values are: `Logs` and `Metrics`.
- Priority: Defines the TCO data pipeline associated with the logs. Valid values are: `High`, `Medium`, `Low` and `Blocked`.
- Pillar: Defines the type of telemetry data. Valid values are: `Logs` and `Metrics`.


## Aggregation options
{: #data-usage-analyzer-agg}

You can aggregate data by choosing one or more options in **Group data by**:
- Entity Type: Define the type of data. Valid values are: `Logs` and `Metrics`.
- Priority: Defines the TCO data pipeline associated with the logs. Valid values are: `High`, `Medium`, `Low` and `Blocked`.

## Viewing data
{: #data-usage-analyzer-data}

You can view information about data ingestion volumes reported in bytes in the following widgets:
- Current usage
- Blocked days
- Max daily usage
- Min daily usage
- Avg daily usage


In the *Usage breakdown* section, you can monitor volumes of ingested data based on the filtering and group by options selected.

![Usage breakdown](/images/usage-breakdown.png "Usage breakdown"){: caption="Usage breakdown" caption-side="bottom"}
