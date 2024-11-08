---

copyright:
  years:  2024
lastupdated: "2024-11-07"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating IAM resources
{: #migration-iam}

The {{site.data.keyword.logs_full}} migration tool is a command line tool that you can use to migrate your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance configuration to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}


Run the migration tool command to create the IAM policies that are identified for migration when migrating one instance:

```text
ibmcloud logging migrate create-resources --scope instance ....
```
{: pre}

The folder `/cl/accountID/manual-tf-files/iam-policies/` is created. In this directory, you can find the Terraform files to migrate the IAM policies that are identified for the instance that is being migrated.

Notice that IAM policies are not applied automatically. You must apply them after you reeview the files.

## Getting info on IAM permissions for instances that must be migrated
{: #migiam-files-acc}


You can also run the following command to find out what IAM resources in the account you will need to migrate and get Terraform for IAM resources that the tool can provide to help you migrate IAM resources:

```text
ibmcloud logging migrate generate-terraform --scope iam
```
{: pre}




### Files generated
{: #migiam-files}

By default the migration tools writes temporary files to the `migration-tool/` directory. You can specify a different directory if required.

#### Temporary files
{: #migiam-temp}


The directory `migration-tool/tmp/accountID/functional-logs/iam` includes detailed logs that are related to the migration of IAM resources.

The file `migration-tool/tmp/accountID/functional-logs/iam/iam_functional_exception_report` includes the list of resources and migration status.

The directory `migration-tool/tmp/accountID/` includes the following information:

| File name | Information |
|-----------|------|
| `iam_exception_report.json` | Information on resources that need attention before migration |
| `iam_groups_summary.json` | Information on access groups that need to be migrated |
| `iam_s2s-cos-authorizations-summary.json` | Information on service to service authorizations that need to be migrated |
| `iam_s2s-kms-authorizations-summary.json` | Information on KMS-COS authorizations that you need for migrating resources |
| `iam_service_ids_summary.json` | Information on service IDs that need to be migrated |
| `iam_trusted_profiles_summary.json` | Information on trusted profiles that need to be migrated |
| `iam_users_summary` | Information on users that need to be migrated |
{: caption="Temporary files" caption-side="bottom"}

#### Terraform files
{: #migiam-tf}

The directory `/migration-tool/cl/accountID/manual-tf-files/iam-tf-files` includes the following Terraform files:

| File name | Information |
|-----------|------|
| `iam_groups.tf` | Terraform to create policies for {{site.data.keyword.logs_full_notm}} in access groups |
| `iam_profiles.tf` | Terraform to create policies for {{site.data.keyword.logs_full_notm}} in trusted profiles |
| `iam_service_ids.tf` | Terraform to create policies for {{site.data.keyword.logs_full_notm}} in service IDs |
| `iam_users/tf` | Terraform to create policies for {{site.data.keyword.logs_full_notm}} for users |
{: caption="Terraform files" caption-side="bottom"}
