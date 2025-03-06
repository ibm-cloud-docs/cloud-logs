## Export data usage report using API
{: #data-usage-reports-api}
{: api}


You can export data usage report programmatically by calling the {{site.data.keyword.logs_full_notm}} API.

The following example shows a query that you can use to export the data usage overview report. When you call the API, replace the ID variables and IAM token with the values that are specific to your {{site.data.keyword.logs_full_notm}} instance.

Overview and detailed data usage reports can be exported using the `query` query parameter with values `daily` and `detailed`.

You can retrieve the data usage report for a specified time range for your {{site.data.keyword.logs_full_notm}} instance with `range` request parameters. Valid values for the `range` parameter are `current_month`, `last_30_days`, `last_90_days`, and `last_week`. The default is `current_month`.


```sh
curl 'https://{instance_ID}.api.{region}.logs.cloud.ibm.com/v1/data_usage?query=daily&&range=last_30_days' \
    -H 'Authorization: Bearer {iam_token}' \
    -H 'Content-Type: application/json' \
    -H 'Accept: application/json'
```
{: codeblock} 


A successful response returns the data usage overview report for the specified timerange. For more information about the API, see [Get data usage metrics export status or return data usage report](/apidocs/logs-service-api#export-data-usage){: external}.

## Export data usage report using CLI
{: #data-usage-reports-cli}
{: cli}

Before you begin, [follow the steps](/docs/cloud-logs?topic=cloud-logs-cloud-logs-cli-temp#logs-cli-prereq-temp) to set your {{site.data.keyword.logs_full_notm}} instance API endpoint.

To export data usage by using the {{site.data.keyword.logs_full_notm}}  CLI plug-in, run the **`ibmcloud logs data-usage`** command. For example, the following command exports the data usage detailed report for last 30 days.

```text
ibmcloud logs data-usage --query detailed --range last_30_days
```
{: pre}

Overview and detailed data usage reports can be exported using `query` parameter with values `daily` and `detailed`.

You can retrieve the data usage report over a specified time range for your {{site.data.keyword.logs_full_notm}} instance with `range` request parameters. Valid values of the `range` parameter are `current_month`, `last_30_days`, `last_90_days`, and `last_week`. The default is `current_month`.

A successful command outputs the data usage detailed report for the specified timerange.
