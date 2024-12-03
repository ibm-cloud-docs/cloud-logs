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
