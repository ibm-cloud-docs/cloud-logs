---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-08"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Provisioning an {{site.data.keyword.logs_full_notm}} instance by using Terraform
{: #terraform-setup}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multitier cloud environments that follow Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.logs_full_notm}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud_notm}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't need to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud_notm}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can install from the {{site.data.keyword.cloud_notm}} catalog.
{: tip}

Before you begin, ensure that you have the [required access](/docs/cloud-logs?topic=cloud-logs-iam) to create and work with {{site.data.keyword.logs_full_notm}} resources.

## Step 1. Install the Terraform CLI
{: #terraform-install-cli}

Complete the following steps to install the Terraform CLI:

1. Create a terraform folder on your local machine, and navigate to your terraform folder.

    ```terraform
    mkdir terraform && cd terraform
    ```
    {: pre}

2. Download the Terraform version that you want. For example, you can download `terraform_1.12.2_darwin_amd64.zip` for a MacOS.

3. Extract the Terraform zip file and copy the files to your terraform directory.

4. Set the environment PATH variable to your Terraform files.

    ```terraform
    export PATH=$PATH:<terraform-directory>/terraform
    ```
    {: codeblock}

5. Verify that the installation is successful by using a terraform command.

    ```terraform
    ./terraform
    ```
    {: pre}

## Step 2. Set up the directory
{: #terraform-setup-ibm-plugin}

 Create a folder and navigate into the folder. This folder is used to store all configuration files and variable definitions that are needed to create the {{site.data.keyword.logs_full_notm}} instance.

For example, in your Terraform installation directory `<terraform-directory>/terraform`, create the directory `myproject`.

```text
mkdir myproject && cd myproject
```
{: codeblock}

## Step 3. Set up the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #terraform-setup-ibm-plugin}

After the Terraform CLI installation is complete, you must set up the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform so that you can start working with resources and services in IBM Cloud.

For a list of supported versions, see the [{{site.data.keyword.cloud_notm}} Provider plug-in releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.

Make sure you use the latest {{site.data.keyword.cloud_notm}} Provider plug-in release.
{: tip}

Create a `versions.tf` file and specify the {{site.data.keyword.cloud_notm}} Provider plug-in version that you want to use with the `version` parameter.

```terraform
terraform {
required_providers {
    ibm = {
        source = "IBM-Cloud/ibm"
        version = "<provider version>"
        }
    }
  }
```
{: codeblock}

For example:

```terraform
terraform {
  required_providers {
    ibm = {
      source  = "IBM-Cloud/ibm"
      version = ">=1.80.0"
    }
  }
}
```
{: codeblock}




## Step 4. Configure the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #terraform-config-ibm-plugin}

After you complete the set up, you must [configure the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference).

Before you can start working with Terraform on {{site.data.keyword.cloud_notm}}, you must retrieve the credentials and parameters that are required for a Terraform resource or data source, and specify them in the `provider` configuration. This configuration is used by the {{site.data.keyword.cloud_notm}} Provider plug-in to authenticate with the {{site.data.keyword.cloud_notm}} platform and to view, create, update, or delete {{site.data.keyword.cloud_notm}} resources and services.

The following table lists input parameters that you can set in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file:

|Input parameter | Required / optional  | Description           |
|----------------|----------------------|-----------------------|
|`ibmcloud_api_key`| Required | The {{site.data.keyword.cloud_notm}} API key to authenticate with the {{site.data.keyword.cloud_notm}} platform. For more information, about how to create an API key, see [Creating an API key](/docs/account?topic=account-userapikey&interface=ui#create_user_key). You can specify the API key in the `provider` block or retrieve the value from the `IC_API_KEY` or `IBMCLOUD_API_KEY` environment variables. If both environment variables are defined, `IC_API_KEY` takes precedence. |
|`ibmcloud_timeout`| Optional | The number of seconds that you want to wait until the {{site.data.keyword.cloud_notm}} API is considered unavailable. The default value is `60`. You can specify the timeout in the `provider` block or retrieve the value from the `IC_TIMEOUT` or `IBMCLOUD_TIMEOUT` environment variables. If both variables are specified, `IC_TIMEOUT` takes precedence. |
|`region`| Optional | The {{site.data.keyword.cloud_notm}} region where you want to create your resources. If this value is not specified, `us-south` is used by default. You can specify the region in the `provider` block or retrieve the value from the `IBMCLOUD_REGION` or `IC_REGION` environment variables. If both environment variables are specified, `IC_REGION` takes precedence. |
|`resource_group`| Optional | The ID of the resource group that you want to use for your {{site.data.keyword.cloud_notm}} resources. To retrieve the ID, run `ibmcloud resource groups`. You can specify the resource group in the `provider` block or retrieve the value from the `IC_RESOURCE_GROUP` or `IBMCLOUD_RESOURCE_GROUP` environment variables. If both environment variables are defined, `IC_RESOURCE_GROUP` takes precedence. |
{: caption="List of input parameters that you can set in the provider block of your Terraform" caption-side="top"}

For more information on how to use environment variables, see [Using environment variables](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#env-vars).


### Configure input variables in the terraform.tfvars file
{: #terraform-config-ibm-plugin-tfvars}

You can store information in a local `terraform.tfvars` file and reference these data in your `provider` block.

Do not commit the `terraform.tfvars` into a public source repository. This file is meant to only be stored on your local machine.
{: important}

In your project directory `<terraform-directory>/terraform/myproject`, create a `terraform.tfvars` file on your local machine and add the input parameters that are required for your resource or data source.

    ```terraform
    ibmcloud_api_key = "<ibmcloud_api_key>"
    region = "region"
    account_id = "<Account ID>"
    rg_id = "d7c0e937c529461f90a19e1421f9746d"
    plan = "standard"
    cos_instance_crn = "crn:v1:bluemix:public:cloud-object-storage:global:a/<Account ID>:<COS instance ID>::"
    cos_storage_class = "standard"
    cos_bucket_data_name = "cloud-logs-tf-data"
    cos_bucket_metrics_name = "cloud-logs-tf-metrics"
    event_notifications_crn = "crn:v1:bluemix:public:event-notifications:eu-gb:a/<Account ID>:<Event Notifications instance ID>::"
    event_notifications_instance_id = "<Event Notifications instance ID>"
    event_notifications_region = "eu-gb"
    ```
    {: codeblock}


### Declare variables in the variables.tf file
{: #terraform-config-ibm-plugin-vars-tf}

In your project directory `<terraform-directory>/terraform/myproject`, create a variables file that is named `variables.tf` to include default values.

The following sample lists variables that you can use when you provision an instance:

```terraform
variable "ibm_region" {
  description = "Region to create resources. To see the list of valid regions, see [Locations](/docs/cloud-logs?topic=cloud-logs-regions)."
  type        = string
  default     = "eu-gb"
}

variable "resource_group_name" {
  type        = string
  description = "Resource group where resources are created"
  default     = "Default"
}


variable "rg_id" {
  type        = string
  description = "Resource group ID where resources are created"
  default     = "b302120431c4456097f8970d80b93dfb"
}

variable "plan" {
  type        = string
  description = "Service plan for Cloud Logs instances"
  default     = "standard"
}

variable "cos_instance_crn" {
  type        = string
  description = "COS instance CRN where buckets are created"
  default     = "crn:v1:bluemix:public:cloud-object-storage:global:a/<Account ID>:<COS instance ID>::"
}

variable "cos_storage_class" {
  type        = string
  description = "COS instance storage class"
  default     = "standard"
}

variable "account_id" {
  type        = string
  description = "Account where resources are created"
  default     = "<Account ID>"
}

variable "cos_bucket_data_name" {
  type        = string
  description = "Cloud Object Storage bucket data name"
  default     = "cloud-logs-tf-data"
}

variable "cos_bucket_metrics_name" {
  type        = string
  description = "Cloud Object Storage bucket data name"
  default     = "cloud-logs-tf-metrics"
}

variable "event_notifications_crn" {
  type        = string
  description = "Event Notifications CRN"
  default     = "crn:v1:bluemix:public:event-notifications:eu-gb:a/<Account ID>:<Event Notifications Instance ID>::"
}

variable "event_notifications_instance_id" {
  type        = string
  description = "Event Notifications instance ID"
  default     = "<Event Notifications Instance ID>"
}

variable "event_notifications_region" {
  type        = string
  description = "Event notifications region"
  default     = "eu-gb"
}
```
{: codeblock}


### Reference variables in the provider.tf file
{: #terraform-config-ibm-plugin-tfvars}

In your project directory `<terraform-directory>/terraform/myproject`, create a `provider.tf` file and use Terraform interpolation syntax to reference the variables from the `terraform.tfvars`.

```terraform
variable "ibmcloud_api_key" {}
variable "region" {}

provider "ibm" {
  ibmcloud_api_key    = var.ibmcloud_api_key
  region = var.region
}
```
{: codeblock}



## Step 5. Create the Terraform configuration files to provision an instance of {{site.data.keyword.logs_full_notm}}
{: #terraform-main-tf}

Next, create the following files:

- `data-bucket.tf`: Contains the Terraform resource definition to create a bucket to store log data.

    ```terraform
    resource "ibm_cos_bucket" "data_bucket" {
	      bucket_name          = var.cos_bucket_data_name
      	resource_instance_id = var.cos_instance_crn
      	region_location      = var.region
  	    storage_class        = var.cos_storage_class
    }
    ```
    {: codeblock}

- `metrics-bucket.tf`: Contains the Terraform resource definition to create a bucket to store metrics collected from log data.

    ```terraform
    resource "ibm_cos_bucket" "metrics_bucket" {
	      bucket_name          = var.cos_bucket_metrics_name
      	resource_instance_id = var.cos_instance_crn
  	    region_location      = var.region
      	storage_class        = var.cos_storage_class
    }
    ```
    {: codeblock}

- `main.tf`: Contains the Terraform resource definition to create the {{site.data.keyword.logs_full_notm}} instance and attach the data bucket and the metrics bucket.

    ```terraform
    data "ibm_resource_group" "group" {
      name = "marisa"
    }

    resource "ibm_resource_instance" "cloud_logs_instance" {
      name              = "cloud-logs-via-tf"
      service           = "logs"
      plan              = var.plan
      location          = var.region
      resource_group_id = data.ibm_resource_group.group.id

      parameters = {
        retention_period = "7"
      }

    }

    resource "null_resource" "update_instance_parameters" {
      triggers = {
        instance_id = ibm_resource_instance.cloud_logs_instance.id
      }

      provisioner "local-exec" {
        command = <<EOT
          ibmcloud login --apikey=$IC_API_KEY
          ibmcloud resource service-instance-update ${ibm_resource_instance.cloud_logs_instance.guid} -p '{"logs_bucket_crn": "${ibm_cos_bucket.data_bucket.crn}", "logs_bucket_endpoint": "${ibm_cos_bucket.data_bucket.s3_endpoint_direct}", "metrics_bucket_crn": "${ibm_cos_bucket.metrics_bucket.crn}","metrics_bucket_endpoint": "${ibm_cos_bucket.metrics_bucket.s3_endpoint_direct}"}'
        EOT
      }
      depends_on = [ibm_iam_authorization_policy.policy-cl-data-bucket,ibm_iam_authorization_policy.policy-cl-metrics-bucket]
    }
    ```
    {: codeblock}

- `en_s2s.tf`: Contains the Terraform resource definition to create the service to service authorizations between the {{site.data.keyword.logs_full_notm}} instance and the buckets.

    ```terraform
    locals {
    	  cos_instance_id = split(":", ibm_cos_bucket.data_bucket.resource_instance_id)[7]
    }

    resource "ibm_iam_authorization_policy" "policy-cl-data-bucket" {
        source_service_name         = "logs"
   	    source_resource_instance_id = ibm_resource_instance.cloud_logs_instance.guid
   	    roles                       = ["Writer"]

        resource_attributes {
	          name  = "serviceName"
    	      value = "cloud-object-storage"
        }

        resource_attributes {
	 	        name  = "serviceInstance"
	 	        value = local.cos_instance_id
	 	        operator = "stringEquals"
        }

        resource_attributes {
		        name = "resourceType"
		        value = "bucket"
		        operator = "stringEquals"
	      }

        resource_attributes {
	 	        name  = "resource"
	      	  value = ibm_cos_bucket.data_bucket.bucket_name
	 	        operator = "stringEquals"
        }

	      resource_attributes {
		        name  = "accountId"
		        value = var.account_id
	      }
    }

    resource "ibm_iam_authorization_policy" "policy-cl-metrics-bucket" {
   	    source_service_name         = "logs"
   	    source_resource_instance_id = ibm_resource_instance.cloud_logs_instance.guid
   	    roles                       = ["Writer"]


        resource_attributes {
	        name  = "serviceName"
	        value = "cloud-object-storage"
        }

        resource_attributes {
	        name  = "serviceInstance"
	 	      value = local.cos_instance_id
	 	      operator = "stringEquals"
        }

        resource_attributes {
		      name = "resourceType"
		      value = "bucket"
		      operator = "stringEquals"
	      }

        resource_attributes {
	 	      name  = "resource"
	 	      value = ibm_cos_bucket.metrics_bucket.bucket_name
	 	      operator = "stringEquals"
        }

        resource_attributes {
		      name  = "accountId"
		      value = var.account_id
	      }
    }
    ```
    {: codeblock}

- `event-notification-extension.tf`: Contains the Terraform resource definition to create an outbound integration between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance through which you send notifications to your destinations such as Slack or email.

    ```terraform
    resource "ibm_logs_outgoing_webhook" "logs_outgoing_webhook_instance" {
	    instance_id               = ibm_resource_instance.cloud_logs_instance.guid
 	    region                    = ibm_resource_instance.cloud_logs_instance.location
 	    name        			  = "Event-notification-cloud-logs-instance"
 	    type                      = "ibm_event_notifications"
 	    ibm_event_notifications {
    	    event_notifications_instance_id = var.event_notifications_instance_id
     	    region_id                       = var.event_notifications_region
 	    }
	    depends_on = [ibm_iam_authorization_policy.policy-event-notifications]
    }
    ```
    {: codeblock}

- `s2s.tf`: Contains the Terraform resource definition to create the authorization between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance.

    ```terraform
    resource "ibm_iam_authorization_policy" "policy-event-notifications" {
	    source_service_name = "logs"
	    source_resource_instance_id = ibm_resource_instance.cloud_logs_instance.guid
	    roles               = ["Reader","Event Source Manager","Viewer"]
	    description         = ""
	    target_service_name = "event-notifications"
    }
    ```
    {: codeblock}

For additional information on how to use Terraform for {{site.data.keyword.cloud_notm}} resources, see [ibm_resource_instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/resource_instance)


## Step 6. Provision resources
{: #terraform-provision}

Complete the following steps:

1. Initialize the Terraform CLI.

    ```terraform
    ../terraform init
    ```
    {: pre}

    You should see the following message: `Terraform has been successfully initialized!`.

2. Create a Terraform execution plan. The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.logs_full_notm}} instance, the resource key, and IAM access policy in your account.

    ```terraform
    ../terraform plan
    ```
    {: pre}

3. Create the resources.

    ```terraform
    ../terraform apply
    ```
    {: pre}

    To delete resources, run `./terraform destroy`.
    {: tip}


## What's next?
{: #terraform_setup_next}

Verify that the resources are created. [Launch the Observability UI](/docs/cloud-logs?topic=cloud-logs-instance-launch) and check the instance has been created.
