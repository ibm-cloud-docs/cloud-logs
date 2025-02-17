---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-13"

keywords:

subcollection: cloud-logs

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for using the Migration Tool
{: #migration-faq}

Frequently asked questions about the Migration Tool.
{: shortdesc}

## What is the difference between the command to `generate-resources` and the command to `create-resources`?
{: #mig_faq_1}
{: faq}

The command `ibmcloud logging migrate generate-resources` is the initial command released with the migration tool to help you plan the migration of instances in your account.

The command `ibmcloud logging migrate create-resources` is the command that you should use to migrate your instances.

Both commands generate the Terraform files that can be applied to migrate the instance.

## Where do I start to migrate an {{site.data.keyword.at_full_notm}} instance?
{: #mig_faq_2}
{: faq}

To migrate an {{site.data.keyword.at_full_notm}} instance, see [Template for migrating {{site.data.keyword.at_full_notm}} instances in the account](/docs/cloud-logs?topic=cloud-logs-template-migration-at).

## Where do I start to migrate an {{site.data.keyword.la_full_notm}} instance?
{: #mig_faq_3}
{: faq}

To migrate an {{site.data.keyword.la_full_notm}} instance, see [Template for tasks for migrating {{site.data.keyword.la_full_notm}} instances collecting logs in the account](/docs/cloud-logs?topic=cloud-logs-template-migration-logs).

## Where do I start to migrate an {{site.data.keyword.la_full_notm}} instance that is configured to receive platform logs?
{: #mig_faq_4}
{: faq}

To migrate an {{site.data.keyword.la_full_notm}} instance that is configured to receive [platform logs](/docs/log-analysis?topic=log-analysis-config_svc_logs&interface=ui), see [Template for migrating Log Analysis instances with platform logs flag enabled in the account](/docs/cloud-logs?topic=cloud-logs-template-migration-la).


## Can I migrate an {{site.data.keyword.la_full_notm}} instance that is configured to receive platform logs without using the Migration Tool?
{: #mig_faq_5}
{: faq}

If you want to manually migrate an {{site.data.keyword.la_full_notm}} instance that is configured to receive platform logs without using the Migration Tool, you must create an {{site.data.keyword.logs_full_notm}} instance and manually configure resources. You must also configure the {{site.data.keyword.logs_routing_full_notm}} service. For more information, see [Getting started with {{site.data.keyword.logs_routing_full_notm}}](/docs/logs-router?topic=logs-router-getting-started).

## Can {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instances be migrated by the migration tool at the same time?
{: #mig_faq_6}
{: faq}

No. Each {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instance needs to be migrated separately.

Three sets of Terraform files are created by the migration tool that you need to apply to fully migrate each instance.

* Terraform files to create an equivalent {{site.data.keyword.logs_full_notm}} instance and configuration and to create {{site.data.keyword.logs_full_notm}} {{site.data.keyword.cos_full_notm}} buckets.

* Terraform files to create notification channels and {{site.data.keyword.en_full_notm}} resources for alerting.

* Terraform files to create policies based on your current {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instance access report.

When migrating {{site.data.keyword.at_full_notm}} instances you can choose to send all events to a single {{site.data.keyword.logs_full_notm}} instance or to separate instances. For more information about migrating {{site.data.keyword.at_full_notm}} instances, see the [{{site.data.keyword.at_full_notm}} migration instructions](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-at-option2).

To migrate {{site.data.keyword.la_full_notm}} instances with platform logs enabled, see the [{{site.data.keyword.la_full_notm}} migration instructions](/docs/cloud-logs?topic=cloud-logs-migration-tutorial-la-plat).


{{/_include-segments/verify-queries.md}}

Any changes made in the UI to view queries must be made in the Terraform `views.tf` file. If you have modified a view query with a configured {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} alert, you must modify the query generated by the `alerts.tf` file and reapply the Terraform changes.

## Can the migration configuration be verified before being applied?
{: #mig_faq_7}
{: faq}

Yes. You can run the migration tool in [`-t`](/docs/cloud-logs?topic=cloud-logs-migration_cli) mode to generate the Terraform files.  For example:

```text
ibmcloud logging migrate create-resources --scope instance --instance-crn CRN_VALUE --ecrn EVENT_NOTIFICATIONS_INSTANCE_CRN --platform --ingestion-key INGESTION_KEY -t
```
{: pre}

You can modify the Terraform files before applying them.

## Does the migration tool support data migration?
{: #mig_faq_8}
{: faq}

No. The migration tool migrates the {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} configuration only.

If you have archiving configured for {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}}, you can continue to access and manage the data in those buckets the way you do today. {{site.data.keyword.logs_full_notm}} migration does not access or modify those buckets.

When you migrate {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instances, new {{site.data.keyword.la_full_notm}} and {{site.data.keyword.cos_full_notm}} buckets are created, configured, and attached to the created {{site.data.keyword.logs_full_notm}} instance. {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} cannot read data from {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} buckets.

## Are there any further considerations I need to be aware of before migrating from {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}}
{: #mig_faq_9}
{: faq}

Before using the migration tool, consider the following:

* You must have the appropriate [permissions](/docs/cloud-logs?topic=cloud-logs-migration-permissions) to migrate.

* Using the [`--platform`](/docs/cloud-logs?topic=cloud-logs-migration_cli) option in the migration tool will change the way platform data is handled in the account. The migration tool creates targets and rules to continue sending events to existing {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} instances and to the newly created {{site.data.keyword.logs_full_notm}} instance.

   You can migrate instances and configure platform data after migrating.
   {: tip}

* Before running the migration tool, make sure you have an {{site.data.keyword.en_full_notm}} instance provisioned. {{site.data.keyword.en_full_notm}} is required for alerting.

* If you are running the migration tool from a Windows environment, make sure the paths where the Terraform files are located do not exceed the Windows maximum path size limit. For more information, see [I am getting a "failed to install provider" error when running terraform init on Windows](/docs/cloud-logs?topic=cloud-logs-ts-mig-tf-path-length).


{{/_include-segments/verify-queries.md}}


{{/_include-segments/clean-directory.md}}


{{/_include-segments/find-ecrn.md}}
