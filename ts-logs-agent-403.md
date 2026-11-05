---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Status code 403 returned when {{site.data.keyword.agent}} sends logs
{: #troubleshoot-agent-rc403}
{: troubleshoot}
{: support}

A status code 403 is returned when {{site.data.keyword.agent}} attempts to send logs to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

Log delivery fails and the {{site.data.keyword.agent}} live output displays `status: 403`.
{: tsSymptoms}

The API key or trusted profile that is used by the agent lacks the `Sender` role on the {{site.data.keyword.logs_full_notm}} instance.
{: tsCauses}

Update the access policy in {{site.data.keyword.iamshort}} (IAM) to grant the `Sender` role to the identity that the agent uses. Use the command that matches your type of identity.
{: tsResolve}

If you use a service ID API key, generate a new API key after the `Sender` role is granted. Then, re-run the configuration script with the new key.

```sh
sudo /opt/otelcol-ibm/configure.sh \
  -i <instance_guid> \
  -r <region> \
  -k <api_key> \
  --application-name <app_name> \
  --log-path /var/log/messages
```
{: codeblock}

For more information, see [Granting IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).
