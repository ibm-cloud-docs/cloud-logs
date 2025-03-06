---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-06"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Generating detailed usage reports
{: #data-usage-detailed-reports}

In {{site.data.keyword.logs_full_notm}}, you can export, as csv, a `Data Usage Report` that provides an overview of your instance's data usage for the current month, the previous 30 days, or the previous 90 days.
{: shortdesc}


You can generate a report for:
- The current month
- Last 30 days
- Last 90 days


## Prereqs
{: #data-usage-detailed-reports-prereqs}

- You must [configure a metrics bucket.](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
- You must enable the data usage feature. For more information, see [Enabling data usage metrics](/docs/cloud-logs?topic=cloud-logs-data-usage-metrics).

## Information included in a report
{: #data-usage-detailed-reports-1}

The detailed usage report includes the following information per application, subsystem, severity, priority, TCO policy, and type:

- Date
- Total Data Sent(GB)


## Generating a report
{: #data-usage-detailed-reports-2}
{: ui}

Complete the following steps to export the Data Usage Report as a CSV file:

1. In the navigation bar, click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Data Usage**.

2. Select **Export as CSV**.

3. Select **Detailed usage report** for the *Data Usage Overview Report type*.

4. Select the time range.

5. Click **EXPORT**.

## Exporting a detailed data usage report using API
{: #data-usage-reports-api}
{: api}


You can export a detailed data usage report programmatically by calling the {{site.data.keyword.logs_full_notm}} API.

The following example shows a query that you can use to export the detailed data usage report. When you call the API, replace the ID variables and IAM token with the values that are specific to your {{site.data.keyword.logs_full_notm}} instance.

Detailed data usage reports are exported using the `query` query parameter with value `detailed`.

You can retrieve the detailed data usage report for a specified time range for your {{site.data.keyword.logs_full_notm}} instance with `range` request parameters. Valid values for the `range` parameter are `current_month`, `last_30_days`, `last_90_days`, and `last_week`. The default is `current_month`.


```sh
curl 'https://{instance_ID}.api.{region}.logs.cloud.ibm.com/v1/data_usage?query=detailed&&range=last_30_days' \
    -H 'Authorization: Bearer {iam_token}' \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json'
```
{: codeblock} 


A successful response returns the detailed data usage report for the specified timerange. For more information about the API, see [Get data usage metrics export status or return data usage report](/apidocs/logs-service-api#export-data-usage){: external}.

## Exporting the detailed data usage report using CLI
{: #data-usage-reports-cli}
{: cli}

Before you begin, [follow the steps](/docs/cloud-logs?topic=cloud-logs-cloud-logs-cli-temp#logs-cli-prereq-temp) to set your {{site.data.keyword.logs_full_notm}} instance API endpoint.

To export the detailed data usage report by using the {{site.data.keyword.logs_full_notm}} CLI plug-in, run the **`ibmcloud logs data-usage`** command. For example, the following command exports the data usage detailed report for last 30 days.

```text
ibmcloud logs data-usage --query detailed --range last_30_days
```
{: pre}

Detailed data usage reports are exported using `query` parameter with value `detailed`.

You can retrieve the detailed data usage report over a specified time range for your {{site.data.keyword.logs_full_notm}} instance with `range` request parameters. Valid values of the `range` parameter are `current_month`, `last_30_days`, `last_90_days`, and `last_week`. The default is `current_month`.

A successful command outputs the detailed data usage report for the specified timerange.
