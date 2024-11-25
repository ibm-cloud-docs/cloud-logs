---

copyright:
  years:  2024
lastupdated: "2024-11-25"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# I am getting an error when starting the {{site.data.keyword.agent}}.
{: #ts-fb-error}
{: troubleshoot}
{: support}

When starting the {{site.data.keyword.logs_full}} {{site.data.keyword.agent}} an error is returned.
{: shortdesc}

You get the following error message: 
{: tsSymptoms}

```text
Failed to start Fluent Bit.
```
{: screen}


Your [agent configuration file](/docs/cloud-logs?topic=cloud-logs-agent-fluentbit) has an error.
{: tsCauses}


Check that each key in the agent configuration has an associated value.
{: tsResolve}

For example, if you didn't specify a value for `Exclude_Path` in your configuration, this error will be returned.

```yaml
[INPUT]
    Name              tail
    Tag               kube.*
    Path              /var/log/containers/logger-agent-ds-*.log
    Path_Key          file
    Exclude_Path
    DB                /var/log/fluent-bit/fluent-bit.DB
    Buffer_Chunk_Size 32KB
    Buffer_Max_Size   256KB
    Parser            cri
    Skip_Long_Lines   On
    Refresh_Interval  10
    storage.type      filesystem
    storage.pause_on_chunks_overlimit on
```
{: codeblock}
