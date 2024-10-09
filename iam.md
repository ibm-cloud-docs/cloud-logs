---

copyright:
  years:  2024
lastupdated: "2024-10-09"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Getting started with IAM
{: #iam}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.cloud_notm}}. Access to {{site.data.keyword.logs_full_notm}} instances for users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).
{: shortdesc}

The access policy that you assign users in your account determines what actions a user can perform within the context of the service or specific instance that you select. The allowable actions are customized and defined by {{site.data.keyword.logs_full_notm}} as operations that are allowed to be performed on the service. An action is mapped to an IAM platform or service role that you can assign to a user.

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned. 
{: important}

## {{site.data.keyword.cloud_notm}} platform roles
{: #iam-platform}

The following table detail actions that are mapped to platform roles.

Platform roles enable users to perform tasks on service resources at the platform level, for example, assign user access for the service, create or delete instances, and bind instances to applications.

Review the following tables that outline what types of tasks each role allows for when you're configuring {{site.data.keyword.logs_full_notm}} in your account.

Use the following table to identify the **Account management** **{{site.data.keyword.logs_full_notm}}** platform roles that you can grant a user in the {{site.data.keyword.cloud_notm}} to run any of the following platform actions:

| Platform role            | Description of actions |
|--------------------------|------------------------|
| Viewer                   | As a viewer, you can view service instances, but you cannot modify them. |
| Operator                 | As an operator, you can perform platform actions required to configure and operate service instances, such as viewing a service's dashboard. |
| Editor                   |As an editor, you can perform all platform actions except for managing the account and assigning access policies. |
| Administrator            | As an administrator, you can perform all platform actions based on the resource where the role is being assigned, including assigning access policies to other users. |
| Service Configuration Reader | As a service configuration reader you can read the service configuration for governance management |
| Key Manager | As a key manager you can manage resource keys, for example creating a new resource key for a resource instance |
{: caption="IAM platform roles for {{site.data.keyword.logs_full_notm}}" caption-side="top"}


## {{site.data.keyword.cloud_notm}} service roles
{: #iam-service}

The following table lists the service roles available in {{site.data.keyword.cloud_notm}}.

| Service role       | Description            |
|--------------------|------------------------|
| Manager            | As a manager, you have permissions beyond the writer role to complete privileged actions such as managing data usage metrics, data access rules, TCO policies, enrichments, events to metrics, and version benchmark tags. |
| Writer             | As a writer, you have permissions beyond the reader role such as the ability to manage actions, alerts and incidents, dashboards and views, enrichments, parsing rules, and webhooks or the ability to view analytics, data access rules, and TCO policies. |
| Reader             | As a reader, you can perform read-only actions on the data such as querying logs and viewing dashboards. |
| Sender             | As a sender, you can send logs to your {{site.data.keyword.logs_full_notm}} service instance - but not query or tail logs. This role is meant to be used by agents and routers sending logs. |
| Data Access Reader | With data access reader permissions, you can access log data that is defined by specific rules. These rules are set using the Data Access Rule attribute. |
{: caption="IAM service roles for {{site.data.keyword.logs_full_notm}}" caption-side="top"}


## {{site.data.keyword.cloud_notm}} resource attributes with dynamic values
{: #iam-resource-attributes-dynamic}

The following table lists the available {{site.data.keyword.cloud_notm}} resource attributes with dynamic values.

| Resource attribute           | Value  |
|--------------------------|------------------------|
| Data Access Rule | Specify which rule to use to restrict access to logs. This attribute must be associated with the Data Access Reader service role. |
{: caption="Resource attributes for {{site.data.keyword.logs_full_notm}}" caption-side="top"}

## IAM platform actions
{: #iam-platform-actions}

You can assign access for the following platform actions.

| Action | Description |
|--------|------------|
| `cbr.rule.create` | Create context-based restriction rules. |
| `cbr.rule.delete` | Delete context-based restriction rules |
| `cbr.rule.read` | View context-based restriction rules. |
| `cbr.rule.update` | Update context-based restriction rules. |
| `global-search-tagging.resource.read` | Find resources using the global search and tagging search API. |
| `global-search-tagging.tag.attach-user-tag` | Attach a user tag to a resource. |
| `global-search-tagging.tag.detach-user-tag` | Detach a user tag from a resource. |
| `global-search-tagging.tag.attach-access-tag` | Attach access management tags to a resource. |
| `global-search-tagging.tag.detach-access-tag` | Detach access management tags to from a resource. |
| `iam.delegationPolicy.create` | Create a policy that can be delegated to another service. |
| `iam.delegationPolicy.update` | Update a policy that can be delegated to another service. |
| `iam.policy.create` | Create policies. |
| `iam.policy.delete` | Delete policies. |
| `iam.policy.read` | View policies.  |
| `iam.policy.update` | Update policies. |
| `iam.service.read` | View services. |
| `iam.role.assign` | Assign roles to policies. |
| `iam.role.read` | View roles. |
{: caption="IAM platform actions" caption-side="top"}


## IAM service actions
{: #iam-service-actions}

Ror information about {{site.data.keyword.logs_full_notm}} actions by role, see [IAM actions by role](/docs/cloud-logs?topic=cloud-logs-iam-actions).


## Assigning access to {{site.data.keyword.logs_full_notm}}
{: #iam-assign-access-how}

For details on assigning access, see [Granting access to {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-iam-assign-access&interface=ui).

## How do I know which access policies are set for me?
{: #iam_accesspolicy}

You can see which access policies are set for you in the [{{site.data.keyword.cloud_notm}} UI](https://cloud.ibm.com/){: external} console.

1. Go to [Access IAM users](https://cloud.ibm.com/iam/users){: external}.
2. Click your name in the user table.
3. Click the **Access > Access policies** tab to see your access policies.
4. Click the **Access > Access groups** tab to see the access groups where you are a member. Check the policies for each group.
