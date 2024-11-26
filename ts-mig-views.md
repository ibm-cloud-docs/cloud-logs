---

copyright:
  years:  2024
lastupdated: "2024-11-26"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# I am getting an error when migrating views using Terraform
{: #ts-mig-views}
{: troubleshoot}
{: support}

When migrating {{site.data.keyword.at_full}} or {{site.data.keyword.la_full_notm}} views to an {{site.data.keyword.logs_full_notm}} instance using the migration tool and Terraform, an error is returned.
{: shortdesc}

You get an error message similar to the following:
{: tsSymptoms}

```text
 ---
id: terraform-37ee6e16
summary: 'CreateViewWithContext failed: {"message":"INVALID_ARGUMENT: A view with
  that name already exists","status":3}'
severity: error
resource: ibm_logs_view
operation: create
component:
  name: github.com/IBM-Cloud/terraform-provider-ibm
  version: 1.70.0-beta0
---


  with ibm_logs_view.logs_view_instance136,
  on views.tf line 194, in resource "ibm_logs_view" "logs_view_instance136":
 194: resource "ibm_logs_view" "logs_view_instance136" {
```
{: screen}


View names in {{site.data.keyword.logs_full_notm}} must be unique. When the {{site.data.keyword.logs_full_notm}} migration tool detects a view with the same name, an error is returned.
{: tsCauses}

Make the following changes to the Terraform files and run `terraform init` and `terraform apply` to create the views and related alerts.
{: tsResolve}

1. Edit the `views.tf` file.

2. Search for the duplicate view name. In the example error message this is `logs_view_instance136`.

3. Look for the `name` value. In this example, `demo16`.

   ```text
   resource "ibm_logs_view" "logs_view_instance136" {
	instance_id               = ibm_resource_instance.cloud_logs_instance.guid
	region				      = ibm_resource_instance.cloud_logs_instance.location
	name           					  = "demo16"
	search_query {
		query = "accountID.keyword:/81de6380e6232019c6567c9c8de6dece.*/ \"error\""
	}
	time_selection {
		quick_selection {
			caption = "Last 24 hours"
			seconds   = 86400
		}
	}

	filters {

		filters {
			name = "applicationName"
			selected_values = {
				"ibm-audit-event" = true
			}
		}
   ```
   {: screen}

4. Change the `name` value to be unique. For example, in this case, to `demo16-1`.

5. Save the `views.tf` file.

If you have 1 or more notification channels configured for the view in the {{site.data.keyword.at_full}} or {{site.data.keyword.la_full_notm}} instance, you will need to update the `alerts.tf` file as well.

1. Edit the `alerts.tf` file.

2. Find the entries with a name starting with the original view name. For example, using the previous `demo16` example:

   ```text
   resource "ibm_logs_alert" "logs_alert_instance_24" {
	instance_id               = ibm_resource_instance.cloud_logs_instance.guid
	region				      = ibm_resource_instance.cloud_logs_instance.location
	name           					  = "demo16-email-f12ef9b958"
  	is_active                           = true
  	severity                            =  "info_or_unspecified"
   ```
   {: screen}

   There might be more than one entry to be changed.
   {: tip}

3. Change the name to match the name used in the `views.tf` file. For example, change `demo16-email-f12ef9b958` to `demo16-1-email-f12ef9b958`.

   The alert name is composed of the view name, the channel type, and an ID.
   {: note}

4. Save the `alert.tf` file.
