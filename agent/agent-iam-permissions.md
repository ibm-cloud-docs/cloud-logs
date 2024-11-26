---

copyright:
  years:  2024
lastupdated: "2024-11-26"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Setting up IAM permissions for ingestion
{: #agent-iam-permissions}

You must grant `Sender` permissions to the API key or trusted profile that you use to send logs to an {{site.data.keyword.logs_full_notm}} instance.
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


You can also use Trusted Profiles to authenticate {{site.data.keyword.cloud_notm}} resources with an {{site.data.keyword.logs_full_notm}} instance when the resource and the instance are located in the same account.
{: note}

Consider the following information when using IAM API Keys:
- You can grant permissions to a user ID, a service ID, or an access group to send logs to an {{site.data.keyword.logs_full_notm}} instance.
- You must generate a new user API key or a new service ID API key after the permissions to send logs are granted to the access group, service ID, or user ID.
- When you grant permissions via an access group, the users and service IDs that are included in the access group will inherit the permissions.
- Grant permissions to send logs to a user ID for testing purposes only.

Consider the following information when using Trusted Profiles:
- You can only use Trusted Profiles to authenticate {{site.data.keyword.cloud_notm}} resources with an {{site.data.keyword.logs_full_notm}} instance.
- The Trusted Profile and the {{site.data.keyword.logs_full_notm}} instance must be located in the same account.
- You must grant the `Sender` permission to a trusted profile before using it.



## Assigning access to {{site.data.keyword.logs_full_notm}} in the console
{: #agent-iam-permissions-access-ui}
{: ui}

There are two common ways to assign access to {{site.data.keyword.logs_full_notm}} in the console:

* Access groups. You can manage access groups and their access from the **Manage** > **Access (IAM)** > **Access groups** page in the console. For more information, see [Assigning access to a group in the console](/docs/account?topic=account-groups&interface=ui#access_ag).

* Access policies per user. You can manage access policies per user from the **Manage** > **Access (IAM)** > **Users** page in the console. For information about the steps to assign IAM access, see [Managing access to resources](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console).



## Setting up permissions for ingestion by sending directly
{: #agent-iam-permissions-d-cli}
{: cli}

To send logs directly to the {{site.data.keyword.logs_full_notm}} instance, the API key or trusted profile must have the `Sender` role for the {{site.data.keyword.logs_full_notm}} service.

Use the appropriate command for the type of identity:

| Type of identity  | Command |
|-------------------|---------|
| Access group      | `ibmcloud iam access-group-policy-create ACCESS_GROUP --roles Sender --service-name logs` |
| User account      | `ibmcloud iam user-policy-create <username> --roles Sender --service-name logs` |
| Service ID        | `ibmcloud iam service-policy-create <serviceID> --roles Sender --service-name logs` |
| Trusted profile   | `ibmcloud iam tp-policy-create <trustedProfile> --roles Sender --service-name logs` |
{: caption="Command to grant IAM permissions by type of identity" caption-side="top"}

Instead of assigning roles directly to identities, a common strategy is to assign roles to access groups, and add identities as members to those access groups. For more information about access groups, see [setting up access groups.](/docs/account?topic=account-groups&interface=cli)
{: tip}

## Setting up permissions for ingestion by using {{site.data.keyword.logs_full_notm}}
{: #agent-iam-permissions-lr-cli}
{: cli}

If you configure your agent to send logs through the {{site.data.keyword.logs_full_notm}} service, the API key or trusted profile must have the `Writer` role for the {{site.data.keyword.logs_routing_full_notm}} service.

Granting the role can be done by using the `ibmcloud` CLI.

Use the appropriate command for the type of identity:

| Type of identity  | Command |
|-------------------|---------|
| Access group      | `ibmcloud iam access-group-policy-create ACCESS_GROUP --roles Writer --service-name logs` |
| User account      | `ibmcloud iam user-policy-create <username> --roles Writer --service-name logs` |
| Service ID        | `ibmcloud iam service-policy-create <serviceID> --roles Writer --service-name logs` |
| Trusted profile   | `ibmcloud iam tp-policy-create <trustedProfile> --roles Writer --service-name logs` |
{: caption="Command to grant IAM permissions by type of identity" caption-side="top"}

Instead of assigning roles directly to identities, a common strategy is to assign roles to access groups, and add identities as members to those access groups. For more information about access groups, see [setting up access groups.](/docs/account?topic=account-groups&interface=cli)
{: tip}
