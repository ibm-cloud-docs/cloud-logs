---

copyright:
  years:  2024
lastupdated: "2024-10-08"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_full_notm}} limits
{: #limits}

{{site.data.keyword.logs_full}} has limits that need to be considered when using the service.
{: shortdesc}

## Character support
{: #unicode}

{{site.data.keyword.logs_full_notm}} does not provide full Unicode support for multibyte characters.

## Limits per instance
{: #limits-per-instance}

{{site.data.keyword.logs_full_notm}} has limits for each provisioned instance.

| Item | Limit |
|------|-------|
| Alerts | 500 |
| Parsing rules | 70 |
| Enrichments | 10 |
| Events to Metrics labels | 8 |
| Ingestion log size | 32 K |
| Largest log size processed by the pipeline | 33 K |
| Branches | 1500 |
| Query time range | 8 days |
| Maximum number of fields | 1500 |
{: caption="Limits per instance" caption-side="bottom"}

## Log ingestion limits
{: #limit-ingestion}

When you send data to an {{site.data.keyword.logs_full_notm}} instance:
- Logs cannot be older than 24 hours.
- Logs cannot be more than 4 hours into the future.

{{site.data.keyword.logs_full_notm}} limits the data ingested by a service instance per day.
- If a user sends data too fast, ingestion is throttled.
- If user uses all of the allowed daily ingestion limit, data that is received after that point is blocked and the data is dropped.



Data in OpenSearch is calculated based on index size after compression.
{: note}

For a single ingestion request {{site.data.keyword.logs_full_notm}}, these limitations exist:

* `request_timeout`: 30 seconds
* `request_body_limit_byte`s: 10 MiB


{{_include-segments/query-limits.md}}
