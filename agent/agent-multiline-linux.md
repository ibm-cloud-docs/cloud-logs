---

copyright:
  years:  2024, 2025
lastupdated: "2025-08-26"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring multiline support for the {{site.data.keyword.agent}} in Linux
{: #agent-multiline-linux}

Grouping of multiline logs by the {{site.data.keyword.logs_full}} {{site.data.keyword.agent}} from non-orchestrated environments (for example, Linux) is configured similar to that of orchestrated environments. The changes include the parsing required to group log lines that are supposed to be together as a single log record.
{: shortdesc}

If you're running the {{site.data.keyword.agent}} in a non-orchestrated environment (such as a standalone VM or  bare-metal server), you do **not** need to apply multiline parsers using a separate filter or preprocessor.

Instead, you can directly specify your multiline parsers in the `[INPUT]` section of the `inputs.conf` file. This is simpler and sufficient.

For example:

```yaml
[INPUT]
      Name              tail
      Tag               *
      Path              /var/log/*.log
      Path_Key          file
      Exclude_Path      /var/log/audit.log
      DB                /var/lib/fluent-bit/fluent-bit.DB
      Buffer_Chunk_Size 32KB
      Buffer_Max_Size   256KB
      Multiline.parser  go,multiline-java-example,multiline-nodejs-winston
      Skip_Long_Lines   On
      Refresh_Interval  10
      storage.type      filesystem
      storage.pause_on_chunks_overlimit on
```
{: codeblock}

Multiple multiline parsers are specified in `Multiline.parser` as a comma-separated list. The agent will try each parser in the order provided until one matches. This is useful when your system hosts applications with different logging formats (for example, Go, Java, Node.js).

## How multiline logs are grouped for display
{: #agent-multiline-display}

When viewing grouped log data in the {{site.data.keyword.logs_full_notm}} UI, the grouped log data is included in the `log` field.

## More information and examples
{: #agent-multiline-non-moreinfo}

For more information and tutorials with example scenarios for configuring multiline processing, see the following topics.

| For information about | See |
|-----------------------|-----|
| Configuring multiline support for the {{site.data.keyword.agent}} in orchestrated environments | [Topic](/docs/cloud-logs?topic=cloud-logs-agent-multiline) |
| Multiline parsing for Java applications with Log4j | [Tutorial](/docs/cloud-logs?topic=cloud-logs-multiline-log4j) |
| Multiline parsing using Helm for Java applications with Log4j | [Tutorial](/docs/cloud-logs?topic=cloud-logs-multiline-log4j-helm) |
| Multiline parsing for Node.js applications using Winston | [Tutorial](/docs/cloud-logs?topic=cloud-logs-multiline-winston) |
| Multiline parsing using Helm for Node.js applications using Winston | [Tutorial](/docs/cloud-logs?topic=cloud-logs-multiline-winston-helm) |
{: caption="Additional resources for the {{site.data.keyword.agent}} multiline processing" caption-side="bottom"}
