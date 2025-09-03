---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# `additionalServiceOptions`
{: #agent-helm-additionalServiceOptions}

You can set the `additionalServiceOptions` to add configuration options to the `service` section of the Fluent Bit configuration. This will add entries to the [service](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/service-section) section of the Fluent Bit yaml configuration.
{: shortdesc}

For example:

```yaml
additionalServiceOptions:
  storage.backlog.mem_limit: 5G
```
{: codeblock}

After you modify the `logs-values.yaml` file, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
