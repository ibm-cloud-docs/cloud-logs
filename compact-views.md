---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-16"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Viewing your data in a compact format in {{site.data.keyword.logs_full_notm}}
{: #compact-views}

{{site.data.keyword.logs_full}} {{site.data.keyword.compact-mode}} provide a simplified and streamlined view providing data with a view to focus on active monitoring and querying without additional widgets, filters, or statistics. This view is helpful when working with large-scale data and performance-heavy queries.
{: shortdesc}

Use the {{site.data.keyword.compact-mode}} to optimize query performance by triggering statistics and filters only when required. This view also enhances usability by removing unnecessary visual clutter when exploring data.
{: tip}


## Accessing views
{: #compact-access-view}

In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

The last view and mode you had opened will be displayed. If no view was previously open, all views will be displayed.


## Switching to the {{site.data.keyword.compact-mode}}
{: #compact-compact-view}

Set **{{site.data.keyword.compact-mode}}** to on.

When {{site.data.keyword.compact-mode}} is enabled, the page opens or reloads without widgets, fiters, and log, tempate, and trace count statistics.

The selected mode will be retained between your user sessions.

## Differences in behavior when using the {{site.data.keyword.compact-mode}}
{: #compact-diff}

### Colapsed filter panel
{: #compact-filter}

When opening the collapsed filter panel in {{site.data.keyword.compact-mode}}, associated statistics are not displayed for better performance.

You can show previously hidden filters in {{site.data.keyword.compact-mode}}. Click the ![Settings icon](/icons/setting.svg "Settings icon") > **Show Filters**.

### Enabling statistics
{: #compact-stats}

If you want to see statistics you need to turn {{site.data.keyword.compact-mode}} off. When fast mode is turned off, all relevant queries are run including:

* Filter statistics
* Log count statistics
* Widget queries
