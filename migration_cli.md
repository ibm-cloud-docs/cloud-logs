---

copyright:
  years:  2024
lastupdated: "2024-09-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migration CLI
{: #migration_cli}

Use the migration CLI to migrate your {{site.data.keyword.la_full}} or {{site.data.keyword.at_full_notm}} instance configuration to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

This topic is still very much a work in progress and subject to significant change.
{: important}

## Installing the CLI
{: #migration-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the CLI by running the following command:

   ```text
   ibmcloud plugin install logging
   ```
   {: pre}

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use the most current commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}



## ibmcloud logging migrate generate-terraform
{: #logging-migrate-generate-terraform}

Use this command to create Terraform scripts to create new {{site.data.keyword.logs_full_notm}} instances from existing {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instances and migrate the {{site.data.keyword.iamshort}} permissions that are associated with those instances.

This command does not automatically create the new instances. The Terraform scripts must be used with the Terraform CLI or API to create the new instances. To create new instances directly by using a command, use [ibmcloud logging migrate create-resources](#logging-migrate-create-resources).
{: important}

```text
ibmcloud logging migrate generate-terraform --scope SCOPE [--instance-crn CRN] [--service SERVICE] [--iam-scope IAM_ENTITY] [--directory DIRECTORY] 
```
{: pre}

### Command options
{: #generate-terraform-options}

`--scope`|`-s`
:   The scope of the configuration to be migrated.

    `account`
    :   All {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instances in the account.

    `instance`
    :   Migrate only a specific instance. Specify the instance type by using `--service` and the instance [CRN](/docs/account?topic=account-crn) by using `--instance-crn`.

    `iam`
    :   Migrate the {{site.data.keyword.iamshort}} permissions that are associated with the account.

`--instance-crn`|`--crn`
   :   The [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance to be migrated. Required when `--scope instance` is specified. `--instance-crn` does not apply to other `--scope` options.

`--service`|`--sv`
   :   The type of service to migrate. 

       `logdna`
       :   The instance to be migrated is an {{site.data.keyword.la_full_notm}} instance.

       `logdnaat`
       :   The instance to be migrated is an {{site.data.keyword.at_full_notm}} instance.

`--iam-scope`|`--is`

   : The [{{site.data.keyword.iamshort}}](/docs/account) configuration to be migrated. Specify only one. If not specified, `all` is assumed.

     `all`
     :   The entire {{site.data.keyword.iamshort}} configuration that is associated with the account is migrated.

     `users`
     :   Only the {{site.data.keyword.iamshort}} users configuration is migrated.

     `trusted-profiles`
     :   Only the {{site.data.keyword.iamshort}} trusted proviles configuration is migrated.

     `service-ids`
     :   Only the {{site.data.keyword.iamshort}} service IDs configuration is migrated.

     `access-groups`
     :   Only the {{site.data.keyword.iamshort}} access groups configuration is migrated.

     `authorizations`
     :   Only the {{site.data.keyword.iamshort}} authorizations configuration is migrated.

`--directory`
   :   The directory on your local computer where migration files are written. If not specified, the directory where the command is run is used.

### Examples
{: #generate-terraform-examples}

Generate the Terraform to migrate all {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instances in the account.

```text
ibmcloud logging migrate generate-terraform --scope account
```
{: pre}

Generate the Terraform to migrate all {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instances in the account and write the migration files to the directory specified by DIRECTORY.

```text
ibmcloud logging migrate generate-terraform --scope account --directory DIRECTORY
```
{: pre}

Generate the Terraform to migrate the single {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance that is associated with the CRN value.

```text
ibmcloud logging migrate generate-terraform --scope instance --crn CRN
```
{: pre}

Generate the Terraform to migrate all {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instances in the account of the service type SERVICE.

```text
ibmcloud logging migrate generate-terraform --scope account --service SERVICE
```
{: pre}

Generate the Terraform to migrate the {{site.data.keyword.iamshort}} configuration associated with the account.

```text
ibmcloud logging migrate generate-terraform --scope iam
```
{: pre}



## ibmcloud logging migrate create-resources
{: #logging-migrate-create-resources}

You can use this command to migrate {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instances and their associated configurations.

* Use this command to create a new {{site.data.keyword.logs_full_notm}} instance from a single existing {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance.

* Use this command to reconfigure {{site.data.keyword.atracker_full_notm}} targets and routes currently configured to {{site.data.keyword.at_full_notm}} instances to point to newly created {{site.data.keyword.logs_full_notm}} instances.

* Use this command to configure the {{site.data.keyword.logs_full_notm}} instance where platform logs will be sent in the region.. Only one {{site.data.keyword.logs_full_notm}} instance can be configured in each region to receive platform logs.

All {{site.data.keyword.at_full_notm}} instances associated with {{site.data.keyword.atracker_full_notm}} targets and routes must be migrated to {{site.data.keyword.logs_full_notm}} instances before migrating the {{site.data.keyword.atracker_full_notm}} targets and routes.
{: important}

The command generates Terraform similar to the [`generate-terraform` command](#logging-migrate-generate-terraform) and applies the generated Terraform by using a single command.


```text
ibmcloud logging migrate create-resources --scope SCOPE [--instance-crn CRN] [--single] [--instance-name instance-name] [--cos-instance-crn cos-instance-crn] [--cos-kms-key-crn cos-kms-key-crn] [--data-bucket-name data-bucket-name] [--metrics-bucket-name metrics-bucket-name] [--plan-retention plan-retention] [--platform platform] [--instance-resource-group-id instance-resource-group-id] [--region region] [--en-instance-crn en-instance-crn] [--ingestion-key ingestion-key] [--ingress-endpoint-type ingress-endpoint-type] [--api | --terraform] [--directory DIRECTORY] [--predefined-resources] [--force] 
```
{: pre}


### Command options
{: #create-resources-tf-options}

`--scope`|`-s`
:   The scope of the configuration to be migrated.

    `instance`
    :   Migrate only a specific instance. Specify the instance [CRN](/docs/account?topic=account-crn) by using `--instance-crn`.

    `atracker`
    :   Migrate {{site.data.keyword.atracker_full_notm}} targets and routes associated with migrated {{site.data.keyword.at_full_notm}} instances.

        For more information about {{site.data.keyword.atracker_full_notm}} migration, see [Migrating {{site.data.keyword.atracker_full_notm}} routes and targets](/docs/cloud-logs?topic=cloud-logs-migration-atracker).

    `platform-logs`
    :   Sets the target {{site.data.keyword.logs_full_notm}} location within the region where platform logs will be sent.

`--api`|`-a`
:   Use the API method to create {{site.data.keyword.logs_full_notm}} instances and resources. If not specified, `--terraform` is the default.

`--terraform`|`-t`
:   Use the Terraform method to create {{site.data.keyword.logs_full_notm}} instances and resources. If not specified, `--terraform` is the default.

    Terraform is not supported for `--scope platform-logs`.
    {: note}

`--instance-crn`|`--crn`
   :   The [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance to be migrated.


`--instance-name`|`--cl`
   :   The name of the {{site.data.keyword.logs_full_notm}} instance to be created when `--scope atracker` is specified.

`--cos-instance-crn`|`--cos`
   :   The {{site.data.keyword.cos_full_notm}} CRN where buckets are created for the {{site.data.keyword.logs_full_notm}} instance when `--scope atracker` is specified.

`--data-bucket-name`|`--db`
   :   The name of the {{site.data.keyword.cos_full_notm}} data bucket created for the {{site.data.keyword.logs_full_notm}} instance when `--scope atracker` is specified.

`--metrics-bucket-name`|`--mb`
   :   The name of the {{site.data.keyword.cos_full_notm}} metrics bucket created for the {{site.data.keyword.logs_full_notm}} instance when `--scope atracker` is specified.

`--plan-retention`|`--rp`
   :   Sets the [{{site.data.keyword.frequent_search}} retention period](/docs/cloud-logs?topic=cloud-logs-service_plans) for the created {{site.data.keyword.logs_full_notm}} instance. Supported values are `30-days`, `14-days`, or `7-days`. If not specified, `7-days` will be used.

`--platform`|`-p`
   :   If specified, {{site.data.keyword.at_full_notm}} and {{site.data.keyword.logs_full_notm}} instances will be migrated along with any existing {{site.data.keyword.atracker_full_notm}} or {{site.data.keyword.logs_routing_full_notm}} configuration.

`--instance-resource-group-id`|`--rg`

   :   The [resource group](/docs/account?topic=account-rgs&interface=ui) ID to be used when creating the {{site.data.keyword.logs_full_notm}} instance.

`--region`|`-r`
   :   The region where {{site.data.keyword.atracker_full_notm}} targets will be configured.

`--single`
   :   Migrate all existing {{site.data.keyword.at_full_notm}} instances to 1 {{site.data.keyword.logs_full_notm}} instance.

`--instance-resource-group-id`|`--rg`
   :   The resource group ID used when creating the {{site.data.keyword.logs_full_notm}} instance.

`--ingress-endpoint-type`

   :   Defines the ingress endpoint type of the configured {{site.data.keyword.logs_full_notm}} instance to be used to receive platform logs. Valid values are `private` and `public`. If not specified the default is `public`.

       This option is only used when `--scope platform-logs` is specified.

`--en-instance-crn`|`--ecrn`

   : The [CRN](/docs/account?topic=account-crn) of an {{site.data.keyword.en_full_notm}} instance. Migrated alerts will be configured to be sent to this instance. 

   If `--en-instance-crn` is not specified, Terraform files are created to migrate alerts, however manual configuration will have to be done after migration to configure {{site.data.keyword.en_full_notm}} to receive the alerts. If the `--api` option is used, and the user does not specify yes when prompted to configure alerting to {{site.data.keyword.en_full_notm}}, the user will have to manally configure sending alerts to {{site.data.keyword.en_full_notm}}.
   {: important}

`--ingestion-key`|`-k`
   :   The [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-ingestion_key&interface=ui) or [{{site.data.keyword.logs_full_notm}}](/docs/log-analysis?topic=log-analysis-ingestion_key&interface=ui) ingestion key. This key is required to migrate {{site.data.keyword.atracker_full_notm}} or {{site.data.keyword.logs_routing_full_notm}} configurations associated with the instance.

`--directory`|`-d`
   :   The directory on your local computer where migration files are written. If not specified, the directory where the command is run is used.

`--force`|`-f`
   :   Runs the command without further prompting of the user.

### Examples
{: #create-resources-tf-example}

In this example, Terraform is generated for the {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance that is indicated by the `CRN` value and that Terraform applied to create a new {{site.data.keyword.logs_full_notm}} instance.

```text
ibmcloud logging migrate create-resources --scope instance --crn CRN --terraform
```
{: pre}

In this example, Terraform is generated to migrate {{site.data.keyword.atracker_full_notm}} targets and routes associated with migrated {{site.data.keyword.at_full_notm}} instances to the newly created {{site.data.keyword.logs_full_notm}} instances.

```text
ibmcloud logging migrate create-resources --scope atracker --terraform
```
{: pre}

In this example, the API is used to configure the {{site.data.keyword.logs_full_notm}} instance in the region to receive platform logs using a private ingress endpoint.

```text
ibmcloud logging migrate create-resources -s platform-logs -i private 
```
{: pre}


## ibmcloud logging migrate remove-resources-tf
{: #logging-migrate-remove-resources-tf}

Use this command to remove an {{site.data.keyword.logs_full_notm}} instance that was created using the migration Terraform files. All associated resources creating during the migration will also be removed. For example, {{site.data.keyword.cos_full_notm}} buckets and {{site.data.keyword.iamlong}} authorizations associated with the instance will be removed.

```text
ibmcloud logging migrate remove-resources-tf --scope SCOPE --instance-crn CRN [--directory DIRECTORY]
```
{: pre}

### Command options
{: #remove-resources-tf-options}

`--scope`|`-s`
:   The scope of the configuration to be removed.

    `instance`
    :   Migrate only a specific instance. Specify the instance [CRN](/docs/account?topic=account-crn) by using `--instance-crn`.

`--instance-crn`|`--crn`
   :   The [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.logs_full_notm}} instance to be removed.

`--directory`|`-d`
   :   The directory on your local computer where the Terraform migration files exist. If not specified, the directory where the command is run is used.


### Example
{: #remove-resources-tf-example}

In this example, the {{site.data.keyword.logs_full_notm}} instance specified by the `CRN` value is removed using the migration Terraform files in the directory where the command is run. All resources associated with the {{site.data.keyword.logs_full_notm}} instance are removed as well.

```sh
ibmcloud logging migrate remove-resources-tf --scope instance --crn CRN 
```
{: pre}







## ibmcloud logging migrate config
{: #logging-migrate-config}

Use this command to export the {{site.data.keyword.logs_full_notm}} resources from an {{site.data.keyword.logs_full_notm}} instance to a file. You can then use this command to import those resources to a different {{site.data.keyword.logs_full_notm}} instance.

Example resources include views, dashboard, and alerts.

Exported files are written to the `logs/<accountID>/<instanceID>` directory. When running an import you must run the `ibmcloud logging migrate config` command from the directory that contains the `logs/<accountID>/<instanceID>` directory which contains the exported files for the {{site.data.keyword.logs_full_notm}} instance that you want to import.

Imported resources will be added to the {{site.data.keyword.logs_full_notm}} instance.
{: note}


```text
ibmcloud logging migrate config [--crn-destination CRN] --crn-origin CRN [--export | --import] 
```
{: pre}

### Command options
{: #mig-config-options}

`--crn-origin value` | `--crn-org value`
:   The [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.logs_full_notm}} instance whose resources are to be exported or whose resources are to be imported.

`--crn-destination value` | `--crn-des value`
   :   The [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.logs_full_notm}} instance importing the exported resources specified by `--crn-origin`. Required for `--import`.

`--export` | `--ex`
   :   Export the {{site.data.keyword.logs_full_notm}} resources of the `--crn-origin` instance. Mutually exclusive with `--import`.

`--import` | `--im`
   :   Import the {{site.data.keyword.logs_full_notm}} resources of the `--crn-origin` instance. Mutually exclusive with `--export`.


### Examples
{: #mig-config-examples}

In this example the {{site.data.keyword.logs_full_notm}} resources of the CRN instance are exported to a file.

```sh
ibmcloud logging migrate config --export --crn-origin CRN
```
{: pre}

In this example the {{site.data.keyword.logs_full_notm}} resources of the ORIGIN_CRN instance, that were exported in a previous `ibmcloud logging migrate config` command, are imported to the {{site.data.keyword.logs_full_notm}} CRN instance.

```sh
ibmcloud logging migrate config --import --crn-origin ORIGIN_CRN --crn-destination CRN 
```
{: pre}
