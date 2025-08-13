---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Helm Chart configuration options
{: #agent-helm-template-config-options}

Starting with Helm chart version 1.6.0, the Fluent Bit log pipeline configuration has transitioned to using the official [Fluent Bit YAML configuration](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml) format. This change brings enhanced flexibility and clarity to configuration management.


| Parameter | Description | Required | Default value |
|-----------|-------------|---------|----------------|
| `metadata.name` | The name used for all of the Kubernetes resources | Yes | `logs-agent` |
| `image.version` | The version of the agent container image | Yes | No default. Sample value: `1.6.1` |
| `env.ingestionHost` | The {{site.data.keyword.logs_full_notm}} host where logs are sent | Yes | No default |
| `env.ingestionPort` | The {{site.data.keyword.logs_full_notm}} port where logs are sent | Yes | No default |
| `env.iamMode` | Indicate the IAM authentication mechanism used | Yes | No default. Valid values: `TrustedProfile`, `IAMAPIKey` |
| `env.trustedProfileID` | The trusted profile to use | Required when `iamMode=TrustedProfile` | No default. Sample value: `Profile-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` |
| `env.iamEnvironment` | Controls the IAM endpoint used by the agent to exchange the tokens.  \n For more information, see [iamEnvironment](#agent-helm-template-clusters-chart-options-iam-env). | Production |
| `env.iamHost` | IAM host required for IAM Environment `Custom` setting.  See [iamEnvironment](#agent-helm-template-clusters-chart-options-160-iam-env) | required for iamEnvironment `Custom` - no default |
| `secret.iamAPIKey` | The APIKey used when `iamMode=IAMAPIKey`. Should only be provided when using the CLI | optional |
| `clusterName` | The name of the Kubernetes cluster | optional |
| `scc.create` | When to create the Secure Context Constraints in Openshift | false |
| `defaultMetadata.subsystemName` | Static string to override the `subsystemName` in {{site.data.keyword.logs_full_notm}} | Container that generated the log |
| `defaultMetadata.applicationName` | Static string to override the `applicationName` in {{site.data.keyword.logs_full_notm}} | Namespace name that generated the log |
| `excludeLogSourcePaths` | Additional logs that should not be collected by the agent.  \n For more information, see [Log Source Paths configurations](#agent-helm-template-clusters-chart-options-160-log-source-paths). | `/var/log/at/*` |
| `includeAnnotations` | Instruct the Kubernetes plug-in to include the container annotations with the log messages.  \n For more information, see [includeAnnotations]#agent-helm-template-clusters-chart-options-include-annotations). | false |
| `retryLimit` | Limit the number of retries that will be attempted | False - no retry limits |
| `loggingLevel` | The type of logs that should be reported by the agent (`debug`, `info`, `error`) | `info` |
| `keepParsedLogs` | If a log is parsed by the Kubernetes filter, still keep the original `log` field containing the message | false |
| `outputWorkers` | The number of worker threads used by the output plug-in to send to {{site.data.keyword.logs_full_notm}} | 4 |

| `enableKubernetesFilter` | Indicate whether the Kubernetes filter should be used when parsing container logs | true |

| `resources` | Override the Kubernetes resources allocated to the logs-agent | Optional | See [Resources](#agent-helm-template-clusters-chart-options-resources) to see the default values|
| `additionalLogSourcePaths` [Deprecated]{: tag-deprecated} | The path of additional logs beyond the default `/var/log/containers/*.log`.  \n For more information, see [Log Source Paths configurations](#agent-helm-template-clusters-chart-options-log-source-paths). | optional - not set |
| `selectedLogSourcePaths` | Override `/var/log/containers/*.log` and only collect logs in these paths. \n For more information, see [Log Source Paths configurations](#agent-helm-template-clusters-chart-options-160-log-source-paths). | optional - not set |
| `additionalMetadata` | A list of key/value pair tags that can be added as metadata to every log line.  \n For more information, see [additionalMetadata](#agent-helm-template-clusters-deploy-chart-options-additional-metadata). | optional - not set |
| `severityFieldName` | The name of the field to be used to populate the severity field in the log record when a severity field doesn't already exist | optional - not set |
| `tolerations` | The toleration definition for the daemonset in order to run the agent pods on nodes with taints | optional - not set |
| `additionalServiceOptions` | Additional user provided service configurations | optional - not set |
| `additionalKubeLogInputProcessors` | Additional user provided input processors | optional - not set |
| `additionalInputs` | Additional user provided input definitions | optional - not set |
| `additionalFilters` | Additional user provided filter definitions | optional - not set |
| `additionalKubeLogInputProcessors` | Additional input processor for container logs | optional - not set |
| `additionalOutputs` | Additional output definitions | optional - not set |
| `additionalParsers` | Additional parsers | optional - not set |
| `additionalMultilineParsers` | Additional multiline parsers | optional - not set |
| `kubernetesFields` | List of Kubernetes metadata fields to keep in log records | pod_name, namespace_name, container_name |
{: caption="Helm configuration options" caption-side="bottom"}


The following table contains a list of the parameters that you can configure in the `logs-values.yaml` file to adjust the {{site.data.keyword.agent}} configurations:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `metadata.name` | The name used for all of the Kubernetes resources | required - no default |`logs-agent` |
| `image.version` | The version of the agent container image (for example 1.6.0) | required - no default |
| `env.ingestionHost` | The {{site.data.keyword.logs_full_notm}} host where logs are sent | required - no default |
| `env.ingestionPort` | The {{site.data.keyword.logs_full_notm}} port where logs are sent | required - no default |
| `env.iamMode` | Indicate the IAM authentication mechanism used - `TrustedProfile` or `IAMAPIKey` | required - no default |TrustedProfile|
| `env.trustedProfileID` | The trusted profile to use - required when `iamMode=TrustedProfile` | optional |
| `env.iamEnvironment` | Controls the IAM endpoint used by the agent to exchange the tokens.  \n For more information, see [iamEnvironment](#agent-helm-template-clusters-chart-options-iam-env). | Production |
| `env.iamHost` | IAM host required for IAM Environment `Custom` setting.  See [iamEnvironment](#agent-helm-template-clusters-chart-options-160-iam-env) | required for iamEnvironment `Custom` - no default |
| `secret.iamAPIKey` | The APIKey used when `iamMode=IAMAPIKey`. Should only be provided when using the CLI | optional |
| `clusterName` | The name of the Kubernetes cluster | optional |
| `scc.create` | When to create the Secure Context Constraints in Openshift | false |
| `defaultMetadata.subsystemName` | Static string to override the `subsystemName` in {{site.data.keyword.logs_full_notm}} | Container that generated the log |
| `defaultMetadata.applicationName` | Static string to override the `applicationName` in {{site.data.keyword.logs_full_notm}} | Namespace name that generated the log |
| `resources` | Override the Kubernetes resources allocated to the logs-agent | Optional | See [Resources](#agent-helm-template-clusters-chart-options-resources) to see the default values|
| `additionalLogSourcePaths` [Deprecated]{: tag-deprecated} | The path of additional logs beyond the default `/var/log/containers/*.log`.  \n For more information, see [Log Source Paths configurations](#agent-helm-template-clusters-chart-options-log-source-paths). | optional - not set |
| `excludeLogSourcePaths` | Additional logs that should not be collected by the agent.  \n For more information, see [Log Source Paths configurations](#agent-helm-template-clusters-chart-options-160-log-source-paths). | `/var/log/at/*` |
| `selectedLogSourcePaths` | Override `/var/log/containers/*.log` and only collect logs in these paths. \n For more information, see [Log Source Paths configurations](#agent-helm-template-clusters-chart-options-160-log-source-paths). | optional - not set |
| `includeAnnotations` | Instruct the Kubernetes plug-in to include the container annotations with the log messages.  \n For more information, see [includeAnnotations]#agent-helm-template-clusters-chart-options-include-annotations). | false |
| `retryLimit` | Limit the number of retries that will be attempted | False - no retry limits |
| `loggingLevel` | The type of logs that should be reported by the agent (`debug`, `info`, `error`) | `info` |
| `additionalMetadata` | A list of key/value pair tags that can be added as metadata to every log line.  \n For more information, see [additionalMetadata](#agent-helm-template-clusters-deploy-chart-options-additional-metadata). | optional - not set |
| `keepParsedLogs` | If a log is parsed by the Kubernetes filter, still keep the original `log` field containing the message | false |
| `outputWorkers` | The number of worker threads used by the output plug-in to send to {{site.data.keyword.logs_full_notm}} | 4 |
| `severityFieldName` | The name of the field to be used to populate the severity field in the log record when a severity field doesn't already exist | optional - not set |
| `tolerations` | The toleration definition for the daemonset in order to run the agent pods on nodes with taints | optional - not set |
| `enableKubernetesFilter` | Indicate whether the Kubernetes filter should be used when parsing container logs | true |
| `additionalServiceOptions` | Additional user provided service configurations | optional - not set |
| `additionalKubeLogInputProcessors` | Additional user provided input processors | optional - not set |
| `additionalInputs` | Additional user provided input definitions | optional - not set |
| `additionalFilters` | Additional user provided filter definitions | optional - not set |
| `additionalKubeLogInputProcessors` | Additional input processor for container logs | optional - not set |
| `additionalOutputs` | Additional output definitions | optional - not set |
| `additionalParsers` | Additional parsers | optional - not set |
| `additionalMultilineParsers` | Additional multiline parsers | optional - not set |
| `kubernetesFields` | List of Kubernetes metadata fields to keep in log records | pod_name, namespace_name, container_name |
{: caption="Helm configuration options" caption-side="bottom"}

## `env.iamMode`
{: #agent-helm-template-clusters-chart-options-160-iammode}

Configure this parameter to choose the authentication method to use by the agent when sending logs to an {{site.data.keyword.logs_full_notm}} instance.

- You can choose an IAM APIKey or a Trusted Profile configuration.
- Valid values are: `TrustedProfile` or `IAMAPIKey`
- The default value is a Trusted Profile configuration.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
env:
  iamMode: IAMAPIKey
```
{: codeblock}

Consider the following information when setting this parameter:

- If `env.iamMode: "TrustedProfile"` is set, then the `env.trustedProfileID` variable must also be provided.

- If `env.iamMode: "IAMAPIKey"` is set, then the configuration expects a secret to be defined that contains an IAM Apikey with permissions.

    If the `secret.iamAPIKey` variable is provided on the helm command (for example `--set secret.iamAPIKey=<your iamAPIKey>`), then the helm chart will create the Kubernetes secret.

    Alternatively, you can create the secret ahead of time with the command: (Make sure you are connected to your cluster.)

    ```sh
    kubectl create secret generic <helm install-name> -n ibm-observe --from-literal=IAM_API_KEY=<apikey>
    ```
    {: codeblock}



## `defaultMetadata`
{: #agent-helm-template-clusters-chart-options-160-defaultmetadata}

This section allows the user to override the default `subsystemName` and `applicationName` that are used in the environment.
By default, the values are not set and the output plug-in will dynamically set the values to:

- `applicationName`: the Kubernetes namespace that generated the log
- `subsystemName`: the container name that generated the log

The entry in the `logs-values.yaml` file looks as follows:

```yaml
defaultMetadata:
  subsystemName: ""
  applicationName: ""
```
{: codeblock}

## `resources`
{: #agent-helm-template-clusters-chart-options-160-resources}

This section allows the user to change the resources that are assigned to the {{site.data.keyword.agent}} container.

The entry in the `logs-values.yaml` file looks as follows and sets the following default values:

```yaml
resources:
  limits:
    cpu: 500m
    ephemeral_storage: 10Gi
    memory: 3Gi
  requests:
    cpu: 100m
    ephemeral_storage: 2Gi
    memory: 1Gi
```
{: codeblock}

If you need to update any of the values, the entire configuration must be provided even if you don't update all of the values.
{: important}

## Log source paths configurations
{: #agent-helm-template-clusters-chart-options-160-log-source-paths}

By default the agent will collect the logs from `/var/log/containers/*.log`.
{: note}

The following additional variables can be provided to include, exclude or restrict the set of logs to be processed:
- `additionalLogSourcePaths` adds locations to the default set of logs that will be processed.
- `excludeLogSourcePaths` overrides the default path of `/var/log/at/*` and ignores logs in the specified locations.
- `selectedLogSourcePaths` overrides the default path `/var/log/containers/*.log` and ignores the `additionalLogSourcePaths` configurations. Only the files that are set through this parameter are collected by the agent.

You can define multiple paths by using a comma separated list, for example `/var/log/abc/*.log,/var/log/xyz/*.log`.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
# comma separated list, for example “/var/log/abc/*.log,/var/log/xyz/*.log”
additionalLogSourcePaths: ""
excludeLogSourcePaths: ""
selectedLogSourcePaths: ""
```
{: codeblock}

## `env.iamEnvironment`
{: #agent-helm-template-clusters-chart-options-160-iam-env}

This configuration controls the IAM endpoint used by the agent to exchange the tokens.

The default value is `Production`.

Valid values are :
- Set `Production` to use the `iam.cloud.ibm.com` default endpoint
- Set `PrivateProduction` to use the `private.iam.cloud.ibm.com` endpoint
- Set `Custom` to use a custom IAM endpoint (for example `private.eu-de.iam.cloud.ibm.com`)

The entry in the `logs-values.yaml` file looks as follows:

```yaml
env:
  iamEnvironment: "Production"
```
{: codeblock}

For the `Custom` `iamEnvironment` setting, the `iamHost` must also be provided.
```yaml
env:
  iamEnvironment: "Custom"
  iamHost: "private.eu-de.iam.cloud.ibm.com"
```
{: codeblock}

## `includeAnnotations`
{: #agent-helm-template-clusters-chart-options-160-include-annotations}

This configuration changes the setting for the Kubernetes filter to include the annotations from Kubernetes with the log records.

The default value for this setting is `false`.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
includeAnnotations: true
```
{: codeblock}

## `retryLimit`
{: #agent-helm-template-clusters-chart-options-160-retrylimit}

This configuration places a limit on the number of times the agent will retry sending data if an error occurs that is considered to be retryable.

The default is `False`.

For more information, see the [Fluentbit documentation about retries](https://docs.fluentbit.io/manual/administration/scheduling-and-retries) to understand the implications of setting this value.

In some situations this setting could lead to log data being discarded by the agent due to the inability to send.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
retryLimit: 8
```
{: codeblock}

## `additionalMetadata`
{: #agent-helm-template-clusters-deploy-chart-options-additional-metadata}

This is a list of key/value pairs that will be added under the `meta` object to permit additional tags.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
additionalMetadata:
  region: ca-tor
  env: production
```
{: codeblock}

The previous example will result in the following additional fields added to each log line in {{site.data.keyword.logs_full_notm}}:

```json
{
  "meta": {
    "region": "ca-tor",
    "env": "production"
  }
}
```
{: codeblock}

## `keepParsedLogs`
{: #keepParsedLogs}

This is a boolean flag that determines whether to retain the original log field after it has been successfully processed by the Kubernetes plug-in.

The default is `false`.

Enabling this will result in duplicate log data, which may increase storage usage.
{: note}

Example configuration:

```yaml
keepParsedLogs: true
```
{: codeblock}

## `outputWorkers`
{: #outputWorkers}

This setting defines the number of worker threads used by the output plug-in to enable parallel processing of log data.

The default is  `4`.

In most environments, increasing the number of threads beyond 4 does not significantly impact performance. If your log volume is high and you’ve allocated more than 1 CPU, increasing this value to 8 can help improve output throughput.

For low-volume enviroments, reducing this value to 1 or 2 will limit the maximum log volume that can be sent to {{site.data.keyword.logs_full_notm}}, which may be suitable for smaller workloads.

```yaml
outputWorkers: 2
```
{: codeblock}

## `severityFieldName`
{: #severityFieldName}

This is an optional setting that allows you to override the default severity field sent to {{site.data.keyword.logs_full_notm}}.
Use this option if your log messages use a non-standard field name (for example, `Log_Level`, `logSeverity`, and so on) to indicate severity.

When configured:
- A new filter is added to the pipeline.
- This filter injects a severity field into each log record.
- The value of severity is populated from the custom field you specify.

```yaml
severityFieldName: Log_Level
```
{: codeblock}

## `tolerations`
{: #tolerations}

In some Kubernetes environments, nodes may have taints that prevent the Fluent Bit agent from being scheduled. To ensure the agent can run on these nodes, you must define appropriate tolerations in your Helm chart configuration.
Refer to the [Kubernetes documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} about taints and tolerations for more information.

For example, if you have a taint on a node:

`kubectl taint nodes 10.1.2.3 myNodeType=ingress:NoSchedule`

You can allow the agent to be scheduled on that node by adding this configuration to your `values.yaml` file:

```yaml
tolerations:
  - effect: NoSchedule
    key: myNodeType
    value: ingress
    operator: Equal
```
{: codeblock}

- These fields are directly added to the DaemonSet's tolerations section.
- This ensures the agent respects the taint rules and can be scheduled accordingly.

## `enableKubernetesFilter`
{: #enableKubernetesFilter}

By default the Helm chart enables the Kubernetes filter for processing the container logs.  This provides capabilities such as:

- Enriching the log lines with metadata about the running container.
- Invoking another parser after the CRI parser to further process the log data.
- Using annotations to choose a secondary parser.

If you do not wish to use these features, then they can be disabled with this option.

```yaml
enableKubernetesFilter: false
```
{: codeblock}

## `systemLogs`
{: #systemLogs}

If you want to process files from a path other than `/var/log/containers` (for example, `/var/log/syslog` or `/var/log/kubelet.log`), then use the `systemLogs` setting to enable the processing for these files.

You can use the `systemLogsParser` option in order to consider a different parser - by default the `kube_syslog` parser is used which is appropriate for newer VPC-based systems.  Some of the classic Kubernetes clusters may require the `systemLogsParser` to be set to `kube_syslog_classic` in order to match the timestamp format on those systems.

```yaml
systemLogs:
  - /var/log/kube-proxy.log
  - /var/log/kubelet.log
```
{: codeblock}

## `additionalServiceOptions`
{: #additionalServiceOptioners}

This option can be used to add configuration options to the `service` section of the Fluent Bit configuration. This will add entries to the [service](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/service-section) section of the Fluent Bit yaml configuration.

```yaml
additionalServiceOptions:
  storage.backlog.mem_limit: 5G
```
{: codeblock}

## `additionalKubeLogInputProcessors`
{: #additionalKubeLogInputProcessors}

This option allows the user to introduce additional processors for their container logs after the normal processing has completed.  This may be useful for example, to introduce an additional parser within the processor pipeline. This will add entries to the [pipeline.inputs.processors](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/pipeline-section) section of the Fluent Bit yaml configuration.

```yaml
additionalKubeLogInputProcessors:
  - name: parser
    parser: json
    key_name: log
    reserve_data: true
```
{: codeblock}

## `additionalInputs`
{: #additionalInputs}

This option allows the user to introduce additional Fluent Bit input plug-in definitions to the current pipeline. This could be, for example, another file with special parsing requirements or other input plug-ins.

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
```
{: codeblock}

### `additionalFilters`
{: #additionalFilters}

There might be some filters that should be applied to both containers and host logs - rather than including in the `additionalKubeLogInputProcessors` and `additionalSystemLogsInputProcessors`. This will add entries to the [pipeline.filters](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/pipeline-section) section of the Fluent Bit yaml configuration.

```yaml
additionalFilters:
  - name: modify
    match: '*'
    set:
      - deployment_env pre-production
```
{: codeblock}

## `additionalOutputs`
{: #additionalOutputs}

In the event that the logs should be sent to another output location, the user can introduce additional output sections in order to send to a second {{site.data.keyword.logs_full_notm}} instance. This will add entries to the [pipeline.outputs](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/pipeline-section) section of the Fluent Bit yaml configuration.

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

## `additionalParsers`
{: #additionalParsers}

If you need to introduce a new parser, this option allows you to introduce your own parsers. If you need to introduce a new parser, this option allows you to introduce your own parsers. This will add entries to the [parsers](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/parsers-section] section of the Fluent Bit yaml configuration.

```yaml
additionalParsers:
  - name: json_raw
    format: json
```
{: codeblock}

## `additionalMultilineParsers`
{: #additionalMultilineParsers}

If you need to introduce a new multiline parser, this option allows you to introduce your own multiline parsers. This will add entries to the [multiline_parsers](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml/multiline-parsers-section) section of the Fluent Bit yaml configuration.

```yaml
additionalMultilineParsers:
  - name: multiline_sample
    type: regex
    flush_timeout: 1000
    rules:
      - state: start_state
        regex: '/^\[\d+\/\d+\/\d+,.*$/'
        next_state: cont
      - state: cont
        regex: '/^[^\[].*$/'
        next_state: cont
      - state: cont
        regex: '/^$/'
        next_state: cont
```
{: screen}

## `kubernetesFields`
{: #kubernetesFields}

This configuration allows controlling which Kubernetes metadata fields are included with each log record. By default, only essential fields such as `pod_name`, `namespace_name`, and `container_name` are kept. This helps reduce the amount of metadata stored with each log and reduces storage costs.

The following fields can be included by uncommenting them or adding them to the list:
- `pod_name`
- `namespace_name`
- `container_name`
- `pod_ip`
- `pod_id`
- `container_hash`
- `container_image`
- `docker_id`
- `host`

**Note:** The following fields are included in the Kubernetes metadata based on other settings:
- `cluster_name` - Included when the `clusterName` is provided.
- `labels` - Included by default unless `includeLabels` is set to `false`.
- `annotations` - Included when `includeAnnotations` is set to `true`.

Example configuration to keep only the essential fields:

```yaml
kubernetesFields:
  - pod_name
  - namespace_name
  - container_name
```
{: codeblock}

Example configuration for including additional fields for more detailed metadata:

```yaml
kubernetesFields:
  - pod_name
  - namespace_name
  - container_name
  - pod_ip
  - container_image
  - host
```
{: codeblock}
