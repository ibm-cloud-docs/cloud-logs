---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Terraform changes required to convert existing {{site.data.keyword.logs_full_notm}} alerts
{: #migrate_alert_definitions}



{{site.data.keyword.logs_full}} changed the configuration and processing of alerts and how alert priorities are defined. These changes might impact any automation that is configured by using Terraform for your environment.
{: shortdesc}

The `ibm_logs_alert_definition` and `ibm_logs_alert` resource providers offer similar functions for {{site.data.keyword.logs_full}} alerts, but are accessed by using different API methods. The `ibm_logs_alert_definition` resource extends the capabilities of the traditional `ibm_logs_alert` resource by supporting advanced configurations, such as:

* [Changing from `severity` to `priority`](/docs/cloud-logs?topic=cloud-logs-new-version-considerations#newconsider_priiority)
* [Multi-condition support](/docs/cloud-logs?topic=cloud-logs-multi-condition)
* [Customizing the evaluation window](/docs/cloud-logs?topic=cloud-logs-eval-window)

To be compatibility with the current alerting configuration, you want to update your Terraform from using `ibm_logs_alert` to `ibm_logs_alert_definition`.


The [Alert Definition API](/apidocs/logs-service-api#create-alert-def) is fully compatible with the [Alerts API](/apidocs/logs-service-api#create-alert). All alerts that were created by using the Alerts API can be accessed and managed by using the Alert Definition API.

To reconfigure existing alerts, use the `ibm_logs_alert_definition` resource to import them. With the `ibm_logs_alert_definition` resource, you can continue managing existing alerts by using the updated resource structure.


## Import your `ibm_logs_alert` and create an `ibm_logs_alert_definition` resource
{: #migrate_import_logs_alert_definition}

### Get the alert ID of the existing alert
{: #migrate_getalertid}

First, you need to get the alert ID of the existing alert to import the alert definition into the new `ibm_logs_alert_definition` resource.

#### Get the alert ID by using the UI
{: #migrate_getalertid_UI}

To get the alert ID by using the UI:

1. Open the {{site.data.keyword.logs_full_notm}} dashboard for your [logging instance](https://cloud.ibm.com/observability/logging){: external}.

2. Click the **Alerts** icon ![Alerts icon](/icons/alerts.svg "Alerts").

3. Click **Alerts management**.

4. Select the alert to be imported.

5. Find `Alert unique identifier:` in the `History` section.

#### Get the alert ID by using the CLI
{: #migrate_getalertid_CLI}


To get the alert ID by using the CLI:

1. Log in to the CLI and set the configuration by following [these steps](/docs/cloud-logs?topic=cloud-logs-cloud-logs-cli-temp#logs-cli-prereq-temp)

2. List the alerts by running the `ibmcloud logs alert-definitions` command.

3. Find the ID of the alert to be imported in the ID column of the CLI command response.

#### Get the alert ID by using Terraform
{: #migrate_getalertid_TF}

To get the alert ID by using Terraform:

1. Create a `main.tf` file with the following data source. This data source lists all the alerts in the instance.

    ```terraform
        data "ibm_logs_alert_definitions" "alerts" {
            instance_id = "guid-of-logs-instance"
            region      = "region-of-logs-instance"
        }

        locals {
            alertdefs  = data.ibm_logs_alert_definitions.alerts.alert_definitions
            alertids   = [for adf in local.alertdefs : "${data.ibm_logs_alert_definitions.alerts.region}/${data.ibm_logs_alert_definitions.alerts.instance_id}/${adf.id}"]
            alertnames = [for adf in local.alertdefs : adf.name]
        }
        output "alertids" {
            value = local.alertids
        }
        output "alertnames" {
            value = local.alertnames
        }

    ```
    {: codeblock}

2. Run `terraform apply`.

The alert IDs and names are returned as output. Identify the ID of the alert that you want to import from the output.


### Creating the constructed alert ID
{: #migrate_construct_alertid}

The `ibm_logs_alert_definition` resource can be imported by using a constructed alert ID. The constructed alert ID is a combination of the {{site.data.keyword.logs_full_notm}} region, the `instance_id`, and the retrieved unique `alert_id`. For more information, see [the `ibm_logs_alert_definition` Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/logs_alert_definition#import){: external}.

You need to create a constructed alert ID in the following format: `<region>/<instance_id><alert_id>`. This constructed alert ID is used in the import steps.


## Importing and converting your alert to an `ibm_logs_alert_definition` resource on a local system
{: #migrate_resource_local}

Use these steps to import and convert an existing alert by running the steps on a local system, console, or virtual machine.

For this example, an alert that is named `alert-managed-by-tf` is managed by Terraform.

1. Edit your `main.tf` file.

    ```hcl
    resource "ibm_logs_alert" "alert_managed_by_tf" {
      instance_id = "d58f8c45-f781-4aca-b18d-71ad17825867"
      region      = "eu-es"
      name        = "alert-managed-by-tf"
      is_active   = true
      severity    = "info_or_unspecified"
      description = "alert managed by tf"

      notification_groups {
        notifications {
          retriggering_period_seconds = 3600
          notify_on                   = "triggered_and_resolved"
          integration_id              = "27"
        }
      }
      incident_settings {
        retriggering_period_seconds  = 3600
        notify_on                    = "triggered_and_resolved"
        use_as_notification_settings = false
      }

      condition {
        less_than {
          parameters {
            threshold          = 1
            timeframe          = "timeframe_1_h"
            relative_timeframe = "hour_or_unspecified"
        cardinality_fields = []
          }
        }
      }
      filters {
        filter_type = "text_or_unspecified"
        text        = "action:tf"
        severities  = ["info"]
      }
    }
    ```
    {: codeblock}

2. Add a resource block to your `main.tf` file.

    ```hcl
    resource "ibm_logs_alert_definition" "alert_managed_by_tf" {
        instance_id = "d58f8c45-f781-4aca-b18d-71ad17825867"
        region      = "eu-es"
    }
    ```
    {: codeblock}

3. Run the following command with the [<constructed_alert_ID>](#migrate_construct_alertid) for the alert to be converted. 

    ```sh
    terraform import ibm_logs_alert_definition.alert_managed_by_tf <constructed_alert_ID>
    ```
    {: pre}

    The state is imported for `ibm_logs_alert_definition.alert_managed_by_tf` resource.

4. Run the following command to see the state of imported resource.
   
    ```sh
    terraform state show ibm_logs_alert_definition.alert_managed_by_tf
    ```
    {: pre}


5. Copy the necessary contents from the `terraform state show` output to your `ibm_logs_alert_definition` resource block.

    The updated resource block would be similar to the following example:

    ```terraform
        resource "ibm_logs_alert_definition" "alert_managed_by_tf" {
            deleted      = false
            description  = "alert managed by tf"
            enabled      = true
            instance_id  = "d58f8c45-f781-4aca-b18d-71ad17825867"
            name         = "alert-managed-by-tf"
            phantom_mode = false
            priority     = "p5_or_unspecified"
            region       = "eu-es"
            type         = "logs_threshold"
            incidents_settings {
                minutes   = 60
                notify_on = "triggered_and_resolved"
            }
            logs_threshold {
                condition_type              = "less_than"
                evaluation_delay_ms         = 0
                notification_payload_filter = []
                logs_filter {
                    simple_filter {
                        lucene_query = "action:tf"
                         label_filters {
                            severities = [
                                "info",
                            ]
                        }
                    }
                }
                rules {
                    condition {
                        threshold = 1

                        time_window {
                            logs_time_window_specific_value = "hour_1"
                        }
                    }
                    override {
                        priority = "p5_or_unspecified"
                    }
                }
                undetected_values_management {
                    auto_retire_timeframe     = "never_or_unspecified"
                    trigger_undetected_values = true
                }
            }
            notification_group {
                group_by_keys = []
                webhooks {
                    minutes   = 60
                    notify_on = "triggered_and_resolved"
                    integration {
                        integration_id = 27
                    }
                }
            }
        }
    ```
    {: codeblock}

6. Remove all references of the `ibm_logs_alert.alert_managed_by_tf` resource from your `main.tf` file.

7. Remove all references of the `ibm_logs_alert.alert_managed_by_tf` resource from the state by running `terraform state rm ibm_logs_alert.alert_managed_by_tf`.

8. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

    ```terraform
    terraform plan
    ```
    {: pre}

9. Run `terraform apply` to create the resources that are defined in the plan.

   ```terraform
   terraform apply
   ```
   {: pre}

The output says `No infrastructure changes`. Your `alert-managed-by-tf` alert can now be managed by using the `ibm_logs_alert_definition` resource.

## Importing and converting your alert to an `ibm_logs_alert_definition` resource in {{site.data.keyword.bpfull_notm}}
{: #migrate_resource_schematics}

Use these steps to import and convert an existing alert that is managed by Terraform in {{site.data.keyword.bpshort}}.

For this example, an alert that is named `alert-managed-by-tf` is converted.

1. Edit your `main.tf` file.

    ```terraform
    resource "ibm_logs_alert" "alert_managed_by_tf" {
      instance_id = "d58f8c45-f781-4aca-b18d-71ad17825867"
      region      = "eu-es"
      name        = "alert-managed-by-tf"
      is_active   = true
      severity    = "info_or_unspecified"
      description = "alert managed by tf"

      notification_groups {
        notifications {
          retriggering_period_seconds = 3600
          notify_on                   = "triggered_and_resolved"
          integration_id              = "27"
        }
      }
      incident_settings {
        retriggering_period_seconds  = 3600
        notify_on                    = "triggered_and_resolved"
        use_as_notification_settings = false
      }

      condition {
        less_than {
          parameters {
            threshold          = 1
            timeframe          = "timeframe_1_h"
            relative_timeframe = "hour_or_unspecified"
            cardinality_fields = []
          }
        }
      }
      filters {
        filter_type = "text_or_unspecified"
        text        = "action:tf"
        severities  = ["info"]
      }
    }
    ```
    {: codeblock}

2. Add the new resource block to your `main.tf` file and push the file to your GitHub repo.

    ```terraform
    resource "ibm_logs_alert_definition" "alert_managed_by_tf" {
        instance_id = "d58f8c45-f781-4aca-b18d-71ad17825867"
        region      = "eu-es"
    }
    ```
    {: codeblock}

3. Log in to the [{{site.data.keyword.bpshort}} CLI](/docs/schematics?topic=schematics-setup-cli).

4. Run the [{{site.data.keyword.bpshort}} `workspace update` command](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-update) to pull latest code into your workspace.

5. Run the [{{site.data.keyword.bpshort}} `workspace import` command](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-import) with the [<constructed_alert_ID>](#migrate_construct_alertid) for the alert to import your resource:

    ```text
    ibmcloud schematics workspace get --id <schematics workspace id> --address ibm_logs_alert_definition.alert_managed_by_tf --resourceID <constructed_alert_ID>
    ```
    {: pre}

6. Run the [{{site.data.keyword.bpshort}} `workspace state show` command](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-show):

    ```text
    ibmcloud schematics workspace state show --id <schematics workspace id>  --address ibm_logs_alert_definition.alert_managed_by_tf`
    ```
    {: pre}

7. Copy the necessary content from {{site.data.keyword.bpshort}} workspace `state show command` output to your `ibm_logs_alert_definition` resource block.

   The updated resource block would be similar to the following example:

    ```terraform
        resource "ibm_logs_alert_definition" "alert_managed_by_tf" {
            deleted      = false
            description  = "alert managed by tf"
            enabled      = true
            instance_id  = "d58f8c45-f781-4aca-b18d-71ad17825867"
            name         = "alert-managed-by-tf"
            phantom_mode = false
            priority     = "p5_or_unspecified"
            region       = "eu-es"
            type         = "logs_threshold"
            incidents_settings {
                minutes   = 60
                notify_on = "triggered_and_resolved"
            }
            logs_threshold {
                condition_type              = "less_than"
                evaluation_delay_ms         = 0
                notification_payload_filter = []
                logs_filter {
                    simple_filter {
                        lucene_query = "action:tf"
                         label_filters {
                            severities = [
                                "info",
                            ]
                        }
                    }
                }
                rules {
                    condition {
                        threshold = 1

                        time_window {
                            logs_time_window_specific_value = "hour_1"
                        }
                    }
                    override {
                        priority = "p5_or_unspecified"
                    }
                }
                undetected_values_management {
                    auto_retire_timeframe     = "never_or_unspecified"
                    trigger_undetected_values = true
                }
            }
            notification_group {
                group_by_keys = []
                webhooks {
                    minutes   = 60
                    notify_on = "triggered_and_resolved"
                    integration {
                        integration_id = 27
                    }
                }
            }
        }
    ```
    {: codeblock}

8. Remove all references of the `ibm_logs_alert.alert_managed_by_tf` resource from your `main.tf` file.

9. Update your GitHub repo with the code changes and update the workspace by using the [{{site.data.keyword.bpshort}} `workspace update` command](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-update).

10. Remove all references of the `ibm_logs_alert.alert_managed_by_tf` resource from workspace state by using the [{{site.data.keyword.bpshort}} `workspace state rm` command](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-wks_staterm):

    ```text
    ibmcloud schematics workspace state rm --id WORKSPACE_ID --address ibm_logs_alert_definition.alert_managed_by_tf
    ```
    {: pre}

11. Run the {{site.data.keyword.bpshort}} [`plan`](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-plan) and [`apply`](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-apply) commands.

The output says `No infrastructure changes`. Now your `alert-managed-by-tf` alert can be managed by using the `ibm_logs_alert_definition` resource by using the {{site.data.keyword.bpshort}} workspace.
