---

copyright:
  years:  2024
lastupdated: "2024-11-28"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Migrating log groups
{: #migration_data_access_rules}

Using the {{site.data.keyword.logs_full}} migration tool you can migrate {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} log groups into {{site.data.keyword.logs_full}} data access rules.
{: shortdesc}

When you run the `ibmcloud loggin migrate create-resources` command, [data access rules](/docs/cloud-logs?topic=cloud-logs-data-access-rules&interface=ui) are created in the {{site.data.keyword.logs_full_notm}} instance based on the log groups defined in the migrated {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance.

A data rule is created for each log group. The data rule is configured with the same name as the log group.

The query creating the original log group cannot be used to create the {{site.data.keyword.logs_full_notm}} data access rules. The query must be manually recreated in [DPXL](/docs/cloud-logs?topic=cloud-logs-dpxl_ref). To assist with the manual migration, the original query from the original log group is included in the created data access rule.

Configuring {{site.data.keyword.iamlong}} (IAM) permissions when using data access rules is similar to configuring IAM policies for log groups. 2 policies are required:
* A policy granting permission on the service.
* A policy for each data access rule granting access to users, access groups, and so on.

    For each data access rule policy, the [`Data Access Reader` role](/docs/cloud-logs?topic=cloud-logs-iam-actions&interface=ui#iam-actions-DataAccessRestrictionReader) in {{site.data.keyword.logs_full_notm}} is required to assign the policy.

When running the {{site.data.keyword.logs_full_notm}} migration tool in `terraform` mode, a directory similar to `/migration-tool/cl/81de6380e6232123c6567c9c8de6dece/manual-tf-files/iam-policies/instanceID` is created with the required policies based on the original {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} IAM permissions. The policy granting permissions on the service is included. You will need to manually apply these policies after migrating the {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance.  You will need to manually create policies for each data access group based on your current configuration.

When running the migration tool in `api` mode, if you have already migrated your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance, you need to run an additional migration command to apply the IAM permissions. This command applies IAM policies for service access. You will need to manually create policies for each data access group based on your current configuration..

```text
ibmcloud logging migrate update-resources --scope SCOPE [--instance-crn CRN] --cl-instance-crn CL-INSTANCE-CRN [--update-iam] --api
```
{: pre}
