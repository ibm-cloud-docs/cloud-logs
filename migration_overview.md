---

copyright:
  years:  2024
lastupdated: "2024-05-24"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating to {{site.data.keyword.logs_full_notm}}
{: #migration-intro}

Learn about migrating {{site.data.keyword.la_full}} or {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

## Understanding how {{site.data.keyword.logs_full_notm}} compares to existing services
{: #service-comparison}

In {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}, you can:

* Configure archiving for long-term storage by configuring an {{site.data.keyword.cos_full_notm}} bucket.

* Define views and alerts to help you monitor your account, applications and infrastructure, and troubleshoot and do problem determination.

* Define dashboards and screens with customizable widgets to visualize your data.

* Define exclusion rules to drop data at ingestion and control log volumes and costs.

* Define parsing rules to extract new fields that you can index and use for querying and faster searching.

* Configure index rate alerts to control the rate of indexing and ingestion.

{{site.data.keyword.logs_full_notm}} is a service that offers you all of the functions of {{site.data.keyword.la_full}} and {{site.data.keyword.at_full_notm}} and more.

* To migrate archiving, you must configure new {{site.data.keyword.cos_full_notm}} buckets: one bucket to store the logs, and a second bucket to store the metrics.

   In {{site.data.keyword.logs_full_notm}}, you can configure a data bucket where the ingested data is stored. You own and manage the bucket and the data. A key differentiator from {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} is that with {{site.data.keyword.logs_full_notm}} you can run unlimited searches on your data from the UI. Searching can include all of your data that is stored in the {{site.data.keyword.cos_full_notm}} bucket. 
   
   You can also configure a metrics bucket to store any metrics that are generated from logs to optimize storage without sacrificing important data.

* Views and alerts are decoupled in {{site.data.keyword.logs_full_notm}}. You do not need a view to configure an alert. 

   You can define private views and public views. When you migrate a view where an alert is configured, you can configure a public view and an alert as separate unrelated resources.

* Dashboards and screens are migrated into dashboards in {{site.data.keyword.logs_full_notm}}.

   * Tables are mapped into tables widgets.

   * Gauges and counters are migrated into gauge widgets.

   * Histograms are migrated into line chart widgets.

   * The time-shifted graph is available by default through the **Logs** page, which is where you work with views in {{site.data.keyword.logs_full_notm}}.

   * Pie charts are migrated into pie chart widgets.
    
   You can also configure other widgets such as a vertical line chart, a horizontal line char, DataPrime creator widgets or even create widgets by using Markdown coding.

* Exclusion rules are migrated by configuring block parsing rules. You can configure dropped data so it can still be viewed in the **Livetail** feature and archived into your {{site.data.keyword.cos_full_notm}} bucket.

   You cannot define alerts on dropped data.
   {: note}
   
   You can configure dropped data to be stored in {{site.data.keyword.compliance}} where you can query it directly from the archive.

* To migrate parsing rules, you must configure an extract parsing rule in {{site.data.keyword.logs_full_notm}}. You can use RegEx expressions to define how you want to extract the data. 

   {{site.data.keyword.logs_full_notm}} uses a Golang RegEx syntax.
   {: note}

   Similar to {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}s, you have a limit to the number of indexed fields per day that you can use for fast searching. In {{site.data.keyword.logs_full_notm}}, you can monitor the number of indexed fields and mapping exceptions that are generated as data is ingested. This limit applies to {{site.data.keyword.frequent-search}} searches, that is, fast searches. It does not apply to searches on data that is stored in {{site.data.keyword.cos_full_notm}} where you can run unlimited searches or alerting.

* In {{site.data.keyword.logs_full_notm}}, you can enable the **Data Usage** feature to collect predefined metrics that you can use to monitor the GB that are sent and the daily quota. You can use these metrics in custom dashboards and alerts. In addition, you can get a report that details the amount of data that is ingested into your account. The report also includes the amount of data that was excluded from ingestion based on your custom exclusion rules over the selected period.


## Migration tool
{: #migov-tool}

The {{site.data.keyword.logs_full}} migration tool is a command-line tool that you can use to migrate your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance configuration to {{site.data.keyword.logs_full_notm}}.

The tool requires minimal user interaction. {{site.data.keyword.iamshort}} authentication and APIs are used to get the details about your current {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance.

The migration tool migrates only configuration information. No data is migrated from {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instances to the new {{site.data.keyword.logs_full_notm}} instances.
{: important}

![Overview of migrating to {{site.data.keyword.logs_full_notm}}](/images/migration-tool.png "Overview of migrating to {{site.data.keyword.logs_full_notm}}"){: caption="Figure 1. Overview of migrating to {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}


## How you can use the migration tool
{: #migov-use-cases}

You can use the migration tool for:

- Planning your migration.

    You can collect information about {{site.data.keyword.cloud_notm}} resources that are impacted by the migration in an account. The information that is generated includes information about current resources, and Terraform scripts for the new resources. You can use this information to find out what needs to be migrated and define your migration plan.

- Migrating 1 instance and its subresources.

    When you migrate 1 instance, you also get information about current resources, and Terraform scripts for the new resources.

