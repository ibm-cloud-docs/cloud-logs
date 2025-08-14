---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configure custom metadata values by using Helm
{: #agent-helm-metadata}

When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to include custom values for applicationName and subsystemName, and also add custom tags to your log records.


## Configure custom values for applicationName and subsystemName
{: #agent-helm-metadata-1}

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
{: #agent-helm-metadata-2}

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
