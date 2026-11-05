---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.agent}} cannot connect to {{site.data.keyword.logs_full_notm}}
{: #troubleshoot-agent-cannot-connect}
{: troubleshoot}
{: support}

{{site.data.keyword.agent}} cannot connect to {{site.data.keyword.logs_full_notm}} when it attempts to send logs.
{: shortdesc}

{{site.data.keyword.agent}} cannot connect to {{site.data.keyword.logs_full_notm}}, and logs are not delivered.
{: tsSymptoms}

A firewall or proxy in your environment blocks the outbound connection from {{site.data.keyword.agent}}.
{: tsCauses}

Complete the following steps to resolve the problem:
{: tsResolve}

1. Check your firewall and proxy settings.

2. If a proxy is required to reach {{site.data.keyword.logs_full_notm}}, run the configuration script again with the `--proxy` parameter. Replace `<url>` with the URL of your proxy, for example `http://proxy.example.com:8080`.

   ```sh
   sudo /opt/otelcol-ibm/configure.sh \
     -i <instance_guid> \
     -r <region> \
     -k <api_key> \
     --application-name <app_name> \
     --log-path /var/log/messages \
     --proxy <url>
   ```
   {: codeblock}

For more information about the configuration parameters, see [Configuring the agent](/docs/cloud-logs?topic=cloud-logs-cloud-logs-agent-configure).
