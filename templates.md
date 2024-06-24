---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Using templates
{: #templates}

{{site.data.keyword.logs_full_notm}} learns from the logs that are ingested through the {{site.data.keyword.frequent-search}} and {{site.data.keyword.monitoring}} data pipelines, and groups similar logs into templates to help you determine logs requiring your attention and others that might not.
{: shortdesc}



## How are templates generated from logs
{: #templates-how}

As data is ingested, automatic log aggregation groups log entries into a narrow set of patterns by using machine learning. Each log that is received by {{site.data.keyword.logs_full_notm}} is analyzed for constant log variable data.

Log aggregation is based on repetitive log activity over a 24-hour period or over 100 K logs.
{: note}

First, metadata fields are analyzed and used for log aggregation and definition of a branch. The metadata fields that are always used are:
- Application name
- Subsystem name
- Severity

Then, the following fields are also used for log aggregation and definition of a template:
- `text`
- `message`
- `msg`
- `log`
- `innerMessage`

When log aggregation processes all ingested data, the logs that match a template must have an identical JSON structure. Any small variation of the JSON fields will result in a different template being created.




## Launching the templates page
{: #templates-view}

Log aggregations can be found as templates in the **Templates** tab in the **Logs** page.

To access the templates tab, complete the following steps:

1. In the navigation, click the *Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs templates**.

   In the **Logs** view you can also click the **Templates** tab to open the template view.
   {: tip}

2. Click a log field to see the unique field values in the aggregated logs.

3. Click the number of occurrences for a template to see the details about the occurrences of the logs included in the aggregation.

4. Select the three dots to view the raw log, copy the permalink to access quickly the log at a later time, or open the info panel.



## Viewing logs associated with a template
{: #templates-view-1}

From the templates page, hover over the column **First seen** and click the magnifying glass icon to open a view that shows the logs that are associated with the template.

## Limits
{: #templates-limits}

- Per {{site.data.keyword.logs_full_notm}} instance, you can have up to 1000 branches by default.
- Per branch, you can have up to 150 templates per branch.
