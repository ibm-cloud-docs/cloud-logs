---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring input plugins by using Helm
{: #agent-helm-additionalInputs}

You can set the `additionalInputs` option to introduce additional Fluent Bit input plug-in definitions. For each input plugin, you must configure the `processors` section that define how to modify or enrich the data before it reaches the filtering or output destinations.

For example, you might need to add a new input plugin if you have a file with special parsing requirements.

The following template shows a sample configuration for data that is sent to an {{site.data.keyword.logs_full_notm}} instance:

```yaml
additionalInputs:
  - name: tail
    tag: var.log.<AppID>
    path: /var/log/<AppDir>/<AppLogFileName>
    processors:
      logs:
        - name: content_modifier
          action: insert
          key: applicationName
          value: <YourAPPName>
        - name: content_modifier
          action: insert
          key: subsystemName
          value: <YourAppSubsystemName>

```
{: codeblock}

For example, the `logs-values.yaml` file looks as follows when you add 2 input plugins:

```yaml
additionalInputs:
  - name: tail
    tag: var.log.myapp
    path: /var/log/myapp/myapp.log
    processors:
      logs:
        - name: content_modifier
          action: insert
          key: applicationName
          value: my-application
        - name: content_modifier
          action: insert
          key: subsystemName
          value: my-subsystem

  - name: tail
    tag: var.log.myapp1
    path: /var/log/myapp1/myapp1.log
    processors:
      logs:
        - name: content_modifier
          action: insert
          key: applicationName
          value: my-application-1
        - name: content_modifier
          action: insert
          key: subsystemName
          value: my-subsystem-1
```
{: codeblock}

Each log record must have an applicationName and a subsystemName, metadata that is required when sent to an {{site.data.keyword.logs_full_notm}} instance.
{: important}

After you modify the `logs-values.yaml` file, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.



## Adding additional processors
{: #additionalKubeLogInputProcessors}


You can configure the `additionalKubeLogInputProcessors` section to introduce additional processors for container logs after the normal processing has completed.  This may be useful for example, to introduce an additional parser within the processor pipeline. This will add entries to the [pipeline.inputs.processors](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/pipeline-section) section of the Fluent Bit yaml configuration.



```yaml
additionalKubeLogInputProcessors:
  - name: parser
    parser: json
    key_name: log
    reserve_data: true
```
{: codeblock}
