---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-21"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# I am getting an error when running `terraform init`
{: #ts-mig-tf-version}
{: troubleshoot}
{: support}

When migrating {{site.data.keyword.at_full}} or {{site.data.keyword.la_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance using the migration tool and running `terraform init` an error is returned.
{: shortdesc}

You get an error message similar to the following:
{: tsSymptoms}

```text
% terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of ibm-cloud/ibm from the dependency lock file
- Reusing previous version of hashicorp/null from the dependency lock file
- Using previously-installed hashicorp/null v3.2.3
╷
│ Error: Failed to query available provider packages
│
│ Could not retrieve the list of available versions for provider ibm-cloud/ibm: locked provider registry.terraform.io/ibm-cloud/ibm 1.70.0-beta0 does not match
│ configured version constraint 1.74.0; must use terraform init -upgrade to allow selection of new versions
╵
```
{: screen}

Or

```text
error running 'terraform init' command. Error Output:
Initializing the backend...

Initializing provider plugins...
- Finding ibm-cloud/ibm versions matching "1.70.0-beta0"...
- Finding latest version of hashicorp/null...
- Installing ibm-cloud/ibm v1.70.0-beta0...
- Installing hashicorp/null v3.2.3...
- Installed hashicorp/null v3.2.3 (signed by HashiCorp)
╷
│ Error: Failed to install provider
│
│ Error while installing ibm-cloud/ibm v1.70.0-beta0: unsuccessful request to
│ https://github.com/IBM-Cloud/terraform-provider-ibm/releases/download/v1.70.0-beta0/terraform-provider-ibm_1.70.0-beta0_darwin_arm64.zip:
│ 500 Internal Server Error
╵
```
{: screen}


The Terraform version needs to be updated.
{: tsCauses}

Do the following to update the Terraform version.
{: tsResolve}

1. Edit the `version.tf` file and change the following section:

   ```json
   terraform {
     required_version = ">= 1.5.0"
     required_providers {
       ibm = {
         source  = "IBM-Cloud/ibm"
         version = "1.70.0-beta0"
       }
     }
   }
   ```
   {: codeblock}

   to

   ```json
   terraform {
     required_version = ">= 1.5.0"
     required_providers {
       ibm = {
         source  = "IBM-Cloud/ibm"
         version = "1.74.0"
       }
     }
   }
   ```
   {: codeblock}

2. Run `terraform init -upgrade`. If successful you will see a message similar to the following:

   ```text
   % terraform init -upgrade

   Initializing the backend...

   Initializing provider plugins...
   - Finding ibm-cloud/ibm versions matching "1.74.0"...
   - Finding latest version of hashicorp/null...
   - Installing ibm-cloud/ibm v1.74.0...
   - Installed ibm-cloud/ibm v1.74.0 (self-signed, key ID AAD3B791C49XX1223)
   - Using previously-installed hashicorp/null v3.2.3

   Partner and community providers are signed by their developers.
   If you'd like to know more about provider signing, you can read about it here:
   https://www.terraform.io/docs/cli/plugins/signing.html

   Terraform has made some changes to the provider dependency selections recorded
   in the .terraform.lock.hcl file. Review those changes and commit them to your
   version control system if they represent changes you intended to make.

   Terraform has been successfully initialized!

   You may now begin working with Terraform. Try running "terraform plan" to see
   any changes that are required for your infrastructure. All Terraform commands
   should now work.

   If you ever set or change modules or backend configuration for Terraform,
   rerun this command to reinitialize your working directory. If you forget, other
   commands will detect it and remind you to do so if necessary.
   ```
   {: screen}
