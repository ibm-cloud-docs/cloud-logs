---

copyright:
  years:  2024, 2026
lastupdated: "2026-06-26"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# About Data Usage
{: #data-usage}

In {{site.data.keyword.logs_full_notm}}, you can get detailed insights into your data usage through the *Data Usage page* or through the *Data Usage pre-defined custom dashboard*.
{: shortdesc}


## Prerequisites
{: #data-usage-prereqs}

1. You must attach a metrics bucket to your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Configuring the metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket).

2. Enable Data Usage system metrics. For more information, see [Enabling System metrics](/docs/cloud-logs?topic=cloud-logs-data-usage-metrics).


## Launching the Data Usage page
{: #data-usage-launch}

Through the *Data Usage page*, you can view information related to:
- Ingested logs and metrics through the *User data sent* tab. For more information, see [Analyzing user data ingested](/docs/cloud-logs?topic=cloud-logs-data-usage-analyzer).
- Metrics usage through the *Metrics Usage* tab. For more information, see [Analyzing metrics usage](/docs/cloud-logs?topic=cloud-logs-data-usage-analyzer).

For example, you can use the information in the *Data Usage* page to:
- Investigate spikes and anomalies in a period of time.
- Run accurate period-over-period comparisons for cost and planning.


Complete the following steps to launch the *Data Usage Page*:

1. Navigate to your {{site.data.keyword.logs_full_notm}} instance: **Observability** > **Logging** > **Cloud Logs** > *Your Service Instance* > **Open Dashboard**.

2. Select the **Usage** icon ![Usage icon](/icons/usage.svg "Usage") > **Data Usage**.

    The *Data Usage page* opens.

    ![Data Usage](/images/data-usage.png "Data Usage"){: caption="Data Usage" caption-side="bottom"}

3. Configure the time selector. You can choose **Quick** to choose a preset or **Custom** to set a custom date and time range to view and compare usage across any timeframe.

    ![Data Usage time selector](/images/data-usage-timepicker-r114.png "Data Usage time selector"){: caption="Data Usage time selector" caption-side="bottom"}


## Launching the Data Usage pre-defined custom dashboard
{: #data-usage-dashboard-launch}

The *System Monitoring* extension includes a predefined dashboard that displays your account's data usage. For more information, see [System Monitoring extension](/docs/cloud-logs?topic=cloud-logs-extensions-system-monitoring){: external}.

To deploy and launch the *Data Usage dashboard*, see [Deploying an extension](/docs/cloud-logs?topic=cloud-logs-extensions-mgmt&interface=ui#extensions-mgmt-deploy-ui).

## Generating reports
{: #data-usage-reports}

From the *Data Usage* page, you can generate and export data usage information. Choose any of the following options:

- [Generating data usage overview reports](/docs/cloud-logs?topic=cloud-logs-data-usage-reports)
- [Generating detailed usage reports](/docs/cloud-logs?topic=cloud-logs-data-usage-detailed-reports)
