---

copyright:
  years:  2024
lastupdated: "2024-06-24"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migration tool
{: #migration-tool}

The {{site.data.keyword.logs_full}} migration tool is a command line tool that you can use to migrate your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance configuration to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}


The tool requires minimal user interaction. {{site.data.keyword.iamshort}} authentication and APIs are used to get the details about your current {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance.

The migration tool migrates only configuration information. No data is migrated from {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instances to the new {{site.data.keyword.logs_full_notm}} instances.
{: important}



## Migration tool use cases
{: #migrate-usecases}

You can use the migration tool for:

- Planning your migration.

    You can collect information about {{site.data.keyword.cloud_notm}} resources that are impacted by the migration in an account. The information that is generated includes information about current resources, and terraform scripts for the new resources. You can use this information to find out what needs to be migrated and define a plan.

- Migrating 1 instance and its subresources.

    When you migrate 1 instance, you also get information about current resources, and terraform scripts for the new resources.

- Preparing the migration of {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instances in a region where {{site.data.keyword.logs_full_notm}} is not available yet.


## Using the migration tool
{: #migrate-provides}

The migration tool is a CLI tool that can be used to migrate 1 or all {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instances in an account based on the existing {{site.data.keyword.la_full}} or {{site.data.keyword.at_full_notm}} configuration.

You can use the tool to:

* Migrate {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instance configurations.

* Migrate {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} resources such as views, dashboards, alerts, exclusion rules, archiving configuration and more.

* Migrate the archiving configuration that is enabled in a {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance.

* Migrate alerting and configure the Event Notifications integration.

The tool generates exception reports that indicate items that cannot be migrated automatically and require manual steps. Exceptions can include:

* Resources requiring user validation before migration. Examples of these include custom catalogs and IAM permissions.

* Migrated resources that require more user tasks, such as regenerating API keys for new {{site.data.keyword.logs_full_notm}} resources.

* Resources that are not part of the migration tool, such as configuring a cross-account {{site.data.keyword.cos_full_notm}} bucket or bucket outside of {{site.data.keyword.cloud_notm}}.

Terraform artifacts are created that can be used to create new {{site.data.keyword.logs_full_notm}} instances. Terraform on {{site.data.keyword.cloud_notm}} enables predictable and consistent creation of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multitier cloud environments by following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the creation, update, and deletion of your {{site.data.keyword.logs_full_notm}} instances by using the HashiCorp Configuration Language (HCL).

## Installing the migration tool
{: #migration-installing}

The migration tool is deployed as part of the `logging` CLI plug-in in {{site.data.keyword.cloud_notm}}.

To install the logging plug-in, run the following commands:

1. Add the repo for plug-ins in stage

    ```sh
    ibmcloud plugin repo-add stage https://plugins.test.cloud.ibm.com
    ```
    {: pre}

2. Install the plug-in

    ```sh
    ibmcloud plugin install logging -r stage
    ```
    {: pre}



## Temporary files
{: #migration-temp-files}

By default the migration tools writes temporary files to the `migration-tool/` directory. You can specify a different directory if required.

Files that are related to the migration of {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instances are saved in the `migration-tool/tmp/accountID/instanceID/` directory. The file name is determined by the type of migrated instance:

* {{site.data.keyword.at_full_notm}} instances: `activity-tracker-instances_summary.json`
* {{site.data.keyword.la_full_notm}} instances: `log-analysis-instances_summary.json`
* {{site.data.keyword.la_full_notm}} instances where the platform logs flag is enabled: `platform-logs-instances_summary.json`

The `migration-tool/tmp/accountID/instances_map.json` file includes information about all the instances to be migrated in the account. This file includes the following variables:

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

The `migration-tool/tmp/accountID/iam_summary.json` file includes information about the {{site.data.keyword.iamshort}} resources to be migrated in the account.

Files are written with details on resources to be migrated.

| Resource | File |
|----------|------|
| Alerts | `migration-tool/tmp/accountID/instanceID/alert_summary.json` |
| Views | `migration-tool/tmp/accountID/instanceID/views_summary.json`|
| Notification channels | `migration-tool/tmp/accountID/instanceID/channels_summary.json` |
| Groups | TBD |
| Exclusion rules | `migration-tool/tmp/accountID/instanceID/exclusion_summary.json` |
| Dashboards | `migration-tool/tmp/accountID/instanceID/dashboards.json` |
| Screens | `migration-tool/tmp/accountID/instanceID/screens.json`|
| Parsing rules | `migration-tool/tmp/accountID/instanceID/parsing_rules_summary.json` |
| Archive configuration | `migration-tool/tmp/accountID/instanceID/archive_summary.json` |
| Index rate alerts | N/A |
{: caption="Table 1. Resource temporary files" caption-side="bottom"}


## Output files
{: #migration-out-files}

The migration tool generates output files that you can use to determine future actions to be taken along with Terraform files that can be used to create more instances.

### Excepion reports
{: #migration-ex-report}

The tool generates exception reports for each migrated instance.

The reports are saved in the `migration-tool/cl/accountID/instanceID/` directory.

| File | Description |
|-----------|-------------|
| `migration_exception_instanceID_resourceType.json` | Exception report for migrated {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instances |
| `migration_exception_instanceID_iam.json` | Exception report for migrated {{site.data.keyword.iamshort}} resources |
| `migration_exception_instanceID_alerts.json` | Exception report for migrated alerts |
{: caption="Table 2. Exception report locations" caption-side="bottom"}


### Terraform files
{: #migration-tf-files}

The migration tool generates Terraform files that can be used to create more instances based on the same migrated configurations.

| Directory | Description |
|-----------|-------------|
| `migration-tool/cl/accountID/instanceID/at/terraform/` | Directory for migrated {{site.data.keyword.at_full_notm}} instances |
| `migration-tool/cl/accountID/instanceID/la/terraform/` | Directory for migrated {{site.data.keyword.la_full_notm}} instances |
| `migration-tool/cl/accountID/instanceID/la-platform/terraform/` | Directory for migrated {{site.data.keyword.la_full_notm}} instances that receive platform logs |
| `migration-tool/cl/accountID/instanceID/terraform/` | Directory for migrated {{site.data.keyword.iamshort}} resources |
| `migration-tool/cl/accountID/instanceID/resourcesType/terraform/` | Directory for migrated resources |
| `migration-tool/cl/accountID/instanceID/alerts/terraform/` | Directory for migrated alerts |
| `migration-tool/cl/accountID/instanceID/views/terraform/` | Directory for migrated views |
{: caption="Table 3. Terraform file locations" caption-side="bottom"}




## Next steps
{: #migration-nextsteps}

- [Migrating 1 account](/docs/cloud-logs?topic=cloud-logs-migration-account)
- [Migrating 1 instance](/docs/cloud-logs?topic=cloud-logs-migration-instance)
- [Migrating IAM](/docs/cloud-logs?topic=cloud-logs-migration-iam)
- [Migrating {{site.data.keyword.at_short}} instances](/docs/cloud-logs?topic=cloud-logs-migration-at)
- [Migrating {{site.data.keyword.la_short}} instances](/docs/cloud-logs?topic=cloud-logs-migration-la)
