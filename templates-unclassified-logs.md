---

copyright:
  years:  2024
lastupdated: "2024-06-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Managing unclassified logs
{: #templates-unclassified-logs}

{{site.data.keyword.logs_full_notm}} learns from the logs that are ingested through the {{site.data.keyword.frequent-search}} and {{site.data.keyword.monitoring}} data pipelines, and groups similar logs into templates to help you determine logs requiring your attention and others that might not. Sometimes log records cannot be grouped into templates. These log records are known as unclassified logs.
{: shortdesc}


There are different reasons for which a log record is considered an unclassified log:


## Cardinality of the metadata is too high
{: #templates-unclassified-logs-1}

Per {{site.data.keyword.logs_full_notm}} instance, you can have up to 1000 branches by default.
{: note}

When the number of branches exceeds the allowed amount per instance, you might see unclassified logs.

Any of the metadata fields is used for log aggregation and definition of a branch. The metadata fields that are always used are:
- Application name
- Subsystem name
- Severity

A branch is calculated by identifying the different combinations of metadata values for application name, subsystem name, and severity. Each combination of unique metadata values constitutes one branch.

For example, when one of the metadata fields contains a high cardinality, you might see unclassified logs since you might have reached the limit of branches per instance.

To reduce the cardinality of the values of a metadata field, you might use [parsing rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) to reduce the number of distint values.


## Cardinality of a field is too high
{: #templates-unclassified-logs-2}

Per branch, you can have up to 150 templates per branch.
{: note}

The following fields are also used for log aggregation and definition of a template:
- `text`
- `message`
- `msg`
- `log`
- `innerMessage`

When the cardinality of the values of any of these fields is too high and exceeds the number of templates per branch, you might see unclassified logs.

You can use [parsing rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) to narrow the value in the field to a shorter message.


## Log size is too long
{: #templates-unclassified-logs-3}

When a log is too long, you might see unclassified logs.

You can use [parsing rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) to remove unnecessary data.
