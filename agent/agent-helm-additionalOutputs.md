---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Configuring multiple outputs by using Helm
{: #agent-helm-additionalOutputs}

You can set the `additionalOutputs` option to introduce additional Fluent Bit output plug-in definitions to the current pipeline. For example, you might need to send logs to multiple {{site.data.keyword.logs_full_notm}} instances.

Additional outputs that you configure add entries to the [pipeline.outputs](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/pipeline-section) section of the Fluent Bit yaml configuration.


For example, the `logs-values.yaml` file looks as follows when you add an output plugin:

```yaml
additionalOutputs:
  - name: logger-icl-output-plugin
    id: logs-router-icl-output-plugin
    match: '*'
    # Connection
    target_host: "replace with host"
    target_port: 443
    target_path: /logs/v1/singles
    ...
```
{: codeblock}


After you modify the `logs-values.yaml` file, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
