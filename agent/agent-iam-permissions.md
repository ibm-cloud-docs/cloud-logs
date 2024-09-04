---

copyright:
  years:  2024
lastupdated: "2024-09-04"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Setting up IAM permissions for ingestion
{: #agent-iam-permissions}

You must grant permissions to the API key or trusted profile that you use to send logs to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

To set the permissions on the API key or trusted profile that you use to send logs to the {{site.data.keyword.logs_full_notm}} instance, the API key or trusted profile must have the `Sender` role for the {{site.data.keyword.logs_full_notm}} service if you configure your agent to send logs directly to the {{site.data.keyword.logs_full_notm}} service.

Trusted profiles are not supported on Linux.
{: note}

You can grant premissions to:
- An access group: The users and service IDs that are included in the access group will inherit the permissions. You must generate a user API key or a service ID API key after the permissions to send logs are granted to the access group.
- User ID: You must grant the permissions and then generate the API key that you can use to send logs. Use this option for testing purposes only.
- Service ID: You must grant the permissions and then generate the API key that you can use to send logs.
- Trusted Profile: You must grant the permissions to the trusted profile before using it.

To see what IAM roles are available for {{site.data.keyword.logs_full_notm}}, see [managing IAM access](/docs/cloud-logs?topic=cloud-logs-iam).

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
{: caption="Table 1. Command to grant IAM permissions by type of identity" caption-side="top"}

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
{: caption="Table 1. Command to grant IAM permissions by type of identity" caption-side="top"}

Instead of assigning roles directly to identities, a common strategy is to assign roles to access groups, and add identities as members to those access groups. For more information about access groups, see [setting up access groups.](/docs/account?topic=account-groups&interface=cli)
{: tip}
