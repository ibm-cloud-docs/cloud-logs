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

You can send logs to an {{site.data.keyword.logs_full_notm}} instance by using the Ingestion REST API, or by using the {{site.data.keyword.agent}}.
{: shortdesc}

To send logs by using the Ingestion REST API, you must get an {{site.data.keyword.iamlong}} (IAM) access token to authenticate your requests. Make sure the entity that you use to obtain the access token has the `Sender` role for the {{site.data.keyword.logs_full_notm}} service.


To send logs to an {{site.data.keyword.logs_full_notm}} instance, you can use as the authentication method any of the following options:
- An IAM API key: The API key is used to open a secure web socket to the {{site.data.keyword.logs_full_notm}} ingestion endpoint to authenticate the {{site.data.keyword.agent}} with the {{site.data.keyword.logs_full_notm}} service.
- A Trusted profile
You must grant `Sender` permissions to the API key or trusted profile that you use to request authorization to send logs to an {{site.data.keyword.logs_full_notm}} instance by using the {{site.data.keyword.agent}}.

Choose one of the following options to send logs to an {{site.data.keyword.logs_full_notm}} instance by using the {{site.data.keyword.agent}}:

| Environment                                                 | Service ID API Key | Trusted Profile    |
|-------------------------------------------------------------|--------------------|--------------------|
| Kubernetes cluster in {{site.data.keyword.cloud_notm}}      | supported          | supported          |
| OpenShift cluster in {{site.data.keyword.cloud_notm}}       | supported          | supported          |
| Virtual Server for VPC in {{site.data.keyword.cloud_notm}}  | supported          | supported          |
| Kubernetes cluster on-prem or in other clouds               | supported          | Not supported      |
| OpenShift cluster on-prem or in other clouds                | supported          | Not supported      |
| Linux server on-prem or in other clouds                     | supported          | Not supported       |
{: caption="Authorization methods by method sending logs" caption-side="bottom"}

You can only use Trusted Profiles to authenticate {{site.data.keyword.cloud_notm}} resources with an {{site.data.keyword.logs_full_notm}} instance when the compute resource and the instance are located in the same account.
{: note}

To send logs from a Kubernetes cluster that is provisioned in a different {{site.data.keyword.cloud_notm}} account than the {{site.data.keyword.logs_full_notm}} instance, you can only use a service ID API key as the agent's authorization method.
{: note}

It is not recommended the use of user ID API keys for the {{site.data.keyword.agent}} configuration.
{: note}


## Setting up permissions for ingestion
{: #iam-ingestion-permissions-role-cli}

To send logs directly to the {{site.data.keyword.logs_full_notm}} instance, the API key or trusted profile must have the `Sender` role for the {{site.data.keyword.logs_full_notm}} service.

Use the appropriate command for the type of identity:

| Type of identity  | Command |
|-------------------|---------|
| Service ID        | `ibmcloud iam service-policy-create <serviceID> --roles Sender --service-name logs` |
| Trusted profile   | `ibmcloud iam tp-policy-create <trustedProfile> --roles Sender --service-name logs` |
{: caption="Command to grant IAM permissions by type of identity" caption-side="top"}



## Generating IAM API keys
{: #iam-ingestion-permissions-apikey}

Consider the following information when using IAM API Keys:
- You must grant the `Sender` permission to a user ID, a service ID, or an access group to send logs to an {{site.data.keyword.logs_full_notm}} instance.
- You must generate a new user API key or a new service ID API key after the permissions to send logs are granted to the access group, service ID, or user ID.
- When you grant permissions via an access group, the users and service IDs that are included in the access group will inherit the permissions.
- Grant permissions to send logs to a user ID for testing purposes only.
- When you use an API key as the authorization method of the {{site.data.keyword.agent}}, the {{site.data.keyword.agent}} can be hosted both inside and outside of {{site.data.keyword.cloud}}.


For more information on how to generate an API key, see [Generating an API Key for ingestion by using a service ID for authentication](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).


## Creating Trusted Profiles
{: #iam-ingestion-permissions-tps}

Consider the following information when using Trusted Profiles:
- You can only use Trusted Profiles to authenticate {{site.data.keyword.cloud_notm}} resources with an {{site.data.keyword.logs_full_notm}} instance.
- The Trusted Profile, the compute resource, and the {{site.data.keyword.logs_full_notm}} instance must be located in the same account.
- You must grant the `Sender` permission to a trusted profile before using it.

For more information on how to create the Trusted Profile, see [Generating a Trusted Profile for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-trusted-profile).
