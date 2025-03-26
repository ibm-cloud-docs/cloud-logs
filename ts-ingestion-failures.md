---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-26"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# I think some of my data is not reaching my {{site.data.keyword.logs_full_notm}} instance. What can I look for to determine possible ingestion failures?
{: #ts-ingestion-failures}
{: troubleshoot}
{: support}

You are monitoring your environment by using {{site.data.keyword.logs_full}} and want to check for issues that affect the ingestion of data to the system.
{: shortdesc}

You believe that data might not be reaching your {{site.data.keyword.logs_full_notm}} instance.
{: tsSymptoms}

Multiple causes can exist where data is not ingested by {{site.data.keyword.logs_full_notm}}.
{: tsCauses}

The following issues can cause data ingestion problems in your {{site.data.keyword.logs_full_notm}} instance.
{: tsResolve}

**Retry limit is exceeded.**

Check for logs in the {{site.data.keyword.logs_full_notm}} UI with the string `could not send data - this batch will not be retried`.

The problem can be due to exceeding the configured retry limit or due to permission issues.

When the {{site.data.keyword.agent}} receive a `403` error from {{site.data.keyword.logs_full_notm}}, a retry error is returned. Check that your [IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions) are properly configured.

If the ingestion permissions are properly configured, you might need to change the `Retry_limit` in the [output plug-in parameters](/docs/cloud-logs?topic=cloud-logs-agent-plugin-parameters).

**Logs are dropped.**

Check for logs in the {{site.data.keyword.logs_full_notm}} UI starting with the string `ICL dropped logs`.

The {{site.data.keyword.agent}} retries sending data to {{site.data.keyword.logs_full_notm}} if the {{site.data.keyword.agent}} does not receive a `200 OK` response.

However, sometimes {{site.data.keyword.logs_full_notm}} sends a `200 OK` and writes a message in the response body that not all logs were accepted.

For example, logs can be dropped if they are older than a specific threshold.

The message from the {{site.data.keyword.agent}} contains the reason why the logs were dropped.

**IAM cannot be reached.**

Check the logs for messages that {{site.data.keyword.iamshort}} (IAM) cannot be reached. Messages can include `received message in token library` or `Failed to obtain token`.

When IAM cannot be reached, the {{site.data.keyword.agent}} cannot get a token to send logs.

This problem could be due to incorrect permissions or network issues.

For example, you might be using an API key that does not exist. Or, a firewall is in place that is blocking the {{site.data.keyword.agent}} from reaching the IAM endpoint.

Check your [IAM permissions](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions) and API key and correct if necessary. If due to a network issue, resolve the network issue.

**Pods are restarting or not starting at all.**

If {{site.data.keyword.agent}} pods are frequently restarting, or not starting at all, check for memory consumption of the {{site.data.keyword.agent}} and review the logs for other errors.
