---

copyright:
  years:  2024, 2025
lastupdated: "2025-12-02"

keywords:

subcollection: cloud-logs

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.logs_full_notm}}
{: #logs-release-notes}

Use these release notes to learn about the latest updates to {{site.data.keyword.logs_full}}.
{: shortdesc}



## 3 December 2025
{: #cloud-logs-dec0325}
{: release-note}

Functional updates and fixes made available on 17 October 2025 are now available in additional regions.

:   Regions supporting new functionality and fixes:

    * Dallas (`us-south`)
    * Frankfurt (`eu-de`)
    * London (`eu-gb`)
    * Madrid (`eu-es`)
    * Montreal (`ca-mon`)
    * Osaka (`jp-osa`)
    * Sao Paulo (`br-sao`)
    * Sydney (`au-syd`)
    * Tokyo (`jp-tok`)
    * Toronto (`ca-tor`)
    * Washington, DC (`us-east`)

    For more information about the changes, see the [17 October 2025 Release notes](#cloud-logs-oct1725)

## 20 November 2025
{: #cloud-logs-nov2025}
{: release-note}

Functional updates and fixes made available on 17 October 2025 are now available in additional regions.

:   Regions supporting new functionality and fixes:

    * Frankfurt (`eu-de`)
    * London (`eu-gb`)
    * Madrid (`eu-es`)
    * Montreal (`ca-mon`)
    * Osaka (`jp-osa`)
    * Sao Paulo (`br-sao`)
    * Sydney (`au-syd`)
    * Tokyo (`jp-tok`)
    * Toronto (`ca-tor`)
    * Washington, DC (`us-east`)

    For more information about the changes, see the [17 October 2025 Release notes](#cloud-logs-oct1725)


## 13 November 2025
{: #cloud-logs-nov1325}
{: release-note}

Functional updates and fixes made available on 17 October 2025 are now available in additional regions.

:   Regions supporting new functionality and fixes:

    * Frankfurt (`eu-de`)
    * London (`eu-gb`)
    * Madrid (`eu-es`)
    * Montreal (`ca-mon`)
    * Sao Paulo (`br-sao`)
    * Sydney (`au-syd`)
    * Toronto (`ca-tor`)

    For more information about the changes, see the [17 October 2025 Release notes](#cloud-logs-oct1725)

## 12 November 2025
{: #cloud-logs-nov1225}
{: release-note}

Functional updates and fixes made available on 17 October 2025 are now available in additional regions.

:   Regions supporting new functionality and fixes:

    * Frankfurt (`eu-de`)
    * London (`eu-gb`)
    * Madrid (`eu-es`)
    * Montreal (`ca-mon`)
    * Sao Paulo (`br-sao`)
    * Sydney (`au-syd`)

    For more information about the changes, see the [17 October 2025 Release notes](#cloud-logs-oct1725)

## 10 November 2025
{: #cloud-logs-nov1025}
{: release-note}

Functional updates and fixes made available on 17 October 2025 are now available in additional regions.

:   Regions supporting new functionality and fixes:

    * Frankfurt (`eu-de`)
    * London (`eu-gb`)
    * Montreal (`ca-mon`)
    * Sao Paulo (`br-sao`)
    * Sydney (`au-syd`)

    For more information about the changes, see the [17 October 2025 Release notes](#cloud-logs-oct1725)

## 6 November 2025
{: #cloud-logs-nov0625}
{: release-note}

Functional updates and fixes made available on 17 October 2025 are now available in additional regions.

:   Regions supporting new functionality and fixes:

    * London (`eu-gb`)
    * Montreal (`ca-mon`)
    * Sao Paulo (`br-sao`)
    * Sydney (`au-syd`)

    For more information about the changes, see the [17 October 2025 Release notes](#cloud-logs-oct1725)

## 4 November 2025
{: #cloud-logs-nov0425}
{: release-note}

Functional updates and fixes made available on 17 October 2025 are now available in additional regions.

:   Regions supporting new functionality and fixes:

    * Montreal (`ca-mon`)
    * Sao Paulo (`br-sao`)
    * Sydney (`au-syd`)

    For more information about the changes, see the [17 October 2025 Release notes](#cloud-logs-oct1725)


## 30 October 2025
{: #cloud-logs-oct3025}

Release of the {{site.data.keyword.agent}} version 1.7.0
:   For more information, see the [Release notes for the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-release-notes-agent#logs-router-agent-oct3025)

## 27 October 2025
{: #cloud-logs-oct2725}
{: release-note}

Functional updates and fixes made available on 17 October 2025 are now available in additional regions.

:   Regions supporting new functionality and fixes:

    * Montreal (`ca-mon`)
    * Sydney (`au-syd`)

    For more information about the changes, see the [17 October 2025 Release notes](#cloud-logs-oct1725)



## 17 October 2025
{: #cloud-logs-oct1725}
{: release-note}

Functional updates and fixes are available in the Montreal (`ca-mon`) region only.

:   New features included in this release.

    * Additional capabilities are now supported for alerts with the introduction of a new `alert_definition` API method. Changes are also made as a result to the {{site.data.keyword.en_full_notm}} payload.  See the following documentation topics for information about the alerts API changes and actions you might need to take as a result.
    
       * [Considerations for new alert and priority configuration](/docs/cloud-logs?topic=cloud-logs-new-version-considerations)
       * [Alert priorities](/docs/cloud-logs?topic=cloud-logs-priorities)
       * [Terraform changes required to convert alerts](/docs/cloud-logs?topic=cloud-logs-migrate_alert_definitions)

    * [Alert] New support for [multi-condition alerts](/docs/cloud-logs?topic=cloud-logs-multi-condition).

    * [Alert] New support for [anomaly detection](/docs/cloud-logs?topic=cloud-logs-alerts-config-metric&interface=ui#alerts-config-metric-anomaly) in metric alerts.

    * [Reserved Fields](/docs/cloud-logs?topic=cloud-logs-reserved-fields) is a new function letting you make sure that important fields are always indexed and available for search in {{site.data.keyword.frequent-search}}.

    * [Custom Enrichments] You can now [view](/docs/cloud-logs?topic=cloud-logs-enrich-howto&interface=ui#enrich-howto-view) a custom enrichment in the UI and [download](/docs/cloud-logs?topic=cloud-logs-enrich-howto&interface=ui#enrich-howto-download) a custom enrichment CSV file to your local system.

    * [UI] [Visual Explorer](/docs/cloud-logs?topic=cloud-logs-visual-explorer) is a powerful new tool that integrates a multifunctional Explore display with customizable dashboard widgets, enhancing your ability to explore logs.

    * [UI] The **Logs** view is enhanced to support [a detailed view of an individual log record](/docs/cloud-logs?topic=cloud-logs-log-details).

    * [Query] [CLI](/docs/cloud-logs?topic=cloud-logs-query-data&interface=cli#background-query-data-cli) and [API](/apidocs/logs-service-api#submit-background-query) support is available for background archive queries (asynchronous archive queries).

    * [DataPrime] Support is available for the following functions:

       * [arrayContains](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-array#arrayContains)
       * [inArray](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-array#inArray)

    * [Incidents] [**Watch data** now presents undetected values that triggered an alert.](/docs/cloud-logs?topic=cloud-logs-incidents#incidents-history) This gives visibility into undetected values that contributed to the alerts, making it easier to understand the full context of an incident.

:   Features that have been removed:

    * The Datamap feature is removed and is no longer supported.

:   Issues that have been resolved:

    * [Query] Fixed a bug where downloading large files in [Asynchronous Archive Queries](/docs/cloud-logs?topic=cloud-logs-query-archive-data-bucket#query_archive) was failing.

    * [Alert] Fixes an issue with **Verify Alert** where results were inconsistent.

    * [UI]/[Views] Fixed a bug when managing text column fields in saved views was not working.

    * [UI] Fixed a bug where layout settings were not restored when switching between views.

    * [UI]/[CustomDashboards] Fixed a bug when a DataPrime query including `groupby` aggregation returned inconsistent results.

    * [UI] Fixed a bug when switching between two saved views keeps the filters from the previous unsaved view.

    * [All logs] Fixed a bug where `segment.manifests` files were stored under wrong path in {{site.data.keyword.cos_full_notm}}.

    * [Query] Improved a warning message displayed when querying from **All logs** to handle cases where the data might be deleted from the bucket because of a lifecycle policy.

    * [Query] Fixed a bug where running a DataPrime query in {{site.data.keyword.frequent-search}} was failing.

    * [UI]/[CustomDashboards] Fixed a bug where `open in explore` was not redirecting correctly to the **Logs** page.

    * [Streams] Fixed a bug where the filtering query was producing unexpected results in some scenarios.



## 12 September 2025
{: #cloud-logs-sep1225}

Release of the {{site.data.keyword.agent}} version 1.6.3
:   For more information, see the [Release notes for the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-release-notes-agent#logs-router-agent-sep1225)

## 26 August 2025
{: #cloud-logs-aug2625}

Release of the {{site.data.keyword.agent}} version 1.6.2
:   For more information, see the [Release notes for the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-release-notes-agent#logs-router-agent-aug2625)



## 31 July 2025
{: #cloud-logs-jul3125}

Montreal support
:   The {{site.data.keyword.logs_full_notm}} service is fully supported in the Montreal (`ca-mon`) region.



## 9 July 2025
{: #cloud-logs-jul0925}

Updated Montreal considerations
:   As {{site.data.keyword.cloud_notm}} provides support for the Montreal (`ca-mon`) region, you need to understand how {{site.data.keyword.cloud_notm}} Observability services are made available and the actions you need to take to operate in Montreal.


## 26 June 2025
{: #cloud-logs-jun2625}

Release of the {{site.data.keyword.agent}} version 1.6.1
:   For more information, see the [Release notes for the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-release-notes-agent#logs-router-agent-jun2625)


## 5 June 2025
{: #cloud-logs-jun0525}

Release of the {{site.data.keyword.agent}} version 1.6.0
:   For more information, see the [Release notes for the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-release-notes-agent#logs-router-agent-jun0525)



## 16 May 2025
{: #cloud-logs-may1625}
{: release-note}


[DataPrime] DataPrime enhancements
:   DataPrime now support the [`multigrouby` operator](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#multigroupby).

    DataPrime now supports the [`union` operator](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#stitch).

    DataPrime now supports the [`join cross` operator](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#join)

    DataPrime now supports passing of query parameter values using [`$p`](/docs/cloud-logs?topic=cloud-logs-query-parameters).

[UI] Compact mode
:   [Compact mode](/docs/cloud-logs?topic=cloud-logs-compact-views) provides a simplified and streamlined view, enabling users to focus on active monitoring and querying without additional widgets, filters, or statistics.

[UI] Shared URL
:   Enhancements added to the [share the URL functionality](/docs/cloud-logs?topic=cloud-logs-share_url) so you can share a URL of the the current view of the logs explore screen.

[UI] New extensions
:   New [extensions](/docs/cloud-logs?topic=cloud-logs-extensions) are available:

    - [Activity Tracking](/docs/cloud-logs?topic=cloud-logs-extensions-activity-tracking): Use to get insights into your {{site.data.keyword.cloud_notm}} activity tracking data.
    - [{{site.data.keyword.containerlong_notm}}](/docs/cloud-logs?topic=cloud-logs-extensions-kubernetes):  Use to get insights into your {{site.data.keyword.containerlong_notm}} logs.
    - [{{site.data.keyword.databases-for-mysql_full}}](/docs/cloud-logs?topic=cloud-logs-extensions-db-mysql):  Use to get insights into your {{site.data.keyword.databases-for-mysql_full}} logs.
    - [{{site.data.keyword.databases-for-postgresql_full}}](/docs/cloud-logs?topic=cloud-logs-extensions-db-postgresql):  Use to get insights into your {{site.data.keyword.databases-for-postgresql_full}} logs.

[Custom dashboards] Variable support
:   [Variables](/docs/cloud-logs?topic=cloud-logs-variables) can be configured as a placeholder for a value that is used in queries. When used in custom dashboards, your dashboard's queries update to display data for that value.


Fixes implemented
:   The following issues are resolved.

    [Alerts] Fixed an issue where the `log_example` field in an alert notification was sometimes including a null value.

    [Custom Dashboards] Fixed an issue where widgets from metrics data were intermittently failing to load.

    [API] Fixed an issue in the alerts list API where the `notification_payload_filters` field contained empty values.

    [Data Usage] Fixed an issue in the data usage graph where usage for some days was displayed as null.

    [UI] Fixed multiple issue where the display of some screens in dark mode was broken.

    [Alerts] Fixed an issue where `condition_timeframe` in notification didn't match the time frame/window defined in the alert configuration.





## 24 February 2025
{: #cloud-logs-feb2425}
{: release-note}

Geo enrichment
:   [Geo enrichment](/docs/cloud-logs?topic=cloud-logs-enriching-data#geo-enrichment) now supports ASN (Autonomous System Number). ASN information will be added to the logs when geo enrichment is used.

[DataPrime] DataPrime enhancements
:   DataPrime now support the [`join` operator](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#join) types `inner`, `full`, and `left`.

    DataPrime now supports the [`stitch` operator](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators#stitch).

[UI] Shared URL
:   Support added so you can [share the URL](/docs/cloud-logs?topic=cloud-logs-share_url) of the the current view of the logs explore screen.

Fixes implemented
:   The following issues are resolved.
    - [UI] Resolved the issue in the custom dashboard where no data was shown in widgets when querying logs from priority insights.
    - [UI] Resolved the issued where livetail did not display UTF-8 encoded characters.
    - [UI] Resolve the issue when expanding the info panel hid the contents behind the navigation menu.



## 6 February 2025
{: #cloud-logs-feb0625}
{: release-note}

Context-based restrictions
:  {{site.data.keyword.logs_full_notm}} now supports context-based restrictions (CBR). For more information see, [Protecting resources with context-based restrictions](/docs/cloud-logs?topic=cloud-logs-iam-cbr&interface=ui).

## 5 February 2025
{: #cloud-logs-feb0525}
{: release-note}

Notice regarding successful {{site.data.keyword.cos_full_notm}} read activity tracking events
:   {{site.data.keyword.atracker_full_notm}} drops successful `cloud-object-storage.object.read` events that are initiated by {{site.data.keyword.logs_full_notm}} instances because they are not needed. For more information see [Why am I not seeing successful read activity tracking events for {{site.data.keyword.cos_full_notm}} activity generated by {{site.data.keyword.logs_full_notm}}?](/docs/cloud-logs?topic=cloud-logs-ts-cos-events).

Documentation about using regex for queries
:   Additional information is available about using regex for queries. For more information, see [Using regex when querying data](/docs/cloud-logs?topic=cloud-logs-query-regex).

## 12 December 2024
{: #cloud-logs-dec1224}
{: release-note}

[UI]\[LiveTail] Livetail support
:   Livetail now supports `Application` and `Subsystem` drop-down filters which can be used to filter logs based on `Application` and `Subsystem`.

Fixes implemented
:   The following issues are resolved.
    - [Query] - Fixed an issue where running a query in `All Logs` would result in a "Query Failed" message with no results returned even if the query ran up to the maximum timeout of 5 minutes.
    - [Alerts] - Fixed an error where Metric alerts were not triggering notifications. 
    - [UI]\[Logs] - Fixed an issue where the selected keys in the `Content` column are reset when switching between `Priority Insights` and `All Logs`. 

## 25 November 2024
{: #cloud-logs-nov2524}
{: release-note}

Fixes implemented
:   The following issues are resolved.   
    - [API]\[Views] - Fixed a bug where setting `quick_selection` using the API sets a custom selection in the UI.
    - [UI]\[TCO] - Resolved an error when clicking **Reset all overrides** resulted in displaying `ERROR: Failed to reset all overrides`.
    - [API]\[View Folder] - Fixed failure when updating view folders through the API.
    - [API]\[Events2Metrics] - Fixed failure when updating Events to Metrics rules through the API.
    - [Query] - Fixed query errors when using longer query windows, for example, for 6 or 12 hours.
    - [UI] - Fixed an error where the dashboard login displayed intermittent HTTP 500 errors.
    - [UI] - Fixed log highlighting for `surrounding logs` improving the ability to view the context around the logs. 
    - [Alerts] - Fixed an error where the alert payload was not sent as valid JSON.
    - [UI]\[TCO] - Fixed an error where editing an existing TCO policy would wait to refresh for a long time.

## 6 November 2024
{: #cloud-logs-nov0624}
{: release-note}

Fixes implemented
:   The following issue is resolved. 
    - Fixed custom dashboards displaying "Something went wrong" when selecting Analyze and Alert.



## 18 September 2024
{: #cloud-logs-sep1824}
{: release-note}

CSE endpoint support
:   {{site.data.keyword.logs_full_notm}} now supports [CSE endpoints](/docs/cloud-logs?topic=cloud-logs-cse_proxy).

## 4 September 2024
{: #cloud-logs-sep0424}
{: release-note}

Documentation updates affecting {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.logs_routing_full_notm}}
:   Significant documentation updates have been made to the {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.logs_routing_full_notm}} documentation sets with information related to using agents to send data to {{site.data.keyword.logs_full_notm}} moved from the [{{site.data.keyword.logs_routing_full_notm}} documentation](/docs/logs-router) to the [{{site.data.keyword.logs_full_notm}} documentation](/docs/cloud-logs).

## 29 August 2024
{: #cloud-logs-aug2924}
{: release-note}

Osaka (`jp-osa`) and Sao Paulo (`br-sao`) region support
:   Osaka and Sao Paulo are now online regions for the {{site.data.keyword.logs_full_notm}} service in the {{site.data.keyword.cloud_notm}}. {{site.data.keyword.logs_full_notm}} instances can now be provisioned in Osaka and Sao Paulo.


## 22 August 2024
{: #cloud-logs-aug2224}
{: release-note}

London (`eu-gb`), Sydney (`au-syd`), and Tokyo (`jp-tok`) region support
:   London, Sydney, and Tokyo are now online regions for the {{site.data.keyword.logs_full_notm}} service in the {{site.data.keyword.cloud_notm}}. {{site.data.keyword.logs_full_notm}} instances can now be provisioned in London, Sydney, and Tokyo.

## 8 August 2024
{: #cloud-logs-aug0824}
{: release-note}

Washington (`us-east`) and Dallas (`us-south`) region support
:   Washington and Dallas are now online regions for the {{site.data.keyword.logs_full_notm}} service in the {{site.data.keyword.cloud_notm}}. {{site.data.keyword.logs_full_notm}} instances can now be provisioned in Washington and Dallas.

## 30 July 2024
{: #cloud-logs-jul2424}
{: release-note}

Toronto (`ca-tor`) region support
:   Toronto is now an online region for the {{site.data.keyword.logs_full_notm}} service in the {{site.data.keyword.cloud_notm}}. {{site.data.keyword.logs_full_notm}} instances can now be provisioned in Toronto.


## 24 June 2024
{: #cloud-logs-jun2424}
{: release-note}

{{site.data.keyword.logs_full}} is generally available
:   {{site.data.keyword.logs_full_notm}} is a service in the {{site.data.keyword.cloud_notm}}.

   For more information about the {{site.data.keyword.logs_full_notm}} service, see [Getting started with {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-getting-started&interface=cli).
