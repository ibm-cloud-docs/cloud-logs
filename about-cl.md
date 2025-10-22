---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-22"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Features
{: #about-cl}

{{site.data.keyword.logs_full}} is an observability service in {{site.data.keyword.cloud_notm}} designed to help organizations monitor, troubleshoot, analyze, and alert on the performance of their applications and infrastructure in real time and long-term. By collecting and analyzing logs from cloud-native applications, servers, databases, and other IT systems, {{site.data.keyword.logs_full_notm}} provides actionable insights into system behavior, helping SRE and Dev teams quickly identify and resolve issues. With {{site.data.keyword.logs_full_notm}}, you can monitor operational data that is generated in {{site.data.keyword.cloud_notm}}, on-premises, and by other cloud providers. You can also monitor security data that is generated in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

As workloads generate an expanding amount of observability data, pressure is increasing on collection tools to process all the data. The data becomes expensive to manage and makes it harder to obtain actionable insights. It is harder to have fast, effective, and cost-efficient operational and performance management.

{{site.data.keyword.logs_full_notm}} is designed to help users take control of their observability data and expedite insights to reduce application downtime.

{{site.data.keyword.logs_full_notm}} supports integration with common workload environments on {{site.data.keyword.cloud_notm}}, on-premises, and other clouds, including VPC, {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.openshiftlong_notm}}. Integration with non-orchestrated environments, such as Linux and Windows, is also supported.

With {{site.data.keyword.logs_full_notm}}, you can send both log data and activity tracking events into the service, which gives you flexibility in how you handle your data. Log and event data can be sent to separate {{site.data.keyword.logs_full_notm}} instances or combined into a single instance to expand observability insights.

{{site.data.keyword.logs_full_notm}} processes incoming data and applies machine learning algorithms, including log aggregation and anomaly detection. This processing helps you focus on the root cause of issues.


- [Optimizing value and controlling your observability budget](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-tco)
- [Collecting data for centralized storage and analysis](/docs/cloud-logs?topic=cloud-logs-about-cl#features-1)
- [Adhering to regulations for compliance and security](/docs/cloud-logs?topic=cloud-logs-about-cl#features-7)
- [Predicting abnormal behaviour for promptly detection of abnormal situations](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-anomaly)
- [Generating metrics derived from logs to enhance observability](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-event2metrics)
- [Restructuring data for easy analysis and troubleshooting](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-parse)
- [Enriching telemetry data with context information for easier analysis](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-enrich)
- [Archiving logs for long-term storage](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-bucket)
- [Integrating with other applications](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-integrate)
- [Querying data to gain insights for troubleshooting and analysis](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-search)
- [Improving operational visibility to gain insights for better analysis](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-config)
- [Notifying issues to raise awareness and take action promptly](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-config)
- [Incident management control](/docs/cloud-logs?topic=cloud-logs-about-cl#about-cl-incident)

Let's explore these features.

## Optimizing value and controlling your observability budget
{: #about-cl-tco}

Not all data is valued equally. {{site.data.keyword.logs_full_notm}} helps optimize the value of the data that you keep by using the TCO optimizer.

When you review your observability needs and budget, you can select from three tiers of log and event processing:

* {{site.data.keyword.compliance}}: Data that is retained primarily for compliance obligations can be stored and searched as necessary at a low cost/GB.

* {{site.data.keyword.monitoring}}: Log and event data with analysis and alert value is processed at a mid-tier cost/GB. The mid-tier includes adding the definition of metrics from logs, allowing the visualization of trends and preparation for quickly handling future incidents.

* {{site.data.keyword.frequent-search}}: Select and configure most critical and highest value data to your operations for priority query results. Data in this tier is retained in hot storage.

In the TCO optimizer, you define policies to configure policies that define which data pipeline handles data after ingestion. Data prioritization before storing or indexing data reduces monitoring costs while simultaneously improving system visibility.

For more information, see [Controlling costs](/docs/cloud-logs?topic=cloud-logs-controlling-cost), [TCO Optimizer](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines) and [Data Usage](/docs/cloud-logs?topic=cloud-logs-data-usage).


## Collecting data for centralized storage and analysis
{: #features-1}

In {{site.data.keyword.logs_full_notm}}, you can collect telemetry data that is generated in {{site.data.keyword.cloud_notm}}, on-premises, and by other cloud providers.

{{site.data.keyword.logs_full_notm}} integrates with popular logging frameworks and libraries, enabling you to easily transfer your data to {{site.data.keyword.logs_full_notm}} for centralized storage and analysis.


## Adhering to regulations for compliance and security
{: #features-7}

Data security and compliance is an {{site.data.keyword.logs_full_notm}} priority.

{{site.data.keyword.logs_full_notm}} offers encryption at rest and in transit, access controls, and adheres to industry-standard security practices.

{{site.data.keyword.logs_full_notm}} helps businesses meet standards, compliance requirements and regulations, such as GDPR and HIPAA, by providing features such as data anonymization and audit logs.



## Predicting abnormal behaviour for promptly detection of abnormal situations
{: #about-cl-anomaly}

In {{site.data.keyword.logs_full_notm}}, you can detect abnormal behaviour by configuring anomaly detection alerts that use artificial intelligence algorithms to analyze incoming logs and predict their expected behavior for 24 hours.

For example, you might want to detect rising trends of errors related to bad API responses that cause a spike in your logs and indicate something usual is happening, discover when a transaction’s response time exceeds its usual duration, allowing you to pinpoint and address performance bottlenecks, or detect unexpected spike of logs in your environment due to outgoing traffic of a host that exceeds its usual levels and could indicate that a potential security breach is occurring.


## Generating metrics derived from logs to enhance observability
{: #about-cl-event2metrics}

In {{site.data.keyword.logs_full_notm}}, you can improve observability to identify performance issues, monitor system's reliability, or troubleshoot problems by using the `Event2metrics` feature.

For example, you could use a log-based metric to monitor the page load time, the duration of a process, or count the number of log entries that contain an error code.

As data is ingested, metric data is derived from your logs and converted into Prometheus metrics. You can use Dashboards to visualize your metrics. You can configure alerts to notify of unexpected behaviour.

For more information, see [Configuring collection of metrics from logs](/docs/cloud-logs?topic=cloud-logs-configure-event2metrics).

## Restructuring data for easy analysis and troubleshooting
{: #about-cl-parse}

You can restructure and parse log data to aid processing and increase the value of your data by using parsing rules.

{{site.data.keyword.logs_full_notm}} parsing tools help you evaluate if data is essential or redundant. Restructuring data can help you aggregate dissimilar information that teams need to quickly find to address incidents.

{{site.data.keyword.logs_full_notm}} is designed to convert log data to summarize what is happening. Using metrics that are generated from log data is a great way to look at vast amounts of data quickly when you search on different data sources.

For more information, see [Parsing rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules).

## Enriching telemetry data with context information for easier analysis
{: #about-cl-enrich}

In {{site.data.keyword.logs_full_notm}}, you can enrich your log data with additional context. You can automatically add fields to your JSON logs based on specific matches in your log data by using a pre-defined custom data source of your own. This way, you can enhance your log data with business, operations, or security information that is not available at run time, making telemetry data more meaningful and actionable for effective troubleshooting, root cause analysis, and performance optimization.

For more information, see [Enriching data](/docs/cloud-logs?topic=cloud-logs-enriching-data).


## Archiving logs for long-term storage
{: #about-cl-bucket}

In {{site.data.keyword.logs_full_notm}}, you can configure a data bucket and a metrics bucket in {{site.data.keyword.cos_full_notm}} to store your logs and metrics for long term storage and search. No need to reindex logs from the archive to explore and query archived data. You can use the same queries and dashboards that you use to initally monitor the data.

In the TCO optimizer, you define policies to configure policies that define which data pipeline handles data after ingestion. For data handled through the {{site.data.keyword.monitoring}} or the {{site.data.keyword.compliance}} pipelines, data is sent to the bucket only. All data that you choose to store for search across all the TCO data pipelines is stored in the data and metrics bucket.

Data is stored after enrichment policies and parsing rules have been applied so the data that you store for long-term storage includes all the context information that you choose to add and any additional restructure of log data that you might apply to enhance your monitoring, analysis and troubleshooting.

For more information, see [Configuring buckets for long term storage and search](/docs/cloud-logs?topic=cloud-logs-about-bucket).


## Integrating with other applications
{: #about-cl-integrate}

{{site.data.keyword.logs_full_notm}} is designed to integrate with most common application and systems management tools and fit within most toolchains. Sharing data with other operational tools is built in by design:

* Integrate with alert management tools by using webhook values within alert messages so that information is included in the alert. This information can be used to quickly identify the source that triggered the alert.

* Share alert data with the {{site.data.keyword.en_full_notm}} service for comprehensive {{site.data.keyword.cloud_notm}} alert management visibility and control.

* Share alert data with PagerDuty and other specialized alert management tools.

* Integrate with other observability, SIEM, and data analysis tools. {{site.data.keyword.logs_full_notm}} can send data to {{site.data.keyword.messagehub_full}}, a Kafka service implementation, where data can be shared with a wide variety of tools and applications.



## Querying data to gain insights for troubleshooting and analysis
{: #about-cl-search}

With {{site.data.keyword.logs_full_notm}}, you can search and easily query all data that is retained by {{site.data.keyword.logs_full_notm}}.

Data is stored in {{site.data.keyword.cos_full_notm}} in a search-friendly format. When rapid-search results are needed, data can also be stored in hot storage for priority insights into the data. Query results for both hot storage and buckets can be displayed in the same dashboards and views.

{{site.data.keyword.logs_full_notm}} offers multiple tools to effectively query data:

* Simple Boolean search.
* Regular expressions (RegEx queries) are available to match patterns in your log.
* Queries based on Apache Lucene for key value querying.
* Queries based on the {{site.data.keyword.logs_full_notm}} DataPrime. Dataprime is a query syntax for describing event transformations and aggregations. Allows users to explore data, perform schema on read transformations, group and aggregate fields, extract data, and much more.
* Prometheus Query Language (PromQL) to select and aggregate time series data derived from your logs.

Prompted help is available to construct queries for complex analysis.


## Improving operational visibility to gain insights for better analysis
{: #about-cl-config}

In {{site.data.keyword.logs_full_notm}}, you can improve operational visibility by configuring dashboards to gain insights for better analysis, troubleshooting and decision-making of your organization's environments and applications.

You can create unlimited, personalized custom dashboards catered to your specific observability needs, or take advantage of pre-built dashboards to help you analyze and visualize log data.

Preconfigured alerts and dashboards are available as extensions for common application environments can be tailored to your specific environment needs. For more information, see [Extensions](/docs/cloud-logs?topic=cloud-logs-extensions).

Dashboard insights, which are paired with {{site.data.keyword.logs_full_notm}} machine learning analytics, gives SREs the ability to quickly identify the start of an incident before it becomes a significant issue.

For more information, see [Dashboards](/docs/cloud-logs?topic=cloud-logs-about_dashboards).



## Notifying issues to raise awareness and take action promptly
{: #about-cl-alert}

You can configure alerts to detect and address issues before users notice them by proactively notifying you

Sophisticated alert rules can be configured to reduce triage time. Examples include:

* Notifying when a combination of alert events happens within a defined set of criteria.

* Receiving alerts when new errors or log types are detected, or anomalous values occur on established data.

For more information, see [Alerts](/docs/cloud-logs?topic=cloud-logs-alerts).

## Incident management control
{: #about-cl-incident}

{{site.data.keyword.logs_full_notm}} provides alert incident management control. This control helps manage the operation of workloads and comprehensive environments with maintenance windows that can be managed within the tool. When complex incidents occur triggering multiple alarms, users can see the situation quickly within {{site.data.keyword.logs_full_notm}}. Configured alert management within {{site.data.keyword.logs_full_notm}} can suppress unnecessary alerts to other alert management solutions.
