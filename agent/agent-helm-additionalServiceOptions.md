---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# `additionalServiceOptions`
{: #agent-helm-additionalServiceOptions}

This option can be used to add configuration options to the `service` section of the Fluent Bit configuration. This will add entries to the [service](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/service-section) section of the Fluent Bit yaml configuration.

```yaml
additionalServiceOptions:
  storage.backlog.mem_limit: 5G
```
{: codeblock}
