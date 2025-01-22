---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-22"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} resources to {{site.data.keyword.logs_full_notm}} resources
{: #migration-instance-resources}

Learn about migrating {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} resources to {{site.data.keyword.logs_full_notm}} resources.
{: shortdesc}


{{/_include-segments/data-not-migrated.md}}

## Understanding how {{site.data.keyword.logs_full_notm}} compares to existing services
{: #migration-instance-resources-comparison}

In {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}, you can:

* Configure archiving for long-term storage by configuring an {{site.data.keyword.cos_full_notm}} bucket.

* Define views and alerts to help you monitor your account, applications and infrastructure, and troubleshoot and do problem determination.

* Define dashboards and screens with customizable widgets to visualize your data.

* Define exclusion rules to drop data at ingestion and control log volumes and costs.

* Define parsing rules to extract new fields that you can index and use for querying and faster searching.

* Configure index rate alerts to control the rate of indexing and ingestion.

{{site.data.keyword.logs_full_notm}} is a service that offers you all of the functions of {{site.data.keyword.la_full}} and {{site.data.keyword.at_full_notm}} and more. For more information, see [About
{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-about-cl).

## Migrating categories
{: #migration-instance-resources-categories}

You can migrate categories into folders. Foder names are unique within the instance.
{: note}

In {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}, you can use categories to group related resources. You have categories for views, for dashboards and for screens.

In {{site.data.keyword.logs_full_notm}}, you can use folders to group related resources. You have folders for views, and folders for dashboards.

When you migrate an instance, migration of categories is included in the migration.

In {{site.data.keyword.logs_full_notm}}, the name of a folder for views must be unique within the instance and the name of a folder for dashboards must be unique within the instance.
{: important}


## Migrating views and alerts
{: #migration-instance-resources-views}

You can migrate a view into a public view. You can migrate a view with an alert into a public view and an alert. View names are unique within an instance.
{: note}

In {{site.data.keyword.logs_full_notm}}, views and alerts are decoupled. You do not need a view to configure an alert. You can configure private views and public views. You can configure alerts.

- Alerts are a type of resource. They are not dependent on views.

- You can define different types of alerts such as standard alerts, flow alerts, and new value alerts. For information on the alert types that are supported, see [Alerts](/docs/cloud-logs?topic=cloud-logs-alerts&interface=ui#alert-types).

- You can use the `Incidents` page to manage alerts that are triggered.

- Alerts are triggered through the {{site.data.keyword.en_full_notm}} service. You configure the notification channels and conditions that trigger the alert in the {{site.data.keyword.en_full_notm}} service.

- For more information on alerts, see [Migrating alerts](/docs/cloud-logs?topic=cloud-logs-migration-alerts).

You can use the Migration tool to migrate views and alerts configured in {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}. When you migrate an instance, migration of views and alerts is included.
- A view is migrated to an {{site.data.keyword.logs_full_notm}} public view.
- A view with an alert is migrated to an {{site.data.keyword.logs_full_notm}} public view and an alert definition.


{{/_include-segments/verify-queries.md}}

In {{site.data.keyword.logs_full_notm}}, the name of a view must be unique within the instance.
{: important}

## Migrating dashboards and screens
{: #migration-instance-resources-dash}

You can migrate dashboards and screens into {{site.data.keyword.logs_full_notm}} dashboards.
{: note}

Dashboards and screens are migrated into dashboards in {{site.data.keyword.logs_full_notm}}.

- Tables are mapped into tables widgets.

- Gauges and counters are migrated into gauge widgets.

- Histograms are migrated into line chart widgets.

- The time-shifted graph is available by default through the **Logs** page, which is where you work with views in {{site.data.keyword.logs_full_notm}}.

- Pie charts are migrated into pie chart widgets.

You can also configure other widgets such as a vertical line chart, a horizontal line char, DataPrime creator widgets or even create widgets by using Markdown coding.

When you migrate an instance, migration of Dashboards and screens are included in the migration. For dashboards, only plots are migrated and streamlined, so you will need to manually customaize the dashboard layout.

In {{site.data.keyword.logs_full_notm}}, the name of a dashboard must be unique within the instance.
{: important}

## Migrating exclusion rules
{: #migration-instance-resources-excl}

You can migrate an exclusion rule by configuring a block parsing rule or configuring TCO policies.
{: note}

In {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}, you can define alerts on data that is excluded at ingestion by configuring an exclusion rule. However, in {{site.data.keyword.logs_full_notm}}, you cannot define alerts on data excluded by using a block parsing rule. If you need to configure alerts on data that is excluded, in {{site.data.keyword.logs_full_notm}}, you should configure the TCO optimizer and distribute logs through the {{site.data.keyword.frequent-search}} pipeline and the {{site.data.keyword.monitoring}} pipeline. You can define alerts on data managed through either data pipeline. For more information, see [Configuring the TCO Optimizer](/docs/cloud-logs?topic=cloud-logs-tco-optimizer).

In {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}, you can configure the exclusion rule so that you can view in livetail the data (shown as not retained). In {{site.data.keyword.logs_full_notm}}, you can also configure a block parsing rule so that you can view through the Livetail feature the data and store in the {{site.data.keyword.compliance}} data pipleine your excluded data. You can then query the excluded data directly from the archive.

You can use the Migration tool to migrate exclusion rules. When you migrate an instance, resources such as exclusion rules are included in the migration.


{{/_include-segments/verify-queries.md}}

## Migrating parsing rules
{: #migration-instance-resources-pars}

In {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}, you can define rules to extract new fields from data in a log record.

In {{site.data.keyword.logs_full_notm}}, you can configure different types of parsing rules such as extract, Timestamp Extract, and remove fields For more information, see [Parsing rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules). Even more, you can enrich your logs by adding fields to your JSON logs based on specific matches in your log data. For mroe information, see [Enriching data](/docs/cloud-logs?topic=cloud-logs-enriching-data).

To migrate parsing rules, you must configure an extract parsing rule in {{site.data.keyword.logs_full_notm}}. You can use RegEx expressions to define how you want to extract the data. {{site.data.keyword.logs_full_notm}} uses a Golang RegEx syntax.
{: note}

Similar to {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}s, you have a limit on the number of indexed fields per day that you can use for fast searching. In {{site.data.keyword.logs_full_notm}}, you can monitor the number of indexed fields and mapping exceptions that are generated as data is ingested. This limit applies to {{site.data.keyword.frequent-search}} searches only, that is, fast searches. It does not apply to searches on data that is stored in {{site.data.keyword.cos_full_notm}} where you can run unlimited searches or alerting.

You can use the Migration tool to find out the indexed fields that you have configured in your instance. Migration of indexed fields is done manually.



## Migrating data usage
{: #migration-instance-resources-usage}

In {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}}, you can monitor your daily and monthly usage quotas, and configure index rate alerts to be notified when an unexpected spike of data exceeds a threshold that you set based on your needs.

In {{site.data.keyword.logs_full_notm}}, you can enable the Data Usage feature to collect predefined metrics that you can use to monitor the GB that are ingested and your daily quota. You can then use these metrics in custom dashboards and alerts. In addition, you can get a report that details the amount of data that is ingested into your account by application, subsystem, and severity. The report also includes the amount of data that was excluded from ingestion based on your custom exclusion rules over the selected period.


## Migrating the archiving configuration
{: #migration-instance-resources-arch}

To migrate archiving, you must use new {{site.data.keyword.cos_full_notm}} buckets: one bucket to store the logs, and a second bucket to store the metrics.
{: note}

In {{site.data.keyword.logs_full_notm}}, you can configure a data bucket where the ingested data is stored. You own and manage the bucket and the data. A key differentiator from {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} is that with {{site.data.keyword.logs_full_notm}} you can run unlimited searches on your data from the UI.

You can also configure a metrics bucket to store any metrics that are generated from logs to optimize storage without sacrificing important data.

You can use the Migration tool to migrate your archiving configuration. For more information, see [Migrating instances with archiving configured](/docs/cloud-logs?topic=cloud-logs-migration-cos-bucket).
