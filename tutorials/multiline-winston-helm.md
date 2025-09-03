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


# Customizing the 1.6.x {{site.data.keyword.agent}} to support custom multiline parsing for Node.js applications using Winston in orchestrated environments
{: #multiline-winston-helm}
{: toc-content-type="tutorial"}
{: toc-services="cloud-logs"}
{: toc-completion-time="30m"}

This tutorial demonstrates how to configure the {{site.data.keyword.logs_full}} {{site.data.keyword.agent}} multiline log handling for a Node.js application using the customized [Winston](https://github.com/winstonjs/winston){: external} logging library. This configuration is for orchestrated environments, for example {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.openshiftlong_notm}}, and uses Helm. This configuration ensures that stack traces and multiline logs are grouped correctly in {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

This tutorial requires the {{site.data.keyword.logs_full_notm}} {{site.data.keyword.agent}} 1.6.0 or later.
{: requirement}

## Before you begin
{: #multiline-winston-prereq-helm}

Before you begin using this tutorial, review the following information to understand {{site.data.keyword.agent}} and multiline concepts.

* [Learn about the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about)

* [Learn about multiline support in orchestrated environments](/docs/cloud-logs?topic=cloud-logs-agent-multiline)

This tutorial also assumes you have:

* An {{site.data.keyword.logs_full_notm}} instance provisioned and configured.

* The {{site.data.keyword.agent}} deployed in an orchestrated environment.

    * [{{site.data.keyword.containershort}}]{: tag-iks} [{{site.data.keyword.containerlong_notm}}](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy)

    * [{{site.data.keyword.openshiftshort}}]{: tag-roks} [{{site.data.keyword.openshiftlong_notm}}](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy)


## Sample Winston configuration
{: #multiline-winston-sample-helm}

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


## Configuring multiline parsing with Helm
{: #multiline-winston-helm-config}

If you are deploying the {{site.data.keyword.agent}} using Helm, you can configure multiline parsing in the Helm `values.yaml` file.

## Enable multiline parsing
{: #multiline-winston-helm-s2}
{: step}

Set `enableMultiline` to `true` in your `values.yaml` file to activate multiline processing:

```yaml
enableMultiline: true
```
{: codeblock}

## Define the multiline parser
{: #multiline-winston-helm-s1}
{: step}

Add a custom multiline parser under the `additionalMultilineParsers` section in your `values.yaml` file.

It is important for the pattern defined in the `log4j.xml` file align with the regex in the multiline parser to ensure proper log grouping.
{: important}

```yaml
additionalMultilineParsers:
  - name: multiline-nodejs-winston
    type: regex
    flush_timeout: 500
    rules:
      - state: start_state
        regex: '/^\[[A-Z][a-z]{2} [A-Z][a-z]{2} \d{2} \d{4} \d{2}:\d{2}:\d{2}\.\d{3}\] .*$/'
        next_state: cont
      - state: cont
        regex: '/^(?!\[[A-Z][a-z]{2} [A-Z][a-z]{2} \d{2} \d{4} \d{2}:\d{2}:\d{2}\.\d{3}\] ).*$/'
        next_state: cont
```
{: codeblock}

The regex assumes that each new log line starts with a timestamp in the format `ddd MMM DD YYYY HH:mm:ss.SSS`. The first rule captures starting lines with timestamps and moves to a continuation state. The second rule matches any line not starting with a timestamp.

This approach is just an example to show you how to ensure multiline log lines are grouped as a single log entry before forwarding them to {{site.data.keyword.logs_full_notm}}. There are different ways to achieve the same thing.
{: note}



## Apply the parser in a preprocessor
{: #multiline-winston-helm-s3}
{: step}

Configure a preprocessor under the `multilinePreprocessor` section to apply the parser to your logs.

For example:

```yaml
multilinePreprocessor:
  - name: multiline
    multiline.parser: multiline-nodejs-winston
    multiline.key_content: log
```
{: codeblock}


## Apply the changes.
{: #multiline-winston-helm-s4}
{: step}

If you have installed a previous version of the {{site.data.keyword.agent}} and have updated the agent configuration by modifying the config map directly in the cluster, make a copy of your config map from the cluster before running the `helm upgrade` command. When the {{site.data.keyword.agent}} is updated, any changes made to the config map will be overwritten.
{: attention}

After updating the `values.yaml` file, apply the changes by running the following on your deployment. This will regenerate the necessary configurations.

```sh
helm upgrade
```
{: pre}


## Verify your multiline logs
{: #multiline-winston-s4}
{: step}

Access your {{site.data.keyword.logs_full_notm}} instance and confirm your multiline entries (for example, stack traces) are grouped correctly.

1. [Access your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

2. Using the **Logs** ![Explore logs icon](../icons/explore.svg "Explore logs") view, verify that your multiline entries are grouped correctly.
