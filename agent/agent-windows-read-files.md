---

copyright:
  years:  2024
lastupdated: "2024-12-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the {{site.data.keyword.agent}} to include or exclude files
{: #agent-windows-read-files}

You can configure the {{site.data.keyword.agent}} to include or exclude files that the agent monitors.
{: shortdesc}

Complete the following steps to deploy an agent to a supported Windows system.

## Configure the Tail plugin
{: #agent-windows-read-files-step1}
{: step}

1. Create the input plug-in configuration file `input-tail.conf` in `C:\Program Files\logs-agent\etc`.

2. Add the *INPUT* section.

    Set the **Path** with the directories and files that you want to monitor.

    Set the **Exclude_Path** with the directories and files that you want to exclude from monitoring.

    ```yaml
    [INPUT]
        Name              tail
        Tag               *
        Path              C:\logs\*.log
        Path_Key          file
        Exclude_Path      C:\logs\audit.log
        DB                C:\logs\fluent-bit.DB
        Buffer_Chunk_Size 32KB
        Buffer_Max_Size   256KB
        Skip_Long_Lines   On
        Refresh_Interval  10
    ```
    {: codeblock}

3. Save the configuration file.

## Modify the fluentbit configuration
{: #agent-windows-read-files-step2}
{: step}

Modify the `C:\Program Files\logs-agent\etc\fluent-bit.conf` file to include the reference to the `C:\Program Files\logs-agent\etc\input-windows-event-log.conf`.

```yaml
@INCLUDE C:\Program Files\logs-agent\etc\input-windows-event-log.conf
```
{: codeblock}

The main configuration file `C:\Program Files\logs-agent\etc\fluent-bit.conf` imports other files with the tag `@INCLUDE <path_to_file>`.


## Restart the agent
{: #agent-windows-read-files-step3}
{: step}

Restart the agent to apply the changes.

```bat
sc.exe stop fluent-bit && sc.exe start fluent-bit
```
{: codeblock}


## Verify logs are being delivered to your target destination
{: #agent-windows-read-files-step4}
{: step}


Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view.
