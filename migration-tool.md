---

copyright:
  years:  2024
lastupdated: "2024-07-04"

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


![Overview of migrating to {{site.data.keyword.logs_full_notm}}](/images/migration-tool.png "Overview of migrating to {{site.data.keyword.logs_full_notm}}"){: caption="Figure 1. Overview of migrating to {{site.data.keyword.logs_full_notm}}" caption-side="bottom"}


## Migration tool use cases
{: #migrate-usecases}

You can use the migration tool for:

- Planning your migration.

    You can collect information about {{site.data.keyword.cloud_notm}} resources that are impacted by the migration in an account. The information that is generated includes information about current resources, and Terraform scripts for the new resources. You can use this information to find out what needs to be migrated and define a plan.

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

```sh
ibmcloud plugin install logging
```
{: pre}
