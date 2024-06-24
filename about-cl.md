---

copyright:
  years:  2024
lastupdated: "2024-05-30"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# About {{site.data.keyword.logs_full_notm}}
{: #about-cl}

{{site.data.keyword.logs_full}} provides observability services for {{site.data.keyword.cloud_notm}} so you can view, analyze, and alert on activity tracking events and logging activity. Logging data can be sent from orchestrated and nonorchestrated environments.
{: shortdesc}

As workloads generate an expanding amount of observability data, pressure is increasing on collection tools to process all the data. The data becomes expensive to manage and makes it harder to obtain actionable insights. It is harder to have fast, effective, and cost-efficient operational and performance management.

{{site.data.keyword.logs_full_notm}} is designed to help users take control of their observability data and expedite insights to reduce application downtime.

{{site.data.keyword.logs_full_notm}} supports integration with common workload environments on {{site.data.keyword.cloud_notm}} including {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.openshiftlong_notm}}. Integration with nonorchestrated environments, such as Linux, is also supported.

With {{site.data.keyword.logs_full_notm}}, you can send both log data and activity tracking events into the service, which gives you flexibility in how you handle your data. Log and event data can be sent to separate {{site.data.keyword.logs_full_notm}} instances or combined into a single instance to expand observability insights.

{{site.data.keyword.logs_full_notm}} processes incoming data and applies machine learning algorithms, including log aggregation and anomaly detection. This processing helps you focus on the root cause of issues.

## Alerting
{: #about-cl-alert}

Sophisticated alert rules can be configured to reduce triage time. Examples include:

* Notifying when a combination of alert events happens within a defined set of criteria.

* Receiving alerts when new errors or log types are detected, or anomalous values occur on established data.

## Parsing
{: #about-cl-parse}

You can parse log data to aid processing and increase the value of your data.

{{site.data.keyword.logs_full_notm}} parsing tools help you evaluate if data is essential or redundant. Restructuring data can help you aggregate dissimilar nformation that teams need to quickly find to address incidents.
Often a simple sparkline of frequency over time will provide the needed insight to quickly determine the problem.

{{site.data.keyword.logs_full_notm}} is designed to convert log data to summarize what is happening. Using metrics that are generated from log data is a great way to look at vast amounts of data quickly when you search on different data sources.

## Enriching
{: #about-cl-enrich}

You can easily enrich your log data with {{site.data.keyword.logs_full_notm}}. You can automatically add fields to your JSON logs based on specific matches in your log data by using a pre-defined custom data source of your own. This way, you can enhance your log data with business, operations, or security information that is not available at run time.

## Searching
{: #about-cl-search}

With {{site.data.keyword.logs_full_notm}}, you can search and easily query all data that is retained by {{site.data.keyword.logs_full_notm}}.

Data is stored in {{site.data.keyword.cos_full_notm}} in a search-friendly format. When rapid-search results are needed, data can also be stored in hot storage for priority insights into the data. Query results for both hot storage and buckets can be displayed in the same dashboards and views.

{{site.data.keyword.logs_full_notm}} offers multiple tools to effectively query data:

* Simple Boolean search
* RegEx queries
* Queries based on Apache Lucene
* Queries based on the {{site.data.keyword.logs_full_notm}} DataPrime language.

Prompted help is available to construct queries for complex analysis.

## Configuration
{: #about-cl-config}

You can configure {{site.data.keyword.logs_full_notm}} dashboards to better visualize your environments. Preconfigured alerts and dashboards for common application environments can be tailored to your specific environment needs. Dashboard insights, which are paired with {{site.data.keyword.logs_full_notm}} machine learning analytics, gives SREs the ability to quickly identify the start of an incident before it becomes a significant issue.

{{site.data.keyword.logs_full_notm}} provides alert incident management control. This control helps manage the operation of workloads and comprehensive environments with maintenance windows that can be managed within the tool. When complex incidents occur triggering multiple alarms, users can see the situation quickly within {{site.data.keyword.logs_full_notm}}. Configured alert management within {{site.data.keyword.logs_full_notm}} can suppress unnecessary alerts to other alert management solutions.

## Integrating with other applications
{: #about-cl-integrate}

{{site.data.keyword.logs_full_notm}} is designed to integrate with most common application and systems management tools and fit within most toolchains. Sharing data with other operational tools is built in by design:

* Integrate with alert management tools by using webhook values within alert messages so that information is included in the alert. This information can be used to quickly identify the source that triggered the alert.

* Share alert data with the {{site.data.keyword.en_full_notm}} service for comprehensive {{site.data.keyword.cloud_notm}} alert management visibility and control.

* Share alert data with PagerDuty and other specialized alert management tools.

* Integrate with other observability, SIEM, and data analysis tools. {{site.data.keyword.logs_full_notm}} can send data to {{site.data.keyword.messagehub_full}}, a Kafka service implementation, where data can be shared with a wide variety of tools and applications.

* Integrate with your workload and bespoke tools. {{site.data.keyword.logs_full_notm}} supports launching into and out of the service by using a defined set of parameters. You can automate and streamline your SRE or users’ ability to navigate the comprehensive workloads and maintain smooth context-switching between tools.


## Optimizing value and controlling your observability budget
{: #about-cl-tco}

Not all data is valued equally. {{site.data.keyword.logs_full_notm}} helps optimize the value of the data that you keep. When you review your observability needs and budget, you can select from three tiers of log and event processing:

* {{site.data.keyword.compliance}}: Data that is retained primarily for compliance obligations can be stored and searched as necessary at a low cost/GB.

* {{site.data.keyword.monitoring}}: Log and event data with analysis and alert value is processed at a mid-tier cost/GB. The mid-tier includes adding the definition of metrics from logs, allowing the visualization of trends and preparation for quickly handling future incidents.

* {{site.data.keyword.frequent-search}}: Select and configure most critical and highest value data to your operations for priority query results. Data in this tier is retained in hot storage.

## Learn more
{: #about-cl-learn}

For more information about {{site.data.keyword.logs_full_notm}} features, see the following topics.

| For more information about | See |
|----------------------------|-----|
| Overview of features | [Link](/docs/cloud-logs?topic=cloud-logs-features) |
| {{site.data.keyword.tco-optimizer}} | [Link](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines) |
| Parsing rules | [Link](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) |
| Enriching data | [Link](/docs/cloud-logs?topic=cloud-logs-enriching-data) |
| Alerting | [Link](/docs/cloud-logs?topic=cloud-logs-alerts) |
| Extensions | [Link](/docs/cloud-logs?topic=cloud-logs-extensions)|
| Data usage | [Link](/docs/cloud-logs?topic=cloud-logs-data-usage) |
| Metadata fields | [Link](/docs/cloud-logs?topic=cloud-logs-metadata) |
{: caption="Links where you can find more information about {{site.data.keyword.logs_full_notm}} features" caption-side="bottom"}

