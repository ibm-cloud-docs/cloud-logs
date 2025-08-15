---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Helm Chart configuration required
{: #agent-helm-template-config-options-required}

Starting with Helm chart version 1.6.0, the Fluent Bit log pipeline configuration has transitioned to using the official [Fluent Bit YAML configuration](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/yaml) format. This change brings enhanced flexibility and clarity to configuration management.
{: note}


## List of required parameters
{: #agent-helm-template-config-options-required-1}

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

#additionalMetadata:        # Add additional metadata
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
