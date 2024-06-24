---

copyright:
  years:  2024
lastupdated: "2024-04-01"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Generating data usage overview reports
{: #data-usage-reports}

In {{site.data.keyword.logs_full_notm}}, you can export, as csv, a `Data Usage Report` that provides an overview of your instance's data usage for the current month, the previous 30 days, or the previous 90 days.
{: shortdesc}


You can generate a report for:
- The current month
- Last 30 days
- Last 90 days


## Prereqs
{: #data-usage-reports-prereqs}

- You must [configure a metrics bucket.](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
- You must enable the data usage feature. For more information, see [Enabling data usage metrics](/docs/cloud-logs?topic=cloud-logs-data-usage-metrics).

## Information included in a report
{: #data-usage-reports-1}

The Data Usage Report includes the following information:

- Date
- Data Blocked Sent(GB)
- Low Logs Data Sent(GB)
- Medium Logs Data Sent(GB)
- High Logs Data Sent(GB)
- High Metrics Data Sent(GB)
- Total Data Sent(GB)


## Generating a report
{: #data-usage-reports-2}

Complete the following steps to export the Data Usage Report as a CSV file:

1. In the navigation bar, click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Data Usage**.

2. Select **Export as CSV**.

3. Select **Data usage overview report** for the *Data Usage Overview Report type*.

4. Select the time range.

5. Click **EXPORT**.
