---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Considerations when you configure the {{site.data.keyword.agent}}
{: #agent-configuration-considerations}

When you configure the {{site.data.keyword.logs_full}} {{site.data.keyword.agent}}, you need to understand how logs are processed and how changing the default configuration can potentially result in dropped logs.
{: shortdesc}

To take advantage of the best logs processing, with the least potential of dropped data, you want to run the latest {{site.data.keyword.agent}} version. This information assumes that you are running the {{site.data.keyword.agent}} 1.6.1 or later.
{: important}

## Retry limit
{: #consid-retry}

By default the {{site.data.keyword.agent}} is configured to keep retrying to send logs until successful if an error occurs.  The default behavior is configured by the [`retryLimit: false`](/docs/cloud-logs?topic=cloud-logs-agent-helm-retry-sending-data) parameter.  In Kubernetes this is managed in the {{site.data.keyword.agent}} configmap, and in Linux environments it is in the {{site.data.keyword.agent}} config file.

If you change the default `retryLimit` value, you have the potential for dropped data. For example, `retryLimit: "no_retries"` indicates that the {{site.data.keyword.agent}} does not retry sending logs at all when an error occurs. Specifying an integer value, for example `retryLimit: 8`, indicates that the {{site.data.keyword.agent}} retries sending logs for the specified number (8) of times before the logs are dropped.

For information about how Fluent Bit schedules the retry intervals, see [Scheduling and retries.](https://docs.fluentbit.io/manual/administration/scheduling-and-retries){: external}

## Fluent Bit buffering
{: #consid-buffer}

The {{site.data.keyword.agent}} is configured by default to use Fluent Bit `filesystem` buffering. This configuration means that logs processed by the {{site.data.keyword.agent}} are kept in file storage in case of a system failure. When the {{site.data.keyword.agent}} restarts, logs in the `filesystem` buffer are processed.

If you change the configuration to use `memory` buffering, and an issue occurs where the {{site.data.keyword.agent}} is terminated or terminates unexpectedly, logs in the `memory` buffer can be dropped.

For more information, see [Buffering and storage](https://docs.fluentbit.io/manual/administration/buffering-and-storage){: external}.

## Log rotation
{: #consid-rotate}

If the environment rotates the log files before the {{site.data.keyword.agent}} can process them, a potential exists that logs might be dropped. Dropped data due to log rotation can occur if the {{site.data.keyword.agent}} stops running for a significant amount of time.

[Kubernetes]{: tag-iks}

In IBM managed clusters all `stdout` container log files in `/var/log/containers` are managed by [kublet](/docs/containers?topic=containers-service-settings&utm_source=chatgpt.com#kubelet).  Each container log file will be rotated when it reaches 100MiB in size.  After rotation, up to 3 log files will be retained per container. The size and number of these files is not configurable.

If the log files fill and rotate before the {{site.data.keyword.agent}} processes the data, the unprocessed logs can be dropped.

[Linux]{: tag-linux}

Log rotation processing can be configured in Linux. For example, by using the `logrotate` tool.

If the log files fill and rotate before the {{site.data.keyword.agent}} processes the data, the unprocessed logs can be dropped.

[Windows]{: tag-windows}

Log rotation processing can be configured in Windows. However, no built-in Windows tool exists for log rotation. Third-party applications, or built-in application settings, can be used to configure log rotation.

If the log files fill and rotate before the {{site.data.keyword.agent}} processes the data, the unprocessed logs can be dropped.
