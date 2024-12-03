---

copyright:
  years:  2024
lastupdated: "2024-12-03"

keywords:

subcollection: cloud-logs

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQs for {{site.data.keyword.logs_full_notm}}
{: #migration-faq}

Frequently asked questions about the Migration Tool.
{: shortdesc}

## What is the difference between the command to generate-resources and the command to create-resources ?
{: #faq_1}
{: faq}

The command `ibmcloud logging migrate generate-resources` was the initial command release with the migration tool to help you plan the migration of instances in your account.

The command `ibmcloud logging migrate create-resources` is the command that you should use to migrate your instances.

Both commands generate the terraform that can be applied to migrate the instance.

## Where do I start to migrate an Activity Tracker instance?
{: #faq_2}
{: faq}

To migrate an Activity Tracker instance, see [Template for migrating Activity Tracker instances in the account](/docs/cloud-logs?topic=cloud-logs-template-migration-at).

## Where do I start to migrate a Log Analysis instance?
{: #faq_3}
{: faq}

To migrate a Log Analysis instance, see [Template for tasks for migrating Log Analysis instances collecting logs in the account](/docs/cloud-logs?topic=cloud-logs-template-migration-logs).

## Where do I start to migrate a Log Analysis instance that has the platform logs flag enabled?
{: #faq_4}
{: faq}

To migrate a Log Analysis instance that has the platform logs flag enabled, see [Template for migrating Log Analysis instances with platform logs flag enabled in the account](/docs/cloud-logs?topic=cloud-logs-template-migration-la).
