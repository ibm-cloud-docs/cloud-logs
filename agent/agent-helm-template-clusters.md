---

copyright:
  years:  2024
lastupdated: "2024-12-10"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Template to deploy the {{site.data.keyword.agent}} using a Helm chart
{: #agent-helm-template-clusters}

You can use a Helm chart to deploy the {{site.data.keyword.agent}} to collect and route infrastructure and application logs from an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster or a Kubernetes cluster to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}


## Template to deploy the {{site.data.keyword.agent}} using a Helm chart on an Openshift cluster
{: #agent-helm-template-os-clusters-template}

```yaml
metadata:
  name: "logs-agent"
image:
  version: "1.3.0"  # required

clusterName: ""     # Enter the name of your cluster. This information is used to improve the metadata and help with your filtering.

env:
  # ingestionHost is a required field. For example:
  # ingestionHost: "<logs instance>.ingress.us-east.logs.cloud.ibm.com"
  ingestionHost: "" # required

  # If you are using private CSE proxy, then use port number "3443"
  # If you are using private VPE Gateway, then use port number "443"
  # If you are using the public endpoint, then use port number "443"
  ingestionPort: "" # required

  iamMode: "TrustedProfile"
  # trustedProfileID - trusted profile id - required for iam trusted profile mode
  trustedProfileID: "" # required if iamMode is set to TrustedProfile

scc:
  # true enables creation of Security Context Constraints in Openshift clusters
  create: true

defaultMetadata:
  # Configure to override the default subsystemName and applicationName that are used in the environment.
  subsystemName: ""  # The default value is set to the namespace that generated the log
  applicationName: ""  # The default value is set to the container name that generated the log

resources:
  # Configure this section to change the resources that are assigned to the agent container.
  limits:
    cpu: 500m
    ephemeral_storage: 10Gi
    memory: 3Gi
  requests:
    cpu: 100m
    ephemeral_storage: 2Gi
    memory: 1Gi

# Configure these parameters to include, exclude or restrict the set of logs that are processed by the agent
# By default, the agent will collect the logs from `/var/log/containers/*.log`.
# Each field is set as comma separated list, for example “/var/log/abc/*.log,/var/log/xyz/*.log”
additionalLogSourcePaths: "" # adds locations to the default set of logs that will be processed.
excludeLogSourcePaths: "" # ignores logs in the specified locations.
selectedLogSourcePaths: ""  # overrides the default path `/var/log/containers/*.log` and ignores the `additionalLogSourcePaths` configurations

# Configure this parameter to control the IAM endpoint used by the agent to exchange the tokens.
# The default value is `Production`.
# Valid values are :
# Set `Production` to use the iam.cloud.ibm.com default endpoint
# Set ProductionPrivate to use the private.iam.cloud.ibm.com endpoint
iamEnvironment: "Production"

# Configure this parameter to change the setting for the Kubernetes filter to include the annotations from Kubernetes with the log records.
# The default value for this setting is `false`.
includeAnnotations: true

# Configure this parameter to control the number of times the agent will retry sending data if an error occurs that is considered to be retryable.
# The default is `False`.
# For more information, see the [Fluentbit documentation about retries](https://docs.fluentbit.io/manual/administration/scheduling-and-retries) to understand the implications of setting this value.
retryLimit: False

# Configure additional tags as key/value pair tags that can be added as metadata to every log line.
additionalMetadata:
#  region: ca-tor
#  env: production

# Configure the level of logging
# Default value is info
# Valid values are: debug, info, or error
loggingLevel: info

```
{: codeblock}



## Template to deploy the {{site.data.keyword.agent}} using a Helm chart on a Kubernetes cluster
{: #agent-helm-template-kube-clusters-template}

```yaml
metadata:
  name: "logs-agent"
image:
  version: "1.3.0"  # required

clusterName: ""     # Enter the name of your cluster. This information is used to improve the metadata and help with your filtering.

env:
  # ingestionHost is a required field. For example:
  # ingestionHost: "<logs instance>.ingress.us-east.logs.cloud.ibm.com"
  ingestionHost: "" # required

  # If you are using private CSE proxy, then use port number "3443"
  # If you are using private VPE Gateway, then use port number "443"
  # If you are using the public endpoint, then use port number "443"
  ingestionPort: "" # required

  iamMode: "TrustedProfile"
  # trustedProfileID - trusted profile id - required for iam trusted profile mode
  trustedProfileID: "" # required if iamMode is set to TrustedProfile

scc:
  # true enables creation of Security Context Constraints in Openshift clusters
  # set to false for Kubernetes clusters
  create: false

defaultMetadata:
  # Configure to override the default subsystemName and applicationName that are used in the environment.
  subsystemName: ""  # The default value is set to the namespace that generated the log
  applicationName: ""  # The default value is set to the container name that generated the log

resources:
  # Configure this section to change the resources that are assigned to the agent container.
  limits:
    cpu: 500m
    ephemeral_storage: 10Gi
    memory: 3Gi
  requests:
    cpu: 100m
    ephemeral_storage: 2Gi
    memory: 1Gi

# Configure these parameters to include, exclude or restrict the set of logs that are processed by the agent
# By default, the agent will collect the logs from `/var/log/containers/*.log`.
# Each field is set as comma separated list, for example “/var/log/abc/*.log,/var/log/xyz/*.log”
additionalLogSourcePaths: "" # adds locations to the default set of logs that will be processed.
excludeLogSourcePaths: "" # ignores logs in the specified locations.
selectedLogSourcePaths: ""  # overrides the default path `/var/log/containers/*.log` and ignores the `additionalLogSourcePaths` configurations

# Configure this parameter to control the IAM endpoint used by the agent to exchange the tokens.
# The default value is `Production`.
# Valid values are :
# Set `Production` to use the iam.cloud.ibm.com default endpoint
# Set ProductionPrivate to use the private.iam.cloud.ibm.com endpoint
iamEnvironment: "Production"

# Configure this parameter to change the setting for the Kubernetes filter to include the annotations from Kubernetes with the log records.
# The default value for this setting is `false`.
includeAnnotations: true

# Configure this parameter to control the number of times the agent will retry sending data if an error occurs that is considered to be retryable.
# The default is `False`.
# For more information, see the [Fluentbit documentation about retries](https://docs.fluentbit.io/manual/administration/scheduling-and-retries) to understand the implications of setting this value.
retryLimit: False

# Configure additional tags as key/value pair tags that can be added as metadata to every log line.
additionalMetadata:
#  region: ca-tor
#  env: production

# Configure the level of logging
# Default value is info
# Valid values are: debug, info, or error
loggingLevel: info

```
{: codeblock}


## Helm Chart Configuration Options
{: #agent-helm-template-clusters-chart-options}

The following table contains a list of the parameters that you can configure in the `logs-values.yaml` file to adjust the {{site.data.keyword.agent}} configurations:

| Parameter | Description | Status | Default value |
|-----------|-------------|--------|---------------|
| `metadata.name` | The name of the agent that is used for all of the Kubernetes resources | Required | `logs-agent` |
| `image.version` | The version of the agent container image (ie. 1.3.0) | Required | No default value |
| `env.ingestionHost` | The {{site.data.keyword.logs_full_notm}} host to send the logs to | Required | No default value |
| `env.ingestionPort` | The {{site.data.keyword.logs_full_notm}} port to send the logs to | Required | No default value |
| `env.iamMode` | Indicate the IAM authentication mechanism used. Valid values are: `TrustedProfile` or `IAMAPIKey` | Required | `TrustedProfile` |
| `env.trustedProfileID` | The Trusted profile ID. | This parameter is required when `iamMode=TrustedProfile` | No default value |
| `secret.iamAPIKey` | The APIKey ID. You only should provide this value via the CLI. For more information, see `env.iamMode`. | This parameter is required when `iamMode=IAMAPIKey`   | No default value |
| `clusterName` | The name of the kubernetes cluster | Optional | No default value |
| `scc.create` | Indicates when to create the Secure Context Constraints in Openshift | Required for Openshift cluster deployments only. | `false` |
| `defaultMetadata.subsystemName` | Static string to override the subsystemName in {{site.data.keyword.logs_full_notm}} | Optional | The default value is set to the namespace that generated the log |
| `defaultMetadata.applicationName` | Static string to override the applicationName in {{site.data.keyword.logs_full_notm}} | Optional | The default value is set to the container name that generated the log |
| `resources` | Override the kubernetes resources allocated to the logs-agent | Optional | See [Resources](#agent-helm-template-clusters-chart-options-resources) to see the default values |
| `additionalLogSourcePaths` | The path of additional logs beyond the default. /var/log/containers/*.log \n For more information, see [Log Source Paths configurations](#agent-helm-template-clusters-chart-options-log-source-paths).| Optional | No default value |
| `excludeLogSourcePaths` | The path of additional logs that should not be collected by the agent. \n For more information, see [Log Source Paths configurations](#agent-helm-template-clusters-chart-options-log-source-paths).| Optional | No default value |
| `selectedLogSourcePaths` | The path of logs that are collected by the agent, excluding the default path and any files configured in `additionalLogSourcePaths`. \n For more information, see [Log Source Paths configurations](#agent-helm-template-clusters-chart-options-log-source-paths).| Optional | No default value |
| `includeAnnotations` | Instruct the kubernetes plugin to include the container annotations with the log messages \n For more information, see [includeAnnotations]#agent-helm-template-clusters-chart-options-include-annotations).| Required | `false` |
| `retryLimit` | Limit the number of retries that will be attempted \n For more information, see [retryLimit](#agent-helm-template-clusters-deploy-chart-options-retrylimit)| Required | False |
| `loggingLevel` | The type of logs that should be reported by the agent itself. Valid values are: `debug`, `info`, or `error`. | Required | `info` |
| `additionalMetadata` | A list of key/value pair tags that can be added as metadata to every log line. \n For more information, see [additionalMetadata](#agent-helm-template-clusters-deploy-chart-options-additional-metadata). | Optional | No default value  |
| `iamEnvironment` | Controls the IAM endpoint used by the agent to exchange the tokens.  \n For more information, see [iamEnvironment](#agent-helm-template-clusters-chart-options-iam-env). | Required | `Production` |
{: caption="Helm chart parameters" caption-side="bottom"}

## env.iamMode
{: #agent-helm-template-clusters-chart-options-iammode}

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

    If the `secret.iamAPIKey` variable is provided on the helm command (ie. `--set secret.iamAPIKey=<your iamAPIKey>`), then the helm chart will create the Kubernetes secret.

    Alternatively, you can create the secret ahead of time with the command: (Make sure you are connected to your cluster.)

    ```sh
    kubectl create secret generic <helm install-name> -n ibm-observe --from-literal=IAM_API_KEY=<apikey>
    ```
    {: codeblock}



## defaultMetadata
{: #agent-helm-template-clusters-chart-options-defaultmetadata}

This section allows the user to override the default subsystemName and applicationName that are used in the environment.
By default, the values are not set and the output plugin will dynamically set the values to:

- subsystemName: the Kubernetes namespace that generated the log
- applicationName: the container name that generated the log

The entry in the `logs-values.yaml` file looks as follows:

```yaml
defaultMetadata:
  subsystemName: ""
  applicationName: ""
```
{: codeblock}

## resources
{: #agent-helm-template-clusters-chart-options-resources}

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

## Log Source Paths configurations
{: #agent-helm-template-clusters-chart-options-log-source-paths}

By default the agent will collect the logs from `/var/log/containers/*.log`.
{: note}

The following additional variables can be provided to include, exclude or restrict the set of logs to be processed:
- `additionalLogSourcePaths` adds locations to the default set of logs that will be processed.
- `excludeLogSourcePaths` ignores logs in the specified locations.
- `selectedLogSourcePaths` overrides the default path `/var/log/containers/*.log` and ignores the `additionalLogSourcePaths` configurations. Only the files that are set through this parameter are collected by the agent.

You can define multiple paths by using a comma separated list, for example “/var/log/abc/*.log,/var/log/xyz/*.log”.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
# comma separated list, for example “/var/log/abc/*.log,/var/log/xyz/*.log”
additionalLogSourcePaths: ""
excludeLogSourcePaths: ""
selectedLogSourcePaths: ""
```
{: codeblock}

## iamEnvironment
{: #agent-helm-template-clusters-chart-options-iam-env}

This configuration controls the IAM endpoint used by the agent to exchange the tokens.

The default value is `Production`.

Valid values are :
- Set `Production` to use the `iam.cloud.ibm.com` default endpoint
- Set `ProductionPrivate` to use the `private.iam.cloud.ibm.com` endpoint

The entry in the `logs-values.yaml` file looks as follows:

```yaml
iamEnvironment: "Production"
```
{: codeblock}

## includeAnnotations
{: #agent-helm-template-clusters-chart-options-include-annotations}

This configuration changes the setting for the Kubernetes filter to include the annotations from Kubernetes with the log records.

The default value for this setting is `false`.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
includeAnnotations: true
```
{: codeblock}

## retryLimit
{: #agent-helm-template-clusters-deploy-chart-options-retrylimit}

This configuration places a limit on the number of times the agent will retry sending data if an error occurs that is considered to be retryable.

The default is `False`.

For more information, see the [Fluentbit documentation about retries](https://docs.fluentbit.io/manual/administration/scheduling-and-retries) to understand the implications of setting this value.

In some situations this setting could lead to log data being discarded by the agent due to the inability to send.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
retryLimit: 8
```
{: codeblock}

## additionalMetadata
{: #agent-helm-template-clusters-deploy-chart-options-additional-metadata}

This is a list of key/value pairs that will be added under the `meta` object to permit additional tags.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
additionalMetadata:
  region: ca-tor
  env: production
```
{: codeblock}

The above example will result in the following additional fields added to each log line in {{site.data.keyword.logs_full_notm}}:

```json
{
  "meta": {
    "region": "ca-tor",
    "env": "production"
  }
}
```
{: screen}
