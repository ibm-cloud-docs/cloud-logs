---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring multiple parsers by using Helm
{: #agent-helm-additionalParsers}

You can configure the `additionalParsers` section in the `logs-values.yaml` file to introduce a new parser and introduce your own parsers. This will add entries to the [parsers](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/parsers-section) section of the Fluent Bit yaml configuration.


For example, you can add a parser in the `logs-values.yaml` file as follows:


```yaml
additionalParsers:
  - name: json_raw
    format: json
```
{: codeblock}


After you modify the `logs-values.yaml`, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
