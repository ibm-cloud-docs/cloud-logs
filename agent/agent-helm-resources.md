---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Change the resources that are assigned to the {{site.data.keyword.agent}} container
{: #agent-helm-resources}

When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to define changes to the resources that are assigned to the {{site.data.keyword.agent}} container.
{: shortdesc}

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

After you modify the `logs-values.yaml`, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
