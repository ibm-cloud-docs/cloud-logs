---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Keep a copy of the original log
{: #agent-helm-raw-log}


When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to set `keepParsedLog` to `true` to retain a copy of the original log field after it has been successfully processed by the Kubernetes plug-in and the parser extracts the fields successfully.

The default is `false`.

Valid values are: `true`, `false`

Enabling this will result in duplicate log data, which may increase storage usage.
{: note}

Example configuration:

```yaml
keepParsedLog: false
```
{: codeblock}
