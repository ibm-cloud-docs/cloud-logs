---

copyright:
  years:  2024
lastupdated: "2024-12-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Adding metadata to the {{site.data.keyword.agent}} for Windows
{: #agent-windows-metadata}

You can configure the {{site.data.keyword.agent}} to include metadata that is associated to each log line.
{: shortdesc}

Complete the following steps:


## Modify the fluentbit configuration
{: #agent-windows-metadata-step1}
{: step}

1. Edit the `fluent-bit.conf` file in the `C:\Program Files\logs-agent\etc` folder.

2. Add custom metadata:

    Use `Add meta.<field_name> <custom_value>` to add a new field `field_name` with the value `custom_value`.

    Use `Copy <log_field_name> <new_field_name>` to add a new field `new_field_name` with the value of the field `log_field_name` that comes in the log line.

    ```yaml
    [FILTER]
        Name modify
        Match winevtlog.*
        Copy ProviderName subsystemName
        Add applicationName ${COMPUTERNAME}
        Add meta.source ${SOURCE}
        Add meta.channel ${Channel}
        Add meta.providerName ${ProviderName}
        Add meta.environment prod   # Sample values: prod, staging, dev, qa
        Add meta.platform windows

    [FILTER]
        Name nest
        Match winevtlog.*
        Operation nest
        Wildcard meta.*
        Nest_under meta
        Remove_prefix meta.
    ```
    {: codeblock}

    For example:

    `Add applicationName ${COMPUTERNAME}`
    :   Sets the field applicationName with the hostname.

    `Copy ProviderName subsystemName`
    :   Copies the value of the `ProviderName` field into a new field called `subsystemName`.

    `<meta.key_name>`
    :   Is the name of the metadata field to be added (for example, `meta.env`) and `<your_custom_value>` is the value to be assigned to the field (for example, the name of your environment).

3. Save the configuration file.



## Restart the agent
{: #agent-windows-metadata-step2}
{: step}

Restart the agent to apply the changes.

```bat
sc.exe stop fluent-bit && sc.exe start fluent-bit
```
{: codeblock}


## Verify logs are being delivered to your target destination
{: #agent-windows-metadata-step3}
{: step}


Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view.
