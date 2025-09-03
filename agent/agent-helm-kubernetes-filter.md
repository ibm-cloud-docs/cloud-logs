---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Enabling the Kubernetes filter to enrich logs with Kubernetes metadata
{: #agent-helm-kubernetes-filter}

When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to enrich logs with Kubernetes metadata. After you modify the `logs-values.yaml` file, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
{: shortdesc}

By default, the Helm chart enables the Kubernetes filter, `enableKubernetesFilter`, for processing the container logs.  This provides capabilities such as:

- Enriching the log lines with metadata about the running container.
- Invoking another parser after the CRI parser to further process the log data.
- Using annotations to choose a secondary parser.

For more information, see [Kubernetes](https://docs.fluentbit.io/manual/data-pipeline/filters/kubernetes){: external}.


If you do not wish to use these features, then they can be disabled with this option.

```yaml
enableKubernetesFilter: false
```
{: codeblock}


## Include metadata fields
{: #agent-helm-kubernetes-filter-1}

Youc an configure `kubernetesFields` to control which Kubernetes metadata fields are included with each log record.

By default, only essential fields such as `pod_name`, `namespace_name`, and `container_name` are kept. This helps reduce the amount of metadata stored with each log and reduces storage costs.

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


## Include annotations
{: #agent-helm-kubernetes-filter-2}

This configuration changes the setting for the Kubernetes filter to include the annotations from Kubernetes with the log records.

The default value for this setting is `false`.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
includeAnnotations: true
```
{: codeblock}


## Include labels
{: #agent-helm-kubernetes-filter-3}

This configuration changes the setting for the Kubernetes filter to include labels from Kubernetes with the log records.

The default value for this setting is `false`.

The entry in the `logs-values.yaml` file looks as follows:

```yaml
includeLabels: false
```
{: codeblock}
