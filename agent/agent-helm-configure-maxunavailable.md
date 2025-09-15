---

copyright:
  years:  2025, 2025
lastupdated: "2025-09-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the maximum number of unavailable pods during an update
{: #agent-helm-configure-maxunavailable}

When you deploy or upgrade the {{site.data.keyword.agent}}, you can configure the `logs-values.yaml` file to include an optional parameter to specify how many pods can be unavailable during a rolling update.
{: shortdesc}


The optional parameter `updateStrategy.maxUnavailable` lets you specify the maximum number or percentage of unavailable pods when the agent daemonset does a rolling update. Enclose a percentage value in quotation marks so it is interpreted as a string. Do not include a number in quotation marks so it is interpreted as int32. By default, a percentage value of `"25%"` is used. Configure the {{site.data.keyword.agent}} to use a custom value by adding the `updateStrategy.maxUnavailable` configuration to your `log-values.yaml` file:

The following specifies that a maximum of 10% of pods can be unavailable.

```yaml
updateStrategy:
  maxUnavailable: "10%" # optional (default is 25%)
```
{: codeblock}

The following specifies that a maximum of 5 of pods can be unavailable.

```yaml
updateStrategy:
  maxUnavailable: 5 # optional (default is 25%)
```
{: codeblock}

After you modify the `logs-values.yaml`, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.

When the pods are updated from an old {{site.data.keyword.agent}} version to a new agent version, Kubernetes will stop no more than the `updateStrategy.maxUnavailable` number of pods running the old agent version. 

When the `updateStrategy.maxUnavailable` number of old pods is reached, the rolling update will be paused until new pods with the new version are running. 

The helm command can be configured to wait for a specific time for the update to complete (see the `timeout` and `wait` [helm upgrade options](https://helm.sh/docs/helm/helm_upgrade/){: external}), but will otherwise only update the daemonset definition and let Kubernetes update the agent pods. The Kubernetes controller will keep retrying to update the agent pods indefinitely until all pods are updated.
 
If new pods are having issues coming up, the update won't continue. For more information on agent configuration errors, see [I am getting an error when starting the {{site.data.keyword.agent}}?](/docs/cloud-logs?topic=cloud-logs-ts-fb-error). Check and correct your configuration if required and retry the update.
