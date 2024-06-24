---

copyright:
  years:  2024
lastupdated: "2024-04-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migrating 1 instance with the migration tool
{: #migration-instance}

The {{site.data.keyword.logs_full}} migration tool is a command line tool that you can use to migrate 1 {{site.data.keyword.la_full_notm}} instance or {{site.data.keyword.at_full_notm}} instance and its configuration to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

You can use the Migration tool to create Terraform scripts to migrate 1 {{site.data.keyword.la_full_notm}} instance or {{site.data.keyword.at_full_notm}} instance and its configuration:

* A new {{site.data.keyword.logs_full_notm}} instance is created for each {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance.
* Tags attached to your instance are added to the new {{site.data.keyword.logs_full_notm}} instance.
* {{site.data.keyword.cos_full_notm}} buckets are created for {{site.data.keyword.logs_full_notm}} use. If Activity Tracker, Monitoring, or Associated key management services are configured, the same configuration is applied to the new buckets.
* The name of the {{site.data.keyword.la_full_notm}} instance or {{site.data.keyword.at_full_notm}} instance is used to name the new {{site.data.keyword.logs_full_notm}} instance.
* An {{site.data.keyword.logs_routing_full_notm}} configuration is created routing log data to the new {{site.data.keyword.logs_full_notm}} instance. (**Not available yet**)


## Generate the TF to migrate 1 instance
{: #mig1instance-gen}

You can run the following command to generate the Terraform to migrate 1 instance:

```text
ibmcloud logging migrate generate-terraform --scope instance --crn CRN
```
{: pre}

## Prereq before you apply the Terraform
{: #mig1instance-prereq}

You must define a S2S authorization between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}} before you run the migration. Requiring the definition will be fixed in the next update of the CLI command.

```text
ibmcloud iam authorization-policy-create logs cloud-object-storage "Writer"
```
{: pre}


## Migrate 1 instance in a supported region by applying Terraform
{: #mig1instance-supported}

Complete the following steps:

1. To apply the Terraform scripts, you must export `IC_API_KEY` with an API key that has permissions to create and manage an instance of {{site.data.keyword.logs_full_notm}}.

    ```text
    export IC_API_KEY=xxxxxx
    ```
    {: pre}

    The API key must have permissions to create instances, create buckets, and manage {{site.data.keyword.logs_full_notm}} instances.{: note}

2. Run the command to generate and apply the Terraform files:

    ```text
    ibmcloud logging migrate create-resources-tf --scope instance --instance-crn CRN --terraform -f
    ```
    {: pre}

    When you are asked if you want to apply the Terraform scripts, make any changes that you need to the Terraform files that are located in `/migration-tool/cl/accountID/instanceID/service-type/terraform/tf-directory/`. Save the changes.

    Then, enter `yes` to apply the Terraform scripts.



## Preparing migration of 1 instance in a nonsupported region
{: #mig1instance-nonsupported}


Complete the following steps:

1. To apply the Terraform scripts, you must export `IC_API_KEY` with an API key that has permissions to create and manage an instance of {{site.data.keyword.logs_full_notm}}.

    ```sh
    export IC_API_KEY=xxxxxx
    ```
    {: pre}

    The API key must have permissions to create instances, create buckets, and manage {{site.data.keyword.logs_full_notm}} instances.{: note}

2. Run the command to generate and apply the Terraform files:

    ```text
    ibmcloud logging migrate create-resources-tf --scope instance --instance-crn CRN --terraform -f
    ```
    {: pre}

    When you are asked if you want to apply the Terraform scripts, edit the file that is located in `/migration-tool/cl/accountID/instanceID/service-type/terraform/tf-directory/cloudlogs.tf`. Modify the location to a supported one where you want to test migration of that instance. Save the change.

    Valid values for `service-type` are `at` for an Activity Tracker instance, and `la` for a Log Analysis instance.

    The `tf-directory` includes the name and region of the instance that you are migrating.

    Then, enter `yes` to apply the Terraform scripts.

## Known issues
{: #mig1instance-known}

- If you have a `/migration-tool/` directory with assets that are generated from a previous run of the command for migrate 1 instance, you must provide a different directory. If you do not provide a different directory, your migration reports errors.

- Currently, {{site.data.keyword.logs_full_notm}} alerts Terraform is not available in production. Remove the `alerts.tf` file before you apply the Terraform script.


## Files generated
{: #mig1instance-files}

By default the migration tools writes temporary files to the `migration-tool/` directory. You can specify a different directory if required.

### Temporary files
{: #mig1instance-temp}

Files that are related to the migration of 1 instance of {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance are saved in the `migration-tool/tmp/accountID/instanceID/` directory.

Files are written with details on resources to be migrated.

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

You might also find the file `migration-tool/tmp/accountID/instanceID/error.txt` that includes resources when no configuration data exists in the instance.

A file with details of the {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance is available in `migration-tool/tmp/accountID/`. The file name is determined by the type of migrated instance:

* {{site.data.keyword.at_full_notm}} instances: `activity-tracker-instances_summary.json`
* {{site.data.keyword.la_full_notm}} instances: `log-analysis-instances_summary.json`
* {{site.data.keyword.la_full_notm}} instances where the platform log flag is enabled: `platform-logs-instances_summary.json`

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




### Terraform files
{: #mig1instance-tf}


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
