---

copyright:
  years:  2024, 2025
lastupdated: "2025-11-11"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring standard alerts
{: #alerts-config-immediate}

Standard alerts are alerts that are triggered by changes to your logs. Triggered by crossing a set quantity threshold of specific logs, this feature allows you to monitor system performance, get notified when changes occur, and pinpoint potential causes. These alerts are useful when trying to measure the number of occurrences of a particular incident.
{: shortdesc}


{{/_include-segments/alerts-prereq.md}}


{{/_include-segments/alerts-alerts-mgmt.md}}

## Choose the type of alert to configure
{: step}
{: #alerts-config-immediate-2}
{: ui}

Complete the following steps:

1. Choose the alert type **Standard Alert**.

    For more information, see [Alert types](/docs/cloud-logs?topic=cloud-logs-alerts#alert-types).

2. In the *Details* section, complete the following steps:

    1. Enter a name.

        - The maximum length of the name is 4096 characters.

    2. [Optional] Enter a description.

        - The maximum length of the description is 4096 characters.

    3. [Optional] Add one or more labels.

        Labels are key:value pairs that you can use later for quick searching.



{{/_include-segments/alerts-choose-logs.md}}


## Specify the triggering condition
{: step}
{: #alerts-config-4-std}
{: ui}


Specify the triggering condition that is evaluated against the data included for analysis for this alert.

Complete the following steps in the *Conditions* section:

1. Select the alert condition type `Notify Immediately` to be notified immediately, as soon as 1 log record is evaluated to match the filtering criteria.

    For `Notify Immediately` alerts, the alert is triggered as soon as 1 line meets the query criteria. {{site.data.keyword.logs_full_notm}} then waits for 1 minute before an additional `Notify Immediately` alert meeting the same query criteria is triggered. If the alert is not resolved, the `Notify` condition indicates how often you are notified of the same alert with a new event after it is triggered.

    In **Alert When**, you can select whether to trigger the alert immediately, or you can define a rule that is based on the number of occurrences within a specified time window, or you can choose to configure a dynamic alert that detects abnormal behavior automatically.

2. Set the condition rule to define the alert priority level. Valid values are `P1`, `P2`, `P3`, `P4` and `P5`.

    For example, `P1` sets the priority of the alert ot `critical` and you can use it to report critical situations.

    For more information, see [Event severities](/docs/cloud-logs?topic=cloud-logs-event-severities).


{{/_include-segments/alerts-config-notif.md}}


{{/_include-segments/alerts-set-schedule.md}}


{{/_include-segments/alerts-save-config.md}}


{{/_include-segments/alerts-next-steps.md}}





{{/_include-segments/alerts-config-tf-prereqs.md}}


{{/_include-segments/terraform-setup-ibm-plugin-dir.md}}


## Create an alert by using Terraform
{: step}
{: #alerts-config-tf-2}
{: terraform}

1. In your Terraform working directory, identify the file that is named `main.tf`.

In this file, you add the configuration to create an authorization between services by using HashiCorp Configuration Language. For more information, see the Terraform documentation.

Update the namespace by using the cr_namespace and namespace resource arguments in your main.tf file.

resource "cr_namespace" "namespace" {
  name = "<new_name>"
}

Important: Changing the name of a Container Registry namespace cannot be done without deleting the old namespace and re-creating the namespace with a new name. Make sure that you backed up and removed any images that you stored in your namespace before you proceed.

After you finish building your configuration file, initialize the Terraform CLI. For more information, see Initializing Working Directories.

terraform init

Provision the resources from the main.tf file. For more information, see Provisioning Infrastructure with Terraform.

    Run terraform plan to generate a Terraform execution plan to preview the proposed actions.

terraform plan

Run terraform apply to create the resources that are defined in the plan.

terraform apply




```terraform
resource "ibm_logs_alert_definition" "standard_immediate_via_tf" {

  description = "immediate-alert via TF"
  instance_id = "d102c08e-8fa6-45ec-ad79-b0aab828afbd"
  region      = "ca-mon"
  enabled     = true

  name         = "standard-immediate"

  entity_labels = {
    env = "prod"
    notif-channel = "slack"
  }

  phantom_mode = false
  priority     = "p1"

  type = "logs_immediate_or_unspecified"


  incidents_settings {
    minutes   = 10
    notify_on = "triggered_only_unspecified"
  }

  logs_immediate {
    notification_payload_filter = [
      "action",
      "initiator.name",
      "severity"
    ]
    logs_filter {
      simple_filter {
        lucene_query = "action:\"delete\""
        label_filters {
          application_name {
            operation = "is_or_unspecified"
            value     = "ibm-audit-event"
          }

          application_name {
            operation = "is_or_unspecified"
            value     = "marisa"
          }

          subsystem_name {
            operation = "is_or_unspecified"
            value     = "iam-am:"
          }

          severities = [
           "critical",
           "error"
          ]
        }
      }
    }
  }
}
```
{: codeblock}
