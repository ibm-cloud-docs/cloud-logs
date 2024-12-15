---

copyright:
  years:  2024
lastupdated: "2024-12-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the {{site.data.keyword.agent}} to collect the Windows event log
{: #agent-windows-event-log}

A commonly used input plug-in on Windows systems is the Windows Event Log input plug-in which gathers events from specific channels. To congifure the {{site.data.keyword.agent}} to read, gather, and forward events from this source using the current API from `winevt.h`, complete the following steps:
{: shortdesc}

## Configure the Input plugin
{: #agent-windows-event-log-step1}
{: step}

1. Edit the input plug-in configuration file `input-windows-event-log.conf` in `C:\Program Files\logs-agent\etc` if one was created during the configuration step. If no file exists, create the `input-windows-event-log.conf` file.

2. Create a new *INPUT* section.

    Set the **Channels** with the channels you want to read events from.

    Set the **Tag** with an identifier that can help with parsing.

    ```yaml
    [INPUT]
        Name         winevtlog
        Tag          winevtlog.*
        Channels     Application,Setup,Windows PowerShell
    ```
    {: codeblock}

3. Save the configuration file.

## Modify the fluentbit configuration
{: #agent-windows-event-log-step2}
{: step}

Modify the `C:\Program Files\logs-agent\etc\fluent-bit.conf` file to include the reference to the `C:\Program Files\logs-agent\etc\input-windows-event-log.conf`.

```yaml
@INCLUDE C:\Program Files\logs-agent\etc\input-windows-event-log.conf
```
{: codeblock}

The main configuration file `C:\Program Files\logs-agent\etc\fluent-bit.conf` imports other files with the tag `@INCLUDE <path_to_file>`.


## Restart the agent
{: #agent-windows-event-log-step3}
{: step}

Restart the agent to apply the changes.

```bat
sc.exe stop fluent-bit && sc.exe start fluent-bit
```
{: codeblock}


## Verify logs are being delivered to your target destination
{: #agent-windows-event-log-step4}
{: step}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view.
