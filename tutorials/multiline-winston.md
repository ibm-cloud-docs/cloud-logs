---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

content-type: tutorial
services:  cloud-logs
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}


# Customizing the 1.6.x {{site.data.keyword.agent}} to support custom multiline parsing for Node.js applications using Winston in non-orchestrated environments
{: #multiline-winston}
{: toc-content-type="tutorial"} 
{: toc-services="cloud-logs"}
{: toc-completion-time="30m"} 

This tutorial demonstrates how to configure the {{site.data.keyword.logs_full}} {{site.data.keyword.agent}} multiline log handling for a Node.js application using the customized [Winston](https://github.com/winstonjs/winston){: external} logging library. This configuration is for non-orchestrated environments, for example, Linux and Windows, and modifies the configuration file. This configuration ensures that stack traces and multiline logs are grouped correctly in {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

This tutorial requires the {{site.data.keyword.logs_full_notm}} {{site.data.keyword.agent}} 1.6.2 or later.
{: requirement}

## Before you begin
{: #multiline-winston-prereq}

Before you begin using this tutorial, review the following information to understand {{site.data.keyword.agent}} and multiline concepts.

* [Learn about the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about)

* Learn about multiline support in non-orchestrated environments.

    * [Linux]{: tag-linux} [Linux](/docs/cloud-logs?topic=cloud-logs-agent-multiline-linux)

    * [Windows]{: tag-windows} [Windows](/docs/cloud-logs?topic=cloud-logs-agent-multiline-windows)

This tutorial also assumes you have:

* An {{site.data.keyword.logs_full_notm}} instance provisioned and configured.

* The {{site.data.keyword.agent}} deployed in a non-orchestrated environment.

    * [Linux]{: tag-linux} [Linux](/docs/cloud-logs?topic=cloud-logs-agent-linux)

    * [Windows]{: tag-windows} [Windows](/docs/cloud-logs?topic=cloud-logs-agent-windows)

The configuration files in this tutorial can be found where the package files were downloaded when you installed the {{site.data.keyword.agent}}.
{: tip}

## Sample Winston configuration
{: #multiline-winston-config}

Let's assume your Node.js application uses Winston and logs to the console in the following format:

```js
const winston = require('winston');

const logger = winston.createLogger({
  level: 'info',
  format: winston.format.combine(
    winston.format.timestamp({
      format: 'ddd MMM DD YYYY HH:mm:ss.SSS'
    }),
    winston.format.errors({ stack: true }),
    winston.format.printf(({ timestamp, level, message, stack }) => {
      const levelUpper = level.toUpperCase();
      const baseLog = `[${timestamp}] ${levelUpper} [Main] - ${message}`;
      if (stack) {
        return `${baseLog}\n${stack}`;
      }
      return baseLog;
    })
  ),
  transports: [
    new winston.transports.Console()
  ]
});
```
{: codeblock}

This format produces log entries that start with a timestamp and level, and multiline logs, such as error stack traces, follow on subsequent lines without timestamps.

Winston typically logs all output, including error stack traces, as a single string so a multiline parser is often not required. However, this example demonstrates what to do if your formatter prints multiline logs, and it helps illustrate how to approach multiline parsing for any custom format.

This configuration is provided as an example to show how to handle multiline logs when using custom log formatting. If your application uses a different structure or logging library, use this as a reference to create your own multiline parser accordingly.
{: note}


## Configuring multiline parsing manually by using a configuration file
{: #multiline-winston-configmap}

To properly group logs, define a multiline parser that recognizes the timestamp at the beginning of new log entries and treats subsequent lines as continuations of the previous entries.

## Define the multiline parser
{: #multiline-winston-configmap-s1}
{: step}

Add the following to `parsers.conf` file:

```yaml
[MULTILINE_PARSER]
    Name            multiline-nodejs-winston
    Type            regex
    Flush_timeout   500
    Rule            "start_state"     "/^\\[[A-Z][a-z]{2} [A-Z][a-z]{2} \\d{2} \\d{4} \\d{2}:\\d{2}:\\d{2}\\.\\d{3}\\] .*$/"
    Rule            "cont"            "/^(?!\\[[A-Z][a-z]{2} [A-Z][a-z]{2} \\d{2} \\d{4} \\d{2}:\\d{2}:\\d{2}\\.\\d{3}\\] ).*$/"
```
{: codeblock}

This parser assumes logs begin with a timestamp such as `[Wed Jul 24 2025 14:52:31.456] ...`. Stack traces are indented on the following lines and do not match the timestamp regex, so they are grouped with the previous log line.

## Apply the parser with a multiline filter
{: #multiline-winston-configmap-s2}
{: step}

Add a filter block to the `filters.conf` file to use the parser:

```yaml
[FILTER]
    Name                  multiline
    Match                 kube.*
    Multiline.key_content log
    Multiline.parser      multiline-nodejs-winston
```
{: codeblock}



## Restart the agent
{: #multiline-winston-s3}
{: step}

After updating the config map, restart the agent.

* [Linux]{: tag-linux} For Linux environments, run:

   ```sh
   systemctl daemon-reload && systemctl restart fluent-bit
   ```
   {: pre}

* [Windows]{: tag-windows} For Windows environments, run:

   ```sh
   sc.exe stop fluent-bit && sc.exe start fluent-bit
   ```
   {: pre}


## Verify your multiline logs
{: #multiline-winston-s4}
{: step}

Access your {{site.data.keyword.logs_full_notm}} instance and confirm your multiline entries (for example, stack traces) are grouped correctly.

1. [Access your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

2. Using the **Logs** ![Explore logs icon](../icons/explore.svg "Explore logs") view, verify that your multiline entries are grouped correctly.

   The grouped log data is included in the `log` field.
   {: note}
