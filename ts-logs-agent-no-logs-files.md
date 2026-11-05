---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# No logs appear when {{site.data.keyword.agent}} collects log files
{: #troubleshoot-agent-no-logs-files}
{: troubleshoot}
{: support}

No logs appear in {{site.data.keyword.logs_full_notm}} when {{site.data.keyword.agent}} is configured to collect log files by using the `--log-path` parameter.
{: shortdesc}

You configured {{site.data.keyword.agent}} to collect log files, but no logs from those files appear in {{site.data.keyword.logs_full_notm}}.
{: tsSymptoms}

The log file that is specified in the `--log-path` parameter does not exist or is not readable. Also, by default, the agent sends only lines that are appended to a file after the agent starts. Existing file content is not sent.
{: tsCauses}

Complete the following steps to resolve the problem:
{: tsResolve}

1. Confirm that the log file exists and is readable. 

2. If you want to send the content that already exists in the file, run the configuration script again with the `--start-at-beginning` parameter.

   ```sh
   sudo /opt/otelcol-ibm/configure.sh \
     -i <instance_guid> \
     -r <region> \
     -k <api_key> \
     --application-name <app_name> \
     --log-path /var/log/messages \
     --start-at-beginning
   ```
   {: codeblock}

For more information about the configuration parameters, see [Configuring the agent](/docs/cloud-logs?topic=cloud-logs-cloud-logs-agent-configure).
