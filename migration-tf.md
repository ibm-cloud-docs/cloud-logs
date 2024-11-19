---

copyright:
  years:  2024
lastupdated: "2024-11-19"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Applying Terraform after you generate the scripts to create resources
{: #migration-tf}

You can use the migration tool to generate Terraform scripts that you can then use to migrate your {{site.data.keyword.at_full_notm}} and {{site.data.keyword.la_full_notm}} instances into a {{site.data.keyword.logs_full_notm}} instance. You can customize the scripts. You can apply or destroy resources by using the Terraform CLI.
{: shortdesc}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multitier cloud environments that follow Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.logs_full_notm}} instances by using HashiCorp Configuration Language (HCL).

## Prereqs
{: #migration-tf-install-prereqs}

- Run the migration tool to generate Terraform scripts that you can then use to migrate your {{site.data.keyword.at_full_notm}} and {{site.data.keyword.la_full_notm}} instances into a {{site.data.keyword.logs_full_notm}} instance. Customize them per your requirements.

## Step 1. Install the Terraform CLI
{: #migration-tf-install-cli}

Complete the following steps to install the Terraform CLI:

1. Create a terraform folder on your local machine, and navigate to your terraform folder.

    ```terraform
    mkdir terraform && cd terraform
    ```
    {: pre}

2. Download the Terraform version that you want. For example, you can download `terraform_0.15.5_darwin_amd64.zip` for a MacOS.

   The IBM Cloud Provider plug-in for Terraform currently supports Terraform version 0.15.x or later. Make sure to select a supported Terraform version.

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


## Step 2. Set up the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #migration-tf-setup-ibm-plugin}

After the Terraform CLI installation is complete, you must set up the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform so that you can start working with resources and services in IBM Cloud. For a list of supported versions, see the [{{site.data.keyword.cloud_notm}} Provider plug-in releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.



To run your Terraform configuration files with Terraform version 0.15.x or higher, complete the following steps:
1. Create a `versions.tf` file and specify the {{site.data.keyword.cloud_notm}} Provider plug-in version that you want to use with the `version` parameter.

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
        required_version = ">= 0.15"
        required_providers {
            ibm = {
                source = "ibm-cloud/ibm"
                version = "~>1.33.0"
            }
        }
    }
    ```
    {: codeblock}

2. Store the `versions.tf` file in your Git repository or the folder where Terraform is set up.


If you are using Terraform on {{site.data.keyword.cloud_notm}} modules, you must add a `versions.tf` file to all the module folders. You can refer the Terraform provider block from the [provider registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest){: external}. You can use the [IBM Cloud Observability - Terraform Module](https://registry.terraform.io/modules/terraform-ibm-modules/observability/ibm/latest){: external} module to configure an instance.
{: note}



## Step 3. Set up the API key
{: #migration-tf-config-ibm-plugin}

Set the API key that you must configure to create resources for migration.

Run `export IC_API_KEY=xxxxxx` in the command line where you plan to run the Terraform CLI commands.

If running in Windows, use `set IC_API_KEY=xxxxxx` instead.
{: note}



## Step 4. Initialize the Terraform CLI.
{: #migration-tf-init-tf-cli}

Next, initialize the Terraform CLI. Run the following command from the directory where the migration Terraform scripts are available:

```terraform
./terraform init
```
{: pre}

You should see the following message: `Terraform has been successfully initialized!`.

## Step 5. Create a Terraform execution plan
{: #migration-tf-plan-tf-cli}

The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.logs_full_notm}} instance, the resource key, and IAM access policy in your account.

```terraform
./terraform plan
```
{: pre}


## Step 6. Create the resources
{: #migration-tf-create-resources}

Run the folloing command:

```terraform
./terraform apply
```
{: pre}

To delete resources, run `./terraform destroy`.
{: tip}
