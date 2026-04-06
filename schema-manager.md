---

copyright:
  years:  2024, 2026
lastupdated: "2026-04-06"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


#  Schema Manager
{: #schema-manager}

In {{site.data.keyword.logs_full}}, you can use the Schema Manager to get a unified approach to governing your logs, letting you both discover the structure of ingested data and enforce the fields that matter most.
{: shortdesc}


The Schema Manager includes the following features:

`Schema Explorer`
:   Use the Schema Explorer to gain visibility into the fields that are indexed from your logs, see how they are structured and behave across your data, and spot inconsistencies before they cause issues. You can see their paths, any mapping exceptions, usage patterns, cardinality trends, and data types.

For more information, see [Schema Explorer](/docs/cloud-logs?topic=cloud-logs-schema-explorer).


`Reserved fields`
:  To take schema governance a step further, {{site.data.keyword.logs_full_notm}} provides Reserved Fields which are a way to explicitly define the fields that matter most for your queries, alerts, and dashboards.

Use Reserved fields to ensure the critical parts of your schema remain consistent. You can explicitly define the list of fields that must be available for querying through Priority Insights, pre-mapping them on ingestion with a specific data type to avoid index limits and mapping issues, misclassification, or query breakage.

For more information, see [Reserved fields](/docs/cloud-logs?topic=cloud-logs-reserved-fields).



While `Schema Explorer` helps you discover and analyze fields, `Reserved Fields` let you lock in critical ones, ensuring they are always indexed with the correct type and available for use.
{: attention}
