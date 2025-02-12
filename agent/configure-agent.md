---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring whether logs are included or excluded
{: #configure-include-exclude}

You can specify whether logs are included or excluded from collection based on a configured path or file name.
{: shortdesc}

## Including paths
{: #include-paths}

To specify included paths, complete the following steps:

1. Log in to the cluster. For more information, see [Access your cluster](/docs/containers?topic=containers-access_cluster).

2. In the {{site.data.keyword.agent}} configmap, locate the `input-kubernetes.conf` section. Then, update the `Path` parameter to specify the log sources that you want to collect.

    By default, the {{site.data.keyword.agent}} collects logs from a single source located at `/var/log/containers/`. Make sure that you add the desired log source paths to the `Path` parameter for your specific requirements. Separate each path with a comma.
    {: important}

    ```yaml
    input-kubernetes.conf: |
    [INPUT]
        Name              tail
        Tag               kube.*
        Path              /var/log/containers/*.log,/path/to/your/logs/*.log
        Path_Key          file
    ```
    {: codeblock}

    Additional log sources can be specified and separated by commas in the `Path` parameter.

    
    {{../_include-segments/kube-config.md}}

3. Restart the agent pods.

    For Kubernetes clusters, run:

    ```sh
    kubectl -n ibm-observe rollout restart ds/logs-agent
    ```
    {: pre}

    For OpenShift clusters, run:

    ```sh
    oc -n ibm-observe rollout restart ds/logs-agent
    ```
    {: pre}



## Excluding paths
{: #exclude-paths}

To specify paths to be excluded, complete the following steps:

1. Log in to the cluster. For more information, see [Access your cluster](/docs/containers?topic=containers-access_cluster).

2. In the {{site.data.keyword.agent}} configmap, locate the `input-kubernetes.conf` section. Then, update the `Exclude_Path` parameter to specify the log sources that you want to exclude from collection. This parameter allows you to specify paths that should be ignored by the {{site.data.keyword.agent}}.

    The `Exclude_Path` parameter might not be present by default, so you might need to add it if it does not exist. This parameter lets you to specify the paths that should be ignored by the {{site.data.keyword.agent}}.
    {: note}

    ```yaml
    input-kubernetes.conf: |
    [INPUT]
        Name              tail
        Tag               kube.*
        Path              /var/log/containers/logger-agent-ds-*.log,/path/to/your/logs/*.log
        Path_Key          file
        Exclude_Path      /path/to/your/logs/exclude-1.log,/path/to/your/logs/exclude-2.log
    ```
    {: codeblock}

    Additional log sources can be specified and separated by commas in the `Exclude_Path` parameter.

3. Restart the agent pods.

    For Kubernetes clusters, run:

    ```sh
    kubectl -n ibm-observe rollout restart ds/logs-agent
    ```
    {: pre}

    For OpenShift clusters, run:

    ```sh
    oc -n ibm-observe rollout restart ds/logs-agent
    ```
    {: pre}



## Sample
{: #configure-include-exclude-sample}

Consider the following example with `Exclude_Path` specified:

For example, if your directory structure is:

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

All files within the directory that match the pattern specified in the `Path` parameter will be collected by the {{site.data.keyword.agent}}, except for those matching the patterns specified in `Exclude_Path`.
{: note}
