---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.agent}} service stops right after starting
{: #troubleshoot-agent-service-stops}
{: troubleshoot}
{: support}

The `otelcol-ibm` service for {{site.data.keyword.agent}} stops right after it starts.
{: shortdesc}

The `otelcol-ibm` service stops shortly after you start it, and logs are not delivered to {{site.data.keyword.logs_full_notm}}.
{: tsSymptoms}

The service stops for one of the following reasons:

- When you install {{site.data.keyword.agent}}, the service starts automatically before you provide your instance GUID, region, and credentials. Without these values, the service cannot start and stops.
- The permissions or ownership of the credentials file `/etc/otelcol-ibm/env` are incorrect.
- The configuration file contains an error.
{: tsCauses}

Check the service output, configure the agent, and restart the service. Complete the following steps:
{: tsResolve}

1. Run the following command to display the last 50 lines of the service output. The first error line identifies the cause.

```sh
   journalctl -u otelcol-ibm -n 50
   ```
    {: pre}

2. Run the configure script with your instance GUID, region, and credentials. For example, to collect log files by using an API key, run the following command. For other options, such as a trusted profile or Rsyslog, see [Configuring the agent](/docs/cloud-logs?topic=cloud-logs-cloud-logs-agent-configure).

   ```sh
   sudo /opt/otelcol-ibm/configure.sh \
     -i <instance_guid> \
     -r <region> \
     -k <api_key> \
     --application-name <app_name> \
     --log-path <log_file_path>
   ```
   {: pre}

3. Verify that only the owner can read the credentials file `/etc/otelcol-ibm/env` and that the `otelcol` user owns it.

   ```sh
   ls -l /etc/otelcol-ibm/env
   ```
   {: pre}

   The permissions must be `-rw-------`, and the owner must be `otelcol`.

4. Clear the failed state and restart the service.

   ```sh
   sudo systemctl reset-failed otelcol-ibm
   sudo systemctl restart otelcol-ibm
   ```
   {: pre}

5. Verify that the service is running.

   ```sh
   systemctl status otelcol-ibm
   ```
   {: pre}

   The status must show `active (running)`.

6. If the service still stops, run the following command to display the last 50 lines of the service output. For information about contacting support, see [Contacting IBM Support](/docs/support?topic=support-using-avatar).

