---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-15"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Configuring geo enrichments
{: #enrich-geo}

With the geo enrichment, you can automatically add IP-based geographical information, including ASN (Autonomous System Number) information, to your logs as new fields that can be queried, visualized, and reported. 

For example, you can add the country name, city name, continent name, postal code, and location geo point.


## Configuring a data enrichment
{: #enrich-data-steps}
{: ui}

1. [Launch the {{site.data.keyword.logs_full_notm}} UI.](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

2. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Data enrichment**.

3. Click **+ Add enrichment**.

4. Select **Geo enrichment**.  

5. Select the key and ASN information.

If you don’t have IP fields set, or your data isn’t JSON-formatted, you can use {{site.data.keyword.logs_full_notm}} rules to extract the IP addresses that are found in your log records by using the [Extract](/docs/cloud-logs?topic=parse-extract-rule) or [Parse](/docs/cloud-logs?topic=parse-rule).

6. Click **Create enrichment**

After you define the IP field, {{site.data.keyword.logs_full_notm}} adds geographical information to the logs based on the selected fields.

These fields are not added if the enrichment database does not have the queried IP.
{: important}

6. Click **Create enrichment**.



## Viewing a geo enrichment
{: #enrich-howto-view}
{: ui}

If you have a geo enrichment configured in your {{site.data.keyword.logs_full_notm}} instance, you can view the enrichment data in the {{site.data.keyword.logs_full_notm}} UI.

1. [Launch the {{site.data.keyword.logs_full_notm}} UI.](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

2. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Data enrichment**.

3. Click **View in explore screen** for the enrichment you want to view.

You can filter, transform, and aggregate the data using DataPrime.

The UI displays up to 2,000 rows, but queries apply to all the geo enrichment data, not just the data that is displayed.
{: note}
