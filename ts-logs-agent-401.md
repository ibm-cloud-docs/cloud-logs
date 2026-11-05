---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Status code 401 returned when {{site.data.keyword.agent}} sends logs
{: #troubleshoot-agent-rc401}
{: troubleshoot}
{: support}

A status code 401 is returned when {{site.data.keyword.agent}} attempts to send logs to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

Log delivery fails and the {{site.data.keyword.agent}} live output displays `status: 401`.
{: tsSymptoms}

The API key used by the agent is invalid, expired, or deleted, or the trusted profile ID is not linked to the virtual machine.
{: tsCauses}

Create a new API key or verify your trusted profile ID, and re-run the configuration script with the new credential.
{: tsResolve}

```sh
sudo /opt/otelcol-ibm/configure.sh \
  -i <instance_guid> \
  -r <region> \
  -k <api_key> \
  --application-name <app_name> \
  --log-path /var/log/messages
```
{: codeblock}



