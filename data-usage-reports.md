---

copyright:
  years:  2024, 2026
lastupdated: "2026-06-03"

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

- You must [configure a metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).
- You must enable the data usage feature. For more information, see [Enabling Data Usage metrics](/docs/cloud-logs?topic=cloud-logs-data-usage-metrics).

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
{: ui}

Complete the following steps to export the Data Usage Report as a CSV file:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Usage icon](/icons/usage.svg "Usage") > **Data Usage**.

    The *Data Usage* page opens. 

4. Select **Overview report** for the *Data Usage Report type*.

5. Select the date range.

6. Choose the export format.

    Valid values are: `CSV`, `TSV`, and `JSON`.

    Use `CSV`, and `TSV` to manage data through spreadsheets.

    Use `JSON` to manage data through automated integrations.

7. For export formats `CSV` and `TSV`, select whether you want to include headers in the report. When selected, column names will be added as first row of the exported file.

8. Select whether you want to apply current filters to the report.

9. Click **Export**.

## Exporting an overview data usage report using API
{: #ov-data-usage-reports-api}
{: api}


You can export an overview data usage report programmatically by calling the {{site.data.keyword.logs_full_notm}} API.

The following example shows a query that you can use to export the data usage overview report. When you call the API, replace the ID variables and IAM token with the values that are specific to your {{site.data.keyword.logs_full_notm}} instance.

Overview data usage reports are exported using the `query` query parameter with value `daily`.

You can retrieve the overview data usage report for a specified time range for your {{site.data.keyword.logs_full_notm}} instance with `range` request parameters. Valid values for the `range` parameter are `current_month`, `last_30_days`, `last_90_days`, and `last_week`. The default is `current_month`.


```sh
curl 'https://{instance_ID}.api.{region}.logs.cloud.ibm.com/v1/data_usage?query=daily&&range=last_30_days' \
    -H 'Authorization: Bearer {iam_token}' \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json'
```
{: codeblock}


A successful response returns the data usage overview report for the specified time range. For more information about the API, see [Get data usage metrics export status or return data usage report](/apidocs/logs-service-api#export-data-usage){: external}.

## Exporting an overview data usage report using CLI
{: #ov-data-usage-reports-cli}
{: cli}

Before you begin, [follow the steps](/docs/cloud-logs?topic=cloud-logs-cloud-logs-cli-temp#logs-cli-prereq-temp) to set your {{site.data.keyword.logs_full_notm}} instance API endpoint.

To export data usage by using the {{site.data.keyword.logs_full_notm}} CLI plug-in, run the **`ibmcloud logs data-usage`** command. For example, the following command exports the data usage detailed report for last 30 days.

```text
ibmcloud logs data-usage --query daily --range last_30_days
```
{: pre}

Overview data usage reports are exported using `query` parameter with value `daily`.

You can retrieve the data usage report over a specified time range for your {{site.data.keyword.logs_full_notm}} instance with `range` request parameters. Valid values of the `range` parameter are `current_month`, `last_30_days`, `last_90_days`, and `last_week`. The default is `current_month`.

A successful command returns the data usage daily report for the specified time range.
