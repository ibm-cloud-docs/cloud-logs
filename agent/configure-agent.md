---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}


# Configuring whether logs are included or excluded
{: #configure-include-exclude}

You can specify whether logs are included or excluded from collection based on a configured path or file name.
{: shortdesc}

## Including paths
{: #include-paths}

To specify included paths, do the following:

1. [Download the YAML configuration file for your environment.](/docs/logs-router?topic=logs-router-download-iclr-agent-configuration-file)
2. Open the downloaded YAML configuration file in a text editor. 
3. Locate the `input-kubernetes.conf` section.
4. Update the `Path` parameter to specify the log sources that you want to collect.

By default, the {{site.data.keyword.logs_routing_full_notm}} agent collects logs from a single source located at `/var/log/containers/logger-agent-ds-*.log`. Make sure that you add the desired log source paths to the `Path` parameter for your specific requirements. Separate each path with a comma.
{: important}

Consider the following example in `input-kubernetes.conf` section:

```text
input-kubernetes.conf: |
    [INPUT]
        Name              tail
        Tag               kube.*
        Path              /var/log/containers/logger-agent-ds-*.log,/path/to/your/logs/*.log
        Path_Key          file
```
{: codeblock}

In this example:
- The `/var/log/containers/logger-agent-ds-*.log` path is the default log source.
- Additional log sources can be specified after the comma in the `Path` parameter. For instance, `/path/to/your/logs/*.log` is an additional log source.


## Excluding paths
{: #exclude-paths}

To specify paths to be excluded, do the following:

1. [Download the YAML configuration file for your environment.](/docs/logs-router?topic=logs-router-download-iclr-agent-configuration-file)
2. Open the downloaded `logger-agent.yaml` file in a text editor.
3. Locate the `input-kubernetes.conf` section.
4. Update the `Exclude_Path` parameter to specify the log sources that you want to exclude from collection. This parameter allows you to specify paths that should be ignored by the {{site.data.keyword.logs_routing_full_notm}} agent.

The `Exclude_Path` parameter might not be present by default, so you might need to add it if it does not exist. This parameter lets you to specify the paths that should be ignored by the {{site.data.keyword.logs_routing_full_notm}} agent.
{: note}

Consider the following example with `Exclude_Path` specified:

If your directory structure is:

```text
/path/to/your/logs
                ├── app1.log
                ├── app2.log
                ├── exclude-1.log
                └── exclude-2.log
```
{: screen}

You can modify `input-kubernetes.conf` section as follows:

```text
input-kubernetes.conf: |
    [INPUT]
        Name              tail
        Tag               kube.*
        Path              /var/log/containers/logger-agent-ds-*.log,/path/to/your/logs/*.log
        Path_Key          file
        Exclude_Path      /path/to/your/logs/exclude-1.log,/path/to/your/logs/exclude-2.log
```
{: codeblock}

In this example:
- The `Path` parameter specifies two paths to be included:
    - `/var/log/containers/logger-agent-ds-*.log`
    - `/path/to/your/logs/*.log`

- The `Exclude_Path` parameter is used to specify two additional paths to be excluded:
    - `/path/to/your/logs/exclude-1.log`
    - `/path/to/your/logs/exclude-2.log`

All files within the directory that match the pattern specified in the `Path` parameter will be collected by the {{site.data.keyword.logs_routing_full_notm}} Agent, except for those matching the patterns specified in `Exclude_Path`.
{: note}

For more detailed information on configuring the Input Tail plugin, see the [Fluent Bit documentation for the Input Tail plugin](https://docs.fluentbit.io/manual/pipeline/inputs/tail){: external}.

