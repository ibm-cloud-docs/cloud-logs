---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the maximum log length
{: #agent-helm-maxloglength}

If you have very long logs which exceed the maximum line length, specifying `maxLogLength` will truncate the log line to the specified number of characters. Truncating the log line ensures that the complete metadata is sent to {{site.data.keyword.logs_full_notm}}. If you want to apply processing by {{site.data.keyword.logs_full_notm}}, for example, using parsing rules, you need to keep the metadata and JSON structure of your log intact. The number of characters after which the log line will be truncated is determined by the `maxLogLength` value. The `maxLogLength` value can be between 1 and 30000 characters.
{: shortdesc}

The length of your metadata needs to be considered when specifying a `maxLogLength` value. The longer your metadata, the smaller your `maxLogLength` should be. The overall log size, including metadata, cannot exceed the [ingestion limits](/docs/cloud-logs?topic=cloud-logs-limits#limits-per-instance).

By default logs are not truncated before they are sent to {{site.data.keyword.logs_full_notm}} and will only be truncated when a `maxLogLength` value is specified.

For example:

```yaml
maxLogLength: 12000
```
