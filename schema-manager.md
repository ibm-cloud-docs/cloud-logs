---

copyright:
  years:  2024, 2026
lastupdated: "2026-04-01"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


#  Schema Management
{: #schema-manager}

In {{site.data.keyword.logs_full_notm}}, you can use the Schema Management to get a unified approach to governing your logs, letting you both discover the structure of ingested data and enforce the fields that matter most.
{: shortdesc}


- The `Schema Explorer` gives you full visibility into how your fields are structured and behave across your data. It surfaces key insights like field paths, data types (including type collisions), usage patterns, cardinality trends, and mapping exceptions, helping you spot inconsistencies before they cause issues.

- `Reserved fields` moves from observation to action. You can explicitly define which fields must always be available for querying, pre-mapping them on ingestion with a specific data type to avoid index limits, misclassification, or query breakage. Reserved fields ensure the critical parts of your schema remain consistent and performant. For more information, see [Reserved fields](/docs/cloud-logs?topic=cloud-logs-reserved-fields).

Together, these tools provide a powerful 1-2 punch for schemas hygiene: explore existing schema health, then reserve what's essential. Want to keep queries reliable and your observability costs in check? Start with the Schema Explorer, then use Reserved Fields, to solidify the parts of your schema that power your dashboards and alerts.
