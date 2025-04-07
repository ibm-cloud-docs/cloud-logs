---

copyright:
  years:  2024, 2025
lastupdated: "2025-04-06"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Mapping log severities to {{site.data.keyword.logs_full_notm}} severities
{: #severities}

Log records can be ingested with severity values that do not match {{site.data.keyword.logs_full_notm}} severities. {{site.data.keyword.logs_full_notm}} maps ingested severity values to {{site.data.keyword.logs_full_notm}} severity values.
{: shortdesc}

Mapped value meanings and the equivalent [API severity values](/docs/cloud-logs?topic=cloud-logs-send-logs-api) are shown in the following table.

| Log record severity value | Mapped to | API mapped value |
|---------------------------|-----------|------------------|
| `emergency` | `Critical` | 6 |
| `alert` | `Critical` | 6 |
| `fatal` | `Critical` | 6 |
| `f` | `Critical` | 6 |
| `critical` | `Critical` | 6 |
| `crit` | `Critical` | 6 |
| `error` | `Error` | 5 |
| `e` | `Error` | 5 |
| `failure` | `Error` | 5 |
| `exception` | `Error` | 5 |
| `exceptin` | `Error` | 5 |
| `err` | `Error` | 5 |
| `warning` | `Warn` | 4 |
| `w` | `Warn` | 4 |
| `Failed` | `Warn` | 4 |
| `fail` | `Warn` | 4 |
| `warn` | `Warn` | 4 |
| `notice` | `Info` | 3 |
| `informational` | `Info` | 3 |
| `info` | `Info` | 3 |
| `i` | `Info` | 3 |
| `information` | `Info` | 3 |
| `verbose` | `Verbose` | 2 |
| `v` | `Verbose` | 2 |
| `trace` | `Verbose` | 2 |
| `debug` | `Debug` | 1 |
| `d` | `Debug` | 1 |
| `50` | `Critical` | 6 |
| `40` | `Error` | 5 |
| `30` | `Warn` | 4 |
| `20` | `Info` | 3 |
| `10` | `Debug` | 1 |
| `100` | `Debug` | 1 |
| `200` | `Verbose` | 2 |
| `300` | `Info` | 3 |
| `400` | `Warn` | 4 |
| `500` | `Error` | 5 |
| `600` | `Critical` | 6 |
| `1` | `Debug` | 1 |
| `2` | `Verbose` | 2 |
| `3` | `Info` | 3 |
| `4` | `Warn` | 4 |
| `5` | `Error` | 5 |
| `6` | `Critical` | 6 |
{: caption="Mapping of ingested log severity values to {{site.data.keyword.logs_full_notm}} severity values" caption-side="bottom"}
