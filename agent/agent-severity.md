---

copyright:
  years:  2024, 2025
lastupdated: "2025-04-23"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Understanding how the {{site.data.keyword.agent}} parses severities
{: #agent-severity}

The {{site.data.keyword.logs_full_notm}} {{site.data.keyword.agent}} will attempt to determin the severity value of a routed log record. If the {{site.data.keyword.agent}} cannot determine the severity of a log record, it sets the severity to `info`.
{: shortdesc}

The severity of a log record is extracted after the log was picked up and modified by the {{site.data.keyword.agent}}.
This means, that all filters and modifications defined in the {{site.data.keyword.agent}} configuration are applied before the record is parsed in preparation for sending it to an {{site.data.keyword.logs_full_notm}} instance.

Severity parsing is done in a specific order.
As soon as a match is found, the parsing is completed and subsequent steps are not executed.

First, the top level elements of the record are searched for fields named `severity`, `level` or `logLevel`, in that order.
If a match is found, the corresponding value is mapped according to the mapping table.
The mapping is case-insensitive and will find all upper-case and lower-case spellings.

If the first step did not yield any results, the same fields (`severity`, `level` or `logLevel`) are searched nested below the keys `message` and `log`.
If a match is found, the value is mapped as described in the mapping table, where upper-case and lower-case spellings are not relevant.

| Log record severity value (case-insensitive) | Mapped to | API mapped value |
|---------------------------|-----------|------------------|
| `debug` | `Debug` | 1 |
| `verbose` | `Verbose` | 2 |
| `info` | `Info` | 3 |
| `warn` | `Warn` | 4 |
| `warning` | `Warn` | 4 |
| `error` | `Error` | 5 |
| `err` | `Error` | 5 |
| `critical` | `Critical` | 6 |
| `crit` | `Critical` | 6 |
| `alert` | `Critical` | 6 |
| `emerg` | `Critical` | 6 |
{: caption="Mapping of log record severity values to {{site.data.keyword.logs_full_notm}} severity values" caption-side="bottom"}

Should the first steps not find any of the predefined field names, a simple text search is applied to fields named `message` and `log`.
In this case, the search is case-sensitive and will only find the spellings defined in the mapping table.

| Log record severity value | Mapped to | API mapped value |
|---------------------------|-----------|------------------|
| `debug`, `Debug`, `DEBUG` | `Debug` | 1 |
| `verbose`, `Verbose`, `VERBOSE` | `Verbose` | 2 |
| `info`, `Info`, `INFO` | `Info` | 3 |
| `warn`, `Warn`, `WARN` | `Warn` | 4 |
| `error`, `Error`, `ERROR` | `Error` | 5 |
| `critical`, `Critical`, `CRITICAL` | `Critical` | 6 |
{: caption="Mapping of text search severity values to {{site.data.keyword.logs_full_notm}} severity values" caption-side="bottom"}

