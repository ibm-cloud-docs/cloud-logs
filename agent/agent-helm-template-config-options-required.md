---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Helm Chart configuration required
{: #agent-helm-template-config-options-required}

Starting with Helm chart version 1.6.0, the Fluent Bit log pipeline configuration has transitioned to using the official [Fluent Bit YAML configuration](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml) format. This change brings enhanced flexibility and clarity to configuration management.


The following table contains a list of the parameters that are required and you can customize in the `logs-values.yaml` file:

| Parameter | Description | Default value |
|-----------|-------------|----------------|
| `metadata.name` | The name used for all of the Kubernetes resources | `logs-agent` |
| `image.version` | The version of the agent container image | No default. \n Sample value: `1.6.1` |
| `clusterName` | The name of the Kubernetes cluster | No default \n Enter your cluster name |
| `loggingLevel` | The type of logs that should be reported by the agent (`debug`, `info`, `error`) | `info` |
| `retryLimit` | Limit the number of retries that will be attempted to send data to {{site.data.keyword.logs_full_notm}} \n Set to `False` so there are no retry limits | `False` |
| `outputWorkers` | The number of worker threads used by the output plug-in to send data to {{site.data.keyword.logs_full_notm}} | `4` |
| `env.ingestionHost` | The {{site.data.keyword.logs_full_notm}} host where logs are sent | No default |
| `env.ingestionPort` | The {{site.data.keyword.logs_full_notm}} port where logs are sent | No default |
| `env.iamMode` | Indicate the IAM authentication mechanism used \n Valid values are: `TrustedProfile`, `IAMAPIKey` | No default  |
| `env.trustedProfileID` | The trusted profile used \n Required when `iamMode=TrustedProfile` | No default. \n Sample value: `Profile-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` |
| `secret.iamAPIKey` | The APIKey used \n Required when `iamMode=IAMAPIKey`. \n Should only be provided when using the CLI | No default |
| `env.iamEnvironment` | Controls the IAM endpoint used by the agent to exchange the tokens. \n Valid values are: `Production`, `Custom`, `PrivateProduction` | `Production` |
| `env.iamHost` | IAM host required for IAM Environment `Custom` setting.  See [iamEnvironment](#agent-helm-template-clusters-chart-options-160-iam-env) | No default |
| `scc.create` | Required to create the Secure Context Constraints in Openshift \n Set to `true` for Openshift clusters. | `false` |
| `defaultMetadata.subsystemName` | Static string to override the `subsystemName` `in {{site.data.keyword.logs_full_notm}} | Set to the container that generated the log |
| `defaultMetadata.applicationName` | Static string to override the `applicationName` in {{site.data.keyword.logs_full_notm}} | Set to the namespace name that generated the log |
| `selectedLogSourcePaths` | Logs that should be collected by the agent. | `/var/log/containers/*.log` |
| `excludeLogSourcePaths` | Logs that should NOT be collected by the agent. | `/var/log/at/*` |
| `keepParsedLog` | If a log is parsed by the Kubernetes filter, still keep the original log field containing the message | `false` |
| `enableKubernetesFilter` | Indicate whether the Kubernetes filter should be used when parsing container logs | `true` |
| `kubernetesFields` | List of Kubernetes metadata fields to keep in log records | `pod_name`, `namespace_name`, `container_name` |
| `includeAnnotations` | Instruct the Kubernetes plug-in to include the container annotations with the log messages.  \n For more information, see [includeAnnotations]#agent-helm-template-clusters-chart-options-include-annotations). | `false` |
| `includeLabels` | Instruct the Kubernetes plug-in to include labels. | `false` |
{: caption="Helm configuration options" caption-side="bottom"}


## Sample logs-values.yaml file
{: #agent-helm-template-config-options-required-sample}

The following sample of the `logs-values.yaml` file includes default values:

```yaml
metadata:
  name: "logs-agent"
image:
  version: "1.6.1"

clusterName: "ENTER_CLUSTER_NAME"     # Enter the name of your cluster. This information is used to improve the metadata and help with your filtering.

enableKubernetesFilter: true
loggingLevel: "info"
retryLimit: false
outputWorkers: 4

#defaultMetadata:
#  subsystemName: ""
#  applicationName: ""

# Add additional metadata
#additionalMetadata:
#  region: us-south
#  env: prod

selectedLogSourcePaths: ""  # Comma separated list. Adds log files to the default value `/var/log/containers/*.log`
excludeLogSourcePaths: ""   # Comma separated list. Adds log files to the default value `/var/log/at/*`

enableKubernetesFilter: true
includeAnnotations: false
includeLabels: false
kubernetesFields:
  - pod_name
  - namespace_name
  - container_name
#  - pod_id
#  - pod_ip
#  - container_hash
#  - container_image
#  - docker_id
#  - host

env:
  # ingestionHost is a required field. For example:
  ingestionHost: "<logs instance>.ingress.us-east.logs.cloud.ibm.com"

  # If you are using private CSE proxy, then use port number "3443"
  # If you are using private VPE Gateway, then use port number "443"
  # If you are using the public endpoint, then use port number "443"
  ingestionPort: "443"

  iamMode: "TrustedProfile"
  # trustedProfileID - trusted profile id - required for iam trusted profile mode
  trustedProfileID: "Profile-yyyyyyyy-xxxx-xxxx-yyyy-zzzzzzzzzzzz" # required if iamMode is set to TrustedProfile

  iamEnvironment: "Production"

scc:
  # Set to true to create the Security Context Constraints in Openshift clusters
  create: false
```
{: codeblock}



## Configure the IAM endpoint
{: #agent-helm-template-config-options-required-1}

Set `env.iamEnvironment` to control the IAM endpoint that is used by the agent to exchange the tokens.

The default value is `Production`.

Valid values are:
- Set `Production` to use the `iam.cloud.ibm.com` default endpoint

    Sample `logs-values.yaml` file looks as follows:

    ```yaml
    env:
      iamEnvironment: "Production"
    ```
    {: codeblock}

- Set `PrivateProduction` to use the `private.iam.cloud.ibm.com` endpoint

    Sample `logs-values.yaml` file looks as follows:

    ```yaml
    env:
      iamEnvironment: "PrivateProduction"
    ```
    {: codeblock}

- Set `Custom` to use a custom IAM endpoint (for example `private.eu-de.iam.cloud.ibm.com`). You must also set `env.iamHost`.

    Sample `logs-values.yaml` file looks as follows:

    ```yaml
    env:
      iamEnvironment: "Custom"
      iamHost: "private.eu-de.iam.cloud.ibm.com"
    ```
    {: codeblock}



## Configure the authenticaion method
{: #agent-helm-template-config-options-required-2}

Configure `env.iamMode` to choose the authentication method to use by the agent when sending logs to an {{site.data.keyword.logs_full_notm}} instance.

You can choose an IAM APIKey or a Trusted Profile configuration.

Valid values are:
- `TrustedProfile`

    Sample `logs-values.yaml` file looks as follows:

    ```yaml
    env:
      iamMode: "TrustedProfile"
      trustedProfileID: "Profile-yyyyyyyy-xxxx-xxxx-yyyy-zzzzzzzzzzzz"
    ```
    {: codeblock}

- `IAMAPIKey`

    Sample `logs-values.yaml` file looks as follows:

    ```yaml
    env:
      iamMode: "IAMAPIKey"
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



## Configure custom values for applicationName and subsystemName
{: #agent-helm-template-config-options-required-3}

You can configure the `defaultMetadata` section to override the default `subsystemName` and `applicationName` that are used in the environment.

The default value is set by the output plug-in dynamically as follows

- `applicationName`: the Kubernetes namespace that generated the log
- `subsystemName`: the container name that generated the log

The entry in the `logs-values.yaml` file looks as follows:

```yaml
defaultMetadata:
  subsystemName: ""
  applicationName: ""
```
{: codeblock}

## Configure custom tags
{: #agent-helm-template-config-options-required-4}

You can configure the `additionalMetadata` section to add additional tags.

A tag is a key/value pair that will be added under the `meta` object in each log record.

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

## Configure the number of retries sending data if an error occurs
{: #agent-helm-template-config-options-required-5}

In FluentBit, the scheduler provides a configuration option called `Retry_Limit`. It is set independently for each output section.
The `retryLimit` configuration places a limit on the number of times the agent will retry sending data if an error occurs that is considered to be retryable.

You can set `retryLimit` to:
- `false` to indicate that there is no limit for the number of retries that the scheduler can do. This is the default value.

    The entry in the `logs-values.yaml` file looks as follows:

    ```yaml
    retryLimit: false
    ```
    {: codeblock}

- An integer N value greater or equal to 1.

    The entry in the `logs-values.yaml` file looks as follows:

    ```yaml
    retryLimit: 8
    ```
    {: codeblock}

- *no_retries* to indicate that data is not sent to the destination if it failed the first time.

    The entry in the `logs-values.yaml` file looks as follows:

    ```yaml
    retryLimit: "no_retries"
    ```
    {: codeblock}

For more information, see the [Fluentbit documentation about retries](https://docs.fluentbit.io/manual/administration/scheduling-and-retries) to understand the implications of setting this value.

In some situations, this setting could lead to log data being discarded by the agent due to the inability to send.

## Change the resources that are assigned to the {{site.data.keyword.agent}} container
{: #agent-helm-template-config-options-required-6}

If you need to update any of the values, the entire configuration must be provided even if you don't update all of the values.
{: important}

You can configure the `resources` section to change the resources that are assigned to the {{site.data.keyword.agent}} container.

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

## `outputWorkers`
{: #agent-helm-template-config-options-required-7}

This setting defines the number of worker threads used by the output plug-in to enable parallel processing of log data.

The default is  `4`.

In most environments, increasing the number of threads beyond 4 does not significantly impact performance. If your log volume is high and you’ve allocated more than 1 CPU, increasing this value to 8 can help improve output throughput.

For low-volume enviroments, reducing this value to 1 or 2 will limit the maximum log volume that can be sent to {{site.data.keyword.logs_full_notm}}, which may be suitable for smaller workloads.

```yaml
outputWorkers: 2
```
{: codeblock}

## `severityFieldName`
{: #agent-helm-template-config-options-required-8}

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
{: #agent-helm-template-config-options-required-9}

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

## Configure the log files that are collected by the agent
{: #agent-helm-template-config-options-required-10}

By default the agent will collect the logs from `/var/log/containers/*.log` and ignore `/var/log/at/*`.
{: note}

The following additional variables can be provided to include and exclude the set of logs to be processed by the agent:
- `excludeLogSourcePaths`: List of files that the agent is configured to ignore. The defailt value is set to ignore `/var/log/at/*`
- `selectedLogSourcePaths`: List of files that the agent collects and sends to {{site.data.keyword.logs_full_notm}}. The default value is set to `/var/log/containers/*.log`. You can define multiple paths by using a comma separated list, for example `/var/log/abc/*.log,/var/log/xyz/*.log`.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
# comma separated list, for example “/var/log/abc/*.log,/var/log/xyz/*.log”
excludeLogSourcePaths: ""
selectedLogSourcePaths: ""
```
{: codeblock}


## Configure the system component logs that are collected by the agent
{: #agent-helm-template-config-options-required-11}

System component logs record events that happen in the cluster. There are two types of system components: system components that run in a container and system components directly involved in running containers. For example, the kubelet and container runtime do not run in containers. The Kubernetes scheduler, controller manager, and API server run within pods. If your cluster uses kube-proxy, you typically run this as a DaemonSet.

Use the `systemLogs` setting to enable the processing of system component logs that are located in the `/var/log` directory. System logs in `/var/log/containers/` are collected automatically unless you exclude them in the `excludeLogSourcePaths` section.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
systemLogs:
  - /var/log/kube-apiserver.log. # Logs generated by the API server.
  - /var/log/kube-scheduler.log # Logs generated by the scheduler. This component is responsible for making scheduling decisions.
  - /var/log/kube-controller-manager.log # Logs generated by the Kube controller manager that runs most Kubernetes built-in controllers.
  - /var/log/kube-proxy.log  # Logs generated by the kube-proxy. This component is responsible for directing traffic to Service endpoints.
  - /var/log/kubelet.log  # Logs generated by the kubelet. This component is responsible for running containers on the node.
  - /var/log/syslog
```
{: codeblock}


By default, the `kube_syslog` parser is used which is appropriate for newer VPC-based systems.

Some of the classic Kubernetes clusters may require the `systemLogsParser` to be set to `kube_syslog_classic` in order to match the timestamp format on those systems. You can use the `systemLogsParser` option in order to consider a different parser.  The entry in the `logs-values.yaml` file looks as follows:

```yaml
systemLogsParser: "kube_syslog_classic"
systemLogs:
  - /var/log/syslog
```
{: codeblock}




## `keepParsedLog`
{: #agent-helm-template-config-options-required-12}

This is a boolean flag that determines whether to retain the original log field after it has been successfully processed by the Kubernetes plug-in.

The default is `false`.

Enabling this will result in duplicate log data, which may increase storage usage.
{: note}

Example configuration:

```yaml
keepParsedLog: true
```
{: codeblock}


## `enableKubernetesFilter`
{: #agent-helm-template-config-options-required-13}

By default, the Helm chart enables the Kubernetes filter for processing the container logs.  This provides capabilities such as:

- Enriching the log lines with metadata about the running container.
- Invoking another parser after the CRI parser to further process the log data.
- Using annotations to choose a secondary parser.

If you do not wish to use these features, then they can be disabled with this option.

```yaml
enableKubernetesFilter: false
```
{: codeblock}


## Customize the Kubernetes metadata fields nincluded with each log record
{: #kubernetesFields}

Youc an configure `kubernetesFields`This configuration allows controlling which Kubernetes metadata fields are included with each log record. By default, only essential fields such as `pod_name`, `namespace_name`, and `container_name` are kept. This helps reduce the amount of metadata stored with each log and reduces storage costs.

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
#  - pod_id
#  - pod_ip
#  - container_hash
#  - container_image
#  - docker_id
#  - host
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
