---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-27"

keywords:

subcollection: cloud-logs

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for the {{site.data.keyword.logs_full_notm}} migration 
{: #releasenotes-migration}

Use these release notes to learn about the latest updates to the migration tool and other migration updates.
{: shortdesc}

For release notes about the {{site.data.keyword.logs_full_notm}} service, see [Release notes for {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-logs-release-notes).
{: note}

Only the current plug-in version and two previous versions are available at any time.
{: note}







##  22 January 2024
{: #migration-jan2224}

The migration tool plug-in v0.1.30 is available.
:   Updates include:

    * IBM Plugin provider is updated to 0.1.74.

    * Due to an {{site.data.keyword.logs_full_notm}} requirement, buckets with retention policies cannot be attached to an {{site.data.keyword.logs_full_notm}} instance. If you have an archiving configuration in your {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} instance, the migration tool has been modified to create and attach buckets without any policies.

    * Duplicate view names are not supported in {{site.data.keyword.logs_full_notm}}. The migration tool is enhanced to allow you to migrate duplicate views without the current manual steps. Duplicate views are created following the naming convention of `viewname-copy1`, `viewname-copy2`, and so on.

    * Fix for error for empty groups data.


##  9 January 2025
{: #migration-jan0925}

The migration tool plug-in v0.1.29 is available.
:   Updates include:

    * Fix for namespace query mapping for views and alerts.


##  6 December 2024
{: #migration-dec0624}

The migration tool plug-in v0.1.28 is available.
:   Updates include:

    * Fix to resolve an issue when duplicate access rule names are found during migration.

    * Improved checking that all required parameters are specified before running migration commands.

    * Fix for progress bar not advancing.



## 19 November 2024
{: #migration-nov1924}

The migration tool plug-in v0.1.26 is available.
:   Updates include:

    * Migrating {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} log groups into {{site.data.keyword.logs_full_notm}} data access rules.

      {{site.data.keyword.logs_full_notm}} uses DPXL as its query language. The migration copies the current {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} log group configuration (1 or more queries) to a data rule in the {{site.data.keyword.logs_full_notm}} instance. Each query must be manually migrated to DPXL individually. For more information about DPXL, see the [DataPrime Expression Language (DPXL) reference](/docs/cloud-logs?topic=cloud-logs-dpxl_ref).

    * Fixes related to configuring {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.cos_full_notm}} buckets, including Windows support.

    * Fixes for errors when migrating IAM policies for users when an inactive user is found.

    * Fixes for errors when `threshold` was found to be of different types, for example, `string` in some cases and `float64` in others.


## 25 October 2024
{: #migration-oct2524}

The migration tool plug-in v0.1.25 is available.
:   Updates include:

    * Fix duplicate topic name creation to allow creation of views that have the same name in an instance. A counter has been used to differentiate views with duplicate names.

    * Add mandatory check before command execution to bring awareness of prerequisites before running the tool.

    * Corrected the help for the `update-resources` command.

## 21 October 2024
{: #migration-oct2124}

The migration tool plug-in v0.1.24 is available.
:   Updates include:

    * Fix for an error when migrating exclusion rules where filters were not being applied.

    * Addition of a new `update-resources` command with an `--iam` option. This command option can be used to migrate IAM policies for users, service IDs, trusted profiles, and access groups associated with an {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} instances to {{site.data.keyword.logs_full_notm}} IAM policies.

    * Fix for terraform to add resource name validation.

## 14 October 2024
{: #migration-oct1424}

The migration tool plug-in v0.1.23 is available.
:   Updates include:

    * Enhanced query mapping to add mappings for Kubernetes fields: `node`, `pod`, `namespace`, and `cluster_name` to `kubernetes.node_name`, `kubernetes.pod_name`, `kubernetes.namespace_name`, `kubernetes.cluster_name`.

    * Add support to automatically migrate IAM resources, users, serviceIds, trusted profiles and access groups per instance.

    * Fixes a bug where alerts were failing to create properly if an alert encountered a problem.



## 2 October 2024
{: #migration-oct0224}

The migration tool plug-in v0.1.22 is available.
:   Updates include:

    * Fixes for problems when configuring buckets with activity tracking events or metrics enabled:

       * Documentation updates to the permissions that are required to create buckets. {{site.data.keyword.cos_full_notm}} buckets with {{site.data.keyword.at_full_notm}} or {{site.data.keyword.mon_full_notm}} enabled must have the `manager` role (`storage.bucket.put_activity_tracking`, `cloud-object-storage.bucket.put_metrics_monitoring`) to create the new buckets with the correct configuration.

       * Configuring the buckets so that the {{site.data.keyword.cos_full_notm}} service identifies where to send events and metrics.

       * A fix for a bug when {{site.data.keyword.cos_full_notm}} buckets are created using the API.

    * Adding labels to alerts that correlate the alert in {{site.data.keyword.logs_full_notm}} with the {{site.data.keyword.en_full_notm}} topic where data from the alert is processed.

## 25 September 2024
{: #migration-sep2524}

The migration tool plug-in v0.1.21 is available.
:   Updates include:

    * The period when an {{site.data.keyword.en_full_notm}} alert is re-sent is set to 10 minutes.

    * If a service to service policy for {{site.data.keyword.en_full_notm}} and {{site.data.keyword.logs_full_notm}} is not required, one is no longer created.

    * A fix for an error during migration when you have archiving configured in your {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} instance, and the collection of metrics for the bucket is not enabled

    * Parsing rules are now maintained in the correct default order. Rules created during migration within an instance are created after the default parsing rule that is included when you provision an instance of {{site.data.keyword.logs_full_notm}}.

## 18 September 2024
{: #migration-sep1824}

The migration tool plug-in v0.1.20 is available.
:   Updates include:

    

    * Support to configure all supported {{site.data.keyword.logs_full_notm}} retention periods.

    * Collection of IAM access report information.

    * Limit {{site.data.keyword.logs_routing_full_notm}} to public ingress endpoints.

    * Improved validation of the usage of the `-t` and `--api` options.

    * Updates to the CLI help.

    * Added plug-in version to log output.

    * Fix for issue when creating webhooks for alerts via the API. A service to service authorization and integration with {{site.data.keyword.en_full_notm}} are only created when you confirm that you want the integration created.

    * Fix for Terraform description validation for invalid characters. Support was added for commas.

    * Fix for {{site.data.keyword.cos_full_notm}} bucket creation error when the {{site.data.keyword.at_full_notm}} or {{site.data.keyword.la_full_notm}} have archiving configured to an {{site.data.keyword.cos_full_notm}} bucket and the endpoint used is a public endpint.

    * Fix for {{site.data.keyword.logs_routing_full_notm}} name error. The migration tool now enforces the 35 character naming limitation.


## 4 September 2024
{: #migration-sep0424}

The migration tool plug-in v0.1.19 is available.
:   In addition to bug fixes, updates include:

    * The ability, with a single command, to continue sending logs to your {{site.data.keyword.la_full_notm}} instance while also sending logs to the newly created {{site.data.keyword.logs_full_notm}} instance. This dual destination configuration will help you verify your migration.

    * The ability to specify the instance name and resource group ID for the created {{site.data.keyword.logs_full_notm}} instance when running the migration command.

    * The ability to set the retention plan for the created {{site.data.keyword.logs_full_notm}} instance.

    * Additional validation of the instance CRN.


## 29 August 2024
{: #migration-aug2924}

The migration tool plug-in v0.1.18 is available.
:   Updates include:

   * The ability to create an {{site.data.keyword.logs_full_notm}} instance in a custom resourceGroupId.

   * When migrating 1 {{site.data.keyword.at_full_notm}} or 1 {{site.data.keyword.la_full_notm}} instance, any associated {{site.data.keyword.atracker_full_notm}} or {{site.data.keyword.logs_routing_full_notm}} configuration can also be migrated.

   * A fix for a dashboard migration bug.

   * The addition of streaming configuration files collected from {{site.data.keyword.at_full_notm}} and {{site.data.keyword.la_full_notm}} instances.

   * A fix for an error when doing query mapping where there was a difference in the conversion of error text. With this fix, error text will remain as-is.


## 21 August 2024
{: #migration-aug2124}

The migration tool plug-in v0.1.17 is available.
:   Updates include:

    * A fix to address a bug creating {{site.data.keyword.cos_full_notm}} buckets when the bucket configuration includes lifecycle policies and retention policies.

    * A fix to address a panic error when accessing an empty archive configuration.


## 19 August 2024
{: #migration-aug1924}

The migration tool plug-in v0.1.16 is available.
:   Updates include:

    * Support for running the migration tool in Windows systems.
    * Enhancements migrating PagerDuty alerts. Terraform scripts are provided.
    * Enhancd migration of views and alerts.

        Migration of apps and subsystems into filters in {{site.data.keyword.logs_full_notm}} views and alerts.

        The App quick search field values in a Mezmo view are mapped to application filters in {{site.data.keyword.logs_full_notm}} views and alerts.


## 12 August 2024
{: #migration-aug1224}

The migration tool plug-in v0.1.15 is available.
:   Updates include:

    * Support for the migration of lifecycle policies and retention policies for the data bucket only.
    * A new command has been added to map a Mezmo view query to a Lucene query.
    * A fix to set the `incident_settings retriggering_period_seconds` for alerts.
    * A fix to remove empty struct in the platform logs report.
    * Support for the latest {{site.data.keyword.cloud_notm}} Terraform provider.


## 01 August 2024
{: #migration-aug0124}

The migration tool plug-in v0.1.14 is available.
:   Updates include:

   * Configure an outbound integration with the {{site.data.keyword.en_full_notm}} service.
   * Create one or more topics and subscriptions in the {{site.data.keyword.en_full_notm}} service.


## 24 July 2024
{: #migration-july2424}

The migration tool plug-in v0.1.13 is available.
:   Updates include:

   * Update {{site.data.keyword.en_full_notm}} notification based on an updated response.

   * Automated Terraform to run with a single flag.

   * Help fixes.

   * Fix for {{site.data.keyword.keymanagementservicelong_notm}} and archiving errors.

   * Support in Terraform for views with an empty query.

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
