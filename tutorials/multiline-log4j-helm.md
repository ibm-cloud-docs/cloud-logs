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


# Customizing the 1.6.x {{site.data.keyword.agent}} to support custom multiline parsing for Java applications with Log4j in orchestrated environments
{: #multiline-log4j-helm}
{: toc-content-type="tutorial"}
{: toc-services="cloud-logs"}
{: toc-completion-time="30m"}

This tutorial demonstrates how to configure the {{site.data.keyword.logs_full}} {{site.data.keyword.agent}} multiline log handling for a Java application using the [Log4j](https://logging.apache.org/log4j/2.x/index.html){: external} logging framework. This configuration is for orchestrated environments, for example {{site.data.keyword.containerlong_notm}} and {{site.data.keyword.openshiftlong_notm}}, and uses Helm. This configuration ensures that stack traces and multiline logs are grouped correctly in {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

This tutorial requires the {{site.data.keyword.logs_full_notm}} {{site.data.keyword.agent}} 1.6.0 or later.
{: requirement}

## Before you begin
{: #multiline-log4j-prereq-helm}

Before you begin using this tutorial, review the following information to understand {{site.data.keyword.agent}} and multiline concepts.

* [Learn about the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about)

* [Learn about multiline support in orchestrated environments](docs/cloud-logs?topic=cloud-logs-agent-multiline-new)

This tutorial also assumes you have:

* An {{site.data.keyword.logs_full_notm}} instance provisioned and configured.

* The {{site.data.keyword.agent}} deployed in an orchestrated environment.

    * [{{site.data.keyword.containershort}}]{: tag-iks} [{{site.data.keyword.containerlong_notm}}](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy)

    * [{{site.data.keyword.openshiftshort}}]{: tag-roks} [{{site.data.keyword.openshiftlong_notm}}](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy)


## Sample Log4j configuration
{: #multiline-log4j-config-helm}

Let's assume that your Java application's Log4j to log to the console (`stdout`) is similar to the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="WARN">
    <Appenders>
        <Console name="Console" target="SYSTEM_OUT">
            <PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n" />
        </Console>
    </Appenders>
    <Loggers>
        <Root level="info">
            <AppenderRef ref="Console"/>
        </Root>
    </Loggers>
</Configuration>
```
{: codeblock}

This configuration outputs logs in the format: `yyyy-MM-dd HH:mm:ss.SSS [thread] LEVEL logger - message`, followed by a newline. Multiline messages, such as stack traces, will appear on subsequent lines without a timestamp prefix. For example:

```text
2025-07-28 10:32:15.423 [main] INFO com.example.logging.Main - Application starting up
2025-07-28 10:32:16.191 [main] INFO com.example.logging.Main - This is an info message
2025-07-18 10:32:18.801 [main] ERROR com.example.logging.Main - This is an error message
java.lang.NullPointerException: null
at com.example.logging.Main.lambda$main$3(Main.java:30) ~[java-log4j-1.0.0.jar:?]
at spark.RouteImpl$1.handle(RouteImpl.java:72) ~[java-log4j-1.0.0.jar:?]
at spark.http.matching.Routes.execute(Routes.java:61) ~[java-log4j-1.0.0.jar:?]
at spark.http.matching.MatcherFilter.doFilter(MatcherFilter.java:134) ~[java-log4j-1.0.0.jar:?]
at spark.embeddedserver.jetty.JettyHandler.doHandle(JettyHandler.java:50) ~[java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.server.session.SessionHandler.doScope(SessionHandler.java:1584) ~[java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.server.handler.ScopedHandler.handle(ScopedHandler.java:141) ~[java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.server.handler.HandlerWrapper.handle(HandlerWrapper.java:127) ~[java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.server.Server.handle(Server.java:501) ~[java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.server.HttpChannel.lambda$handle$1(HttpChannel.java:383) ~[java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.server.HttpChannel.dispatch(HttpChannel.java:556) [java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.server.HttpChannel.handle(HttpChannel.java:375) [java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.server.HttpConnection.onFillable(HttpConnection.java:273) [java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.io.AbstractConnection$ReadCallback.succeeded(AbstractConnection.java:311) [java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.io.FillInterest.fillable(FillInterest.java:105) [java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.io.ChannelEndPoint$1.run(ChannelEndPoint.java:104) [java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.util.thread.QueuedThreadPool.runJob(QueuedThreadPool.java:806) [java-log4j-1.0.0.jar:?]
at org.eclipse.jetty.util.thread.QueuedThreadPool$Runner.run(QueuedThreadPool.java:938) [java-log4j-1.0.0.jar:?]
at java.lang.Thread.run(Unknown Source) [?:?]
```
{: screen}


## Configuring multiline parsing with Helm
{: #multiline-log4j-helm-config}

If you are deploying the {{site.data.keyword.agent}} using Helm, you can configure multiline parsing in the Helm `values.yaml` file.

## Enable multiline parsing
{: #multiline-log4j-helm-s2}
{: step}

Set `enableMultiline` to `true` in your `values.yaml` file to activate multiline processing:

```yaml
enableMultiline: true
```
{: codeblock}

## Define the multiline parser
{: #multiline-log4j-helm-s1}
{: step}

Add a custom multiline parser under the `additionalMultilineParsers` section in your `values.yaml` file. 

It is important for the pattern defined in the `log4j.xml` file align with the regex in the multiline parser to ensure proper log grouping.
{: important}

Example:

```yaml
additionalMultilineParsers:
  - name: multiline-java-example
    type: regex
    flush_timeout: 500
    rules:
      - state: start_state
        regex: '/^(\d+-\d+-\d+ \d+:\d+:\d+\.\d+)(.*)$/'
        next_state: cont
      - state: cont
        regex: '/^(?!\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2}\.\d{3}).*$/'
        next_state: cont
```
{: codeblock}

The regex assumes that each new log line starts with a timestamp in the format `yyyy-MM-dd HH:mm:ss.SSS`. The first rule captures starting lines with timestamps and moves to a continuation state. The second rule matches any line not starting with a timestamp.

This approach is just an example to show you how to ensure multiline log lines, such as Java stack traces and exceptions, are grouped as a single log entry before forwarding them to {{site.data.keyword.logs_full_notm}}. There are different ways to achieve the same thing.
{: note}

## Define the multiline preprocessor
{: #multiline-log4j-helm-s3}
{: step}

Configure a preprocessor under the `multilinePreprocessor` section to apply the parser to your logs.

For example:

```yaml
multilinePreprocessor:
  - name: multiline
    multiline.parser: multiline-java-example
    multiline.key_content: log
```
{: codeblock}

## Apply the changes.
{: #multiline-log4j-helm-s4}
{: step}

If you have installed a previous version of the {{site.data.keyword.agent}} and have updated the agent configuration by modifying the config map directly in the cluster, make a copy of your config map from the cluster before running the `helm upgrade` command. When the {{site.data.keyword.agent}} is updated, any changes made to the config map will be overwritten.
{: attention}

After updating the `values.yaml` file, apply the changes by running the following on your deployment. This will regenerate the necessary configurations.

```sh
helm upgrade
```
{: pre}


## Verify your multiline logs
{: #multiline-log4j-helm-s5}
{: step}

Access your {{site.data.keyword.logs_full_notm}} instance and confirm your multiline entries (for example, stack traces) are grouped correctly.

1. [Access your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

2. Using the **Logs** ![Explore logs icon](../icons/explore.svg "Explore logs") view, verify that your multiline entries are grouped correctly.
