---

copyright:
  years:  2024
lastupdated: "2024-07-11"

keywords:

subcollection: cloud-logs

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for the {{site.data.keyword.logs_full_notm}} migration tool
{: #releasenotes-migration}

Use these release notes to learn about the latest updates to the migration tool.
{: shortdesc}

For release notes about the {{site.data.keyword.logs_full_notm}} service, see [Release notes for {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-logs-release-notes).
{: note}

## 11 July 2024
{: #migration-july1124}

The migration tool plug-in v0.1.12 is available.
:   Updates include:

   * Consolidating the {{site.data.keyword.atracker_full_notm}} configuration into 1 {{site.data.keyword.logs_full_notm}} instance using either Terraform or the API.

   * Data usage support.

   * Fixes related to:

      * Dashboard
      * {{site.data.keyword.logs_routing_full_notm}}
      * {{site.data.keyword.cos_full_notm}} bucket errors


## 3 July 2024
{: #migration-july0324}

The migration tool plug-in v0.1.11 is available.
: Updates include:

   * {{site.data.keyword.atracker_full_notm}} configuration when {{site.data.keyword.atracker_full_notm}} is not configured in the account

   * Fix error setting the severity when alerts are created.

   * Vulnerability fixes.

## 2 July 2024
{: #migration-july0224}

The migration tool plug-in v0.1.10 is available.
: Sets the correct service plan `standard` for production {{site.data.keyword.logs_full_notm}} instances.

## 24 June 2024
{: #migration-jun2424}

The migration tool plug-in is generally available
:   The migration tool helps you plan and migrate {{site.data.keyword.la_full}} instances or {{site.data.keyword.at_full_notm}} instances to {{site.data.keyword.logs_full_notm}} instances. For more information about the migration tool, see [Migrating to {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-migration-intro).
