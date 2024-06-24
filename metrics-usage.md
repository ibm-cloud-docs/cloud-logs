---

copyright:
  years:  2024
lastupdated: "2024-06-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Exploring metrics usage
{: #metrics-usage}

In {{site.data.keyword.logs_full_notm}}, you can discover your current metric usage and data trends by viewing the **Metrics Usage** page. You can visualize your estimated usage, identify the most resource-intensive metrics, and evaluate the impact of code changes on your usage.
{: shortdesc}

You can see estimates of your metrics usage that is categorized by:

* Metric name
* Label name
* Label-value pair
* Label value count by label

The highest 1000 metrics are displayed sorted by permutations in descending order.

By viewing usage by metric name per series, you can understand daily quota consumption.

Byte and unit calculations are approximate and might not be identical to data usage. On average, a variance exists between estimated and billable usage. The margin of error is larger for smaller usage volumes due to the nature of the estimation.
{: important}

## Exploring metrics usage
{: #eplore-m-usage}

To explore your metrics usage, complete the following steps:

1. In the navigation bar, click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Metrics Usage**.

2. In **Search**, enter a metric or label of interest and adjust the time frame to analyze usage data for the day and time (UTC).

   The series count is the number of metric permutations. The percentage is the metric's percentage against the total permutations.

   The 7-day average is the weekly average of total permutations.
