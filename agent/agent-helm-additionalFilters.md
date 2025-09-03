---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring multiple filters
{: #agent-helm-additionalFilters}


You can configure multiple filters, such as modify, grep, and nest, to modify the data that is collected before it is delivered to a destination. You can use a filter to match, exclude, or enrich your log records with specific metadata.
{: shortdesc}

When you add a filter, the configuration is added to the [pipeline.filters](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/pipeline-section) section of the Fluent Bit yaml configuration.


Sample use cases:
- To add the correct metadata associated with a pod, you can use a filter plugin to enrich the log lines.

- There might be some filters that should be applied to both containers and host logs rather than including the action required in the `additionalKubeLogInputProcessors` and `additionalSystemLogsInputProcessors` after the normal processing has completed.

For example, you can add the `Modify` filter plugin in the `logs-values.yaml` file as follows:

```yaml
additionalFilters:
  - name: modify
    match: '*'
    set:
      - deployment_env production
```
{: codeblock}

Where
- `name` is set to the name of the filter plug-in. Determines which filter plug-in should be loaded by Fluent Bit.
- `match` defines the pattern that is used to match against the tags that are defined on incoming records. `Match` is case-sensitive. You can use the asterisk character `*` as a wildcard.
- `set` adds key/value pairs to each log record


After you modify the `logs-values.yaml`, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
