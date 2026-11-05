---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Very long log lines are shortened or split by {{site.data.keyword.agent}}
{: #troubleshoot-agent-long-lines}
{: troubleshoot}
{: support}

Log lines that exceed the size limit are shortened or split when {{site.data.keyword.agent}} sends them to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

Some log lines in {{site.data.keyword.logs_full_notm}} are shorter than the original log lines, or a single log line appears as more than one log record.
{: tsSymptoms}

The log lines exceed the size limit.
{: tsCauses}

Lines over the size limit are shortened or split. A line that was split is marked as such in {{site.data.keyword.logs_full_notm}}.

For more information about the size limits, see [{{site.data.keyword.logs_full_notm}} limits](/docs/cloud-logs?topic=cloud-logs-limits#limit-ingestion). To control where long lines are truncated, see [Configuring the maximum log length](/docs/cloud-logs?topic=cloud-logs-agent-helm-maxloglength).
{: tsResolve}
