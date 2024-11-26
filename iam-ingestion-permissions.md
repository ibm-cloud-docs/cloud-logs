---

copyright:
  years:  2024
lastupdated: "2024-11-26"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Granting IAM permissions for ingestion
{: #iam-ingestion-permissions}

You must grant `Sender` permissions to the API key or trusted profile that you use to request authorization to send logs to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

You can send logs to an {{site.data.keyword.logs_full_notm}} instance by using the Ingestion REST API, or by using the {{site.data.keyword.agent}}.

To send logs to an {{site.data.keyword.logs_full_notm}} instance, you can use as the authentication method any of the following options:
- An IAM API key: The API key is used to open a secure web socket to the {{site.data.keyword.logs_full_notm}} ingestion endpoint to authenticate the {{site.data.keyword.agent}} with the {{site.data.keyword.logs_full_notm}} service.
- A Trusted profile

Choose one of the following options to send logs to an {{site.data.keyword.logs_full_notm}} instance:

| Method sending logs                      | User API key    | Service ID API Key |
|------------------------------------------|-----------------|--------------------|
| By using the REST API                    | supported       | supported          |
| By using the {{site.data.keyword.agent}} | not recommended | supported          |
{: caption="Authorization methods by method sending logs" caption-side="bottom"}

You can also use Trusted Profiles to authenticate {{site.data.keyword.cloud_notm}} resources with an {{site.data.keyword.logs_full_notm}} instance when the compute resource and the instance are located in the same account.
{: note}

## IAM API keys
{: #iam-ingestion-permissions-apikey}

Consider the following information when using IAM API Keys:
- You must grant the `Sender` permission to a user ID, a service ID, or an access group to send logs to an {{site.data.keyword.logs_full_notm}} instance.
- You must generate a new user API key or a new service ID API key after the permissions to send logs are granted to the access group, service ID, or user ID.
- When you grant permissions via an access group, the users and service IDs that are included in the access group will inherit the permissions.
- Grant permissions to send logs to a user ID for testing purposes only.
- When you use an API key as the authorization method of the {{site.data.keyword.agent}}, the {{site.data.keyword.agent}} can be hosted both inside and outside of {{site.data.keyword.cloud}}.


For more information on how to generate an API key, see:
- [Generating an API Key for ingestion by using a service ID for authentication](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).
- [Generating an API Key for ingestion by using a user ID for authentication](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-userid-api-key).


## Trusted Profiles
{: #iam-ingestion-permissions-tps}

Consider the following information when using Trusted Profiles:
- You can only use Trusted Profiles to authenticate {{site.data.keyword.cloud_notm}} resources with an {{site.data.keyword.logs_full_notm}} instance.
- The Trusted Profile, the compute resource, and the {{site.data.keyword.logs_full_notm}} instance must be located in the same account.
- You must grant the `Sender` permission to a trusted profile before using it.

For more information on how to create the Trusted Profile, see [Generating a Trusted Profile for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-trusted-profile).
