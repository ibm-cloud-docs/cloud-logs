---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Override the default severity field
{: #agent-helm-severity}

When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to set `severityFieldName` to override the default severity field that is sent to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

Use this option if your log messages use a non-standard field name (for example, `Log_Level`, `logSeverity`, and so on) to indicate severity.

When configured:
- A new filter is added to the pipeline.
- This filter injects a severity field into each log record.
- The value of severity is populated from the custom field you specify.

```yaml
severityFieldName: Log_Level
```
{: codeblock}

After you modify the `logs-values.yaml`, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
