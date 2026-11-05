---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# No logs appear when {{site.data.keyword.agent}} collects logs forwarded by Rsyslog
{: #troubleshoot-agent-no-logs-rsyslog}
{: troubleshoot}
{: support}

No logs appear in {{site.data.keyword.logs_full_notm}} when {{site.data.keyword.agent}} is configured to collect logs that are forwarded by Rsyslog.
{: shortdesc}

You configured {{site.data.keyword.agent}} to collect logs that are forwarded by Rsyslog, but no logs appear in {{site.data.keyword.logs_full_notm}}.
{: tsSymptoms}

Rsyslog is not forwarding logs to the {{site.data.keyword.agent}}.
{: tsCauses}

Complete the following steps to confirm that Rsyslog is forwarding logs:
{: tsResolve}

1. Send a test message to the system log.

   ```sh
   logger -t test hello
   ```
   {: pre}

2. Check that the `/etc/rsyslog.d/60-otelcol-ibm.conf` file exists.

   ```sh
   ls -l /etc/rsyslog.d/60-otelcol-ibm.conf
   ```
   {: pre}

For more information about configuring Rsyslog forwarding, see [Configuring the agent](/docs/cloud-logs?topic=cloud-logs-cloud-logs-agent-configure).
