---

copyright:
  years:  2024
lastupdated: "2024-04-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating instances in 1 account
{: #migration-account}

The {{site.data.keyword.logs_full}} migration tool is a command line tool that you can use to migrate your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance configuration to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

You can use the Migration tool to create Terraform scripts to migrate an account:

* A new {{site.data.keyword.logs_full_notm}} instance is created for each {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance.
* Tags attached to your instance are added to the new {{site.data.keyword.logs_full_notm}} instance.
* {{site.data.keyword.cos_full_notm}} buckets are created for {{site.data.keyword.logs_full_notm}} use. If Activity Tracker, Monitoring, or Associated key management services are configured, the same configuration is applied to the new buckets.
* The name of the {{site.data.keyword.la_full_notm}} instance or {{site.data.keyword.at_full_notm}} instance is used to name the new {{site.data.keyword.logs_full_notm}} instance.
* An {{site.data.keyword.logs_routing_full_notm}} configuration is created routing log data to the new {{site.data.keyword.logs_full_notm}} instance. (**Not available yet**)
* An {{site.data.keyword.atracker_full_notm}} configuration is created routing auditing events to the new {{site.data.keyword.logs_full_notm}} instance. (**Not available yet**)


You can run the following command to generate the Terraform to migrate 1 account:

```text
ibmcloud logging migrate generate-terraform --scope account
```
{: pre}



## Files generated
{: #migacct-files}

By default the migration tools writes temporary files to the `migration-tool/` directory. You can specify a different directory if required.

### Temporary files
{: #migacct-temp}

Files that are related to the migration of 1 instance of {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance are saved in the `migration-tool/tmp/accountID/instanceID/` directory.

Files are also written with details on resources to be migrated.

| Resource | File |
|----------|------|
| Alerts | `migration-tool/tmp/accountID/instanceID/alerts_summary.json` |
| Views | `migration-tool/tmp/accountID/instanceID/views_summary.json` |
| Notification channels | `migration-tool/tmp/accountID/instanceID/channels_summary.json` |
| Groups | `migration-tool/tmp/accountID/instanceID/groups_summary.json` |
| Exclusion rules | `migration-tool/tmp/accountID/instanceID/exclusion_summary.json`|
| Dashboards (*) | `migration-tool/tmp/accountID/instanceID/dashboards_summary.json`|
| Screens (*) | `migration-tool/tmp/accountID/instanceID/screens_summary.json`|
| Parsing rules (*) | `migration-tool/tmp/accountID/instanceID/rules_summary.json`|
| Archive configuration | `migration-tool/tmp/accountID/instanceID/archive_summary.json` |
{: caption="Resource temporary files" caption-side="bottom"}

(*) Not available yet

You might also find the file `migration-tool/tmp/accountID/instanceID/error.txt` that includes resources when no configuration data existed in the instance.

A file with details of the {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance is available in `migration-tool/tmp/accountID/`. The file name is determined by the type of migrated instance:

* {{site.data.keyword.at_full_notm}} instances: `activity-tracker-instances_summary.json`
* {{site.data.keyword.la_full_notm}} instances: `log-analysis-instances_summary.json`
* {{site.data.keyword.la_full_notm}} instances where the platform logs flag is enabled: `platform-logs-instances_summary.json`

The file `migration-tool/tmp/accountID/instances_map.json` includes information about the {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance and the newly created {{site.data.keyword.logs_full_notm}} instance.

`account_id`
:   The account ID.

`instanceType`
:   Either `logdnaat` or `logdna` where `logdnaat` is an {{site.data.keyword.at_full_notm}} instance and `logdna` is an {{site.data.keyword.la_full_notm}} instance.

`instanceName`
:   The name of the instance.

`instanceID`
:   The ID of the instance.

`instance-crn`
:   The CRN of the instance.

`cl-instance-name`
:   The name of the {{site.data.keyword.logs_full_notm}} instance that is created by the migration.

`cl-instance-crn`
:   The CRN of the {{site.data.keyword.logs_full_notm}} instance that is created by the migration.

`cl-instanceID`
:   The ID of the {{site.data.keyword.logs_full_notm}} instance that is created by the migration.


The directory `migration-tool/tmp/accountID/functional-logs/iam` includes detailed logs related to migration of IAM resources.
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

### Terraform files
{: #migacct-tf}


Terraform files that are related to the migration of 1 instance of {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance are saved in the `/migration-tool/cl/accountID/instanceID/service-type/terraform/tf-directory/cloudlogs.tf` directory.

Valid values for `service-type` are `at` for an Activity Tracker instance, and `la` for a Log Analysis instance.

The `tf-directory` includes the name and region of the instance that you are migrating.

| File name | Information |
|-----------|------|
| `cloudlogs.tf` | Terraform to re-create the instance, attach buckets, and attach tags. |
| `data.tf`  | Terraform to create the data bucket |
| `metrics.tf` | Terraform to create the metrics bucket |
| `alerts.tf` | Terraform to create alerts |
{: caption="Terraform files" caption-side="bottom"}


The directory `/migration-tool/cl/accountID/manual-tf-files/iam-tf-files` includes the following Terraform files:

| File name | Information |
|-----------|------|
| `iam_groups.tf` | Terraform to create policies for {{site.data.keyword.logs_full_notm}} in access groups |
| `iam_profiles.tf` | Terraform to create policies for {{site.data.keyword.logs_full_notm}} in trusted profiles |
| `iam_service_ids.tf` | Terraform to create policies for {{site.data.keyword.logs_full_notm}} in service IDs |
| `iam_users/tf` | Terraform to create policies for {{site.data.keyword.logs_full_notm}} for users |
{: caption="Terraform files for policies" caption-side="bottom"}
