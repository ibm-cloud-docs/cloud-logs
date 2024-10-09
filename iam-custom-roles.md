---

copyright:
  years:  2024
lastupdated: "2024-10-09"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Managing custom roles
{: #iam-custom-roles}

The {{site.data.keyword.logs_full_notm}} service maps different sets of actions to different platform roles. However, you might want to combine some of the actions that are currently spread across multiple roles to make assigning meet your custom use case. With a custom role, you can pick and choose actions that are mapped to different roles so that next time you assign access to the service, you don't have to select three different roles.
{: shortdesc}

You can create new roles that are scoped to the {{site.data.keyword.logs_full_notm}} service. This means that you can't combine actions for two different services in a custom role, but you can combine as many actions that you want into a new role for a single service. After you create a custom role with a name of your choosing, anyone in the account who can assign access to the {{site.data.keyword.logs_full_notm}} service can use that role when assigning access.


## Permissions to manage custom roles
{: #iam-custom-roles-1}

Anyone can view the pre-defined roles for the {{site.data.keyword.logs_full_notm}} service in the account.

However, to view, create, edit, or delete a custom role, you must be assigned specific access for the `IAM Access Management` service and the resource type `Role Management`.

| Action              | Administrator | Operator | Editor | Viewer |
|---------------------|---------------|----------|--------|--------|
| View custom roles   | ![Checkmark icon](/icons/checkmark-icon.svg "checkmark") | ![Checkmark icon](/icons/checkmark-icon.svg "checkmark") | ![Checkmark icon](/icons/checkmark-icon.svg "checkmark") | ![Checkmark icon](/icons/checkmark-icon.svg "checkmark") |
| Create custom roles | ![Checkmark icon](/icons/checkmark-icon.svg "checkmark") | | | |
| Update custom roles | ![Checkmark icon](/icons/checkmark-icon.svg "checkmark") | | | |
| Delete custom roles | ![Checkmark icon](/icons/checkmark-icon.svg "checkmark") | | | |
{: caption="Actions for Role management service" caption-side="top"}

## Creating custom roles in the console
{: #iam-custom-roles-2}
{: ui}

Complete the following steps:

1. In the {{site.data.keyword.cloud}} console, go to **Manage** > **Access (IAM)**, and select **Roles**.
2. Click **Create**.
3. Enter a name for your role. This name must be unique within the account. Users see this role name in the console when they assign access to the service.
4. Enter an ID for the role. This ID is used in the CRN, which is used when assigning access by using the API. The role ID must begin with a capital letter and use only alphanumeric characters.
5. Optional: Enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This descriptionis also displayed in the console when a user assigns access to the service.
6. Select a service for the created role.
7. Review the available actions, and select **Add** for all actions that you want in your new role.

   You must add at least one service-defined action to successfully create the new role. If you aren't sure which actions are defined by the service, look in the Type column.
   {: important}

1. Click **Create** when you're done adding actions.


If a service removes an action that you use in a custom role, the custom role is not updated, and might not be valid anymore if the role contained only the removed actions.
{: note}

If you plan to delete a custom role because it is no longer needed, you must be assigned the `Administrator` role. Deleting a custom role automatically updates access for any users, access groups, or service IDs assigned access by using that role to remove it from any existing policies.

## Creating custom roles by using the CLI
{: #iam-custom-roles-3}
{: cli}

Run the following command to create an authorization for the {{site.data.keyword.logs_full_notm}} service.

```bash
ibmcloud iam role-create ROLE_NAME --display-name DISPLAY_NAME --service-name logs [-a, --actions ROLE_ACTION1 [ROLE_ACTION2...]] [-d, --description DESCRIPTION] [--output FORMAT] [-q --quiet]
```
{: codeblock}

Where

--display-name DISPLAY_NAME
:   The display name of the role that is shown in the console.

--service-name SERVICE_NAME
:   The name of the service.

-a, --actions ROLE_ACTION1,ROLE_ACTION2...
:   The actions of the role. For more information, see [IAM actions](/docs/cloud-logs?topic=cloud-logs-iam-actions).

-d, --description DESCRIPTION
:   The description of the role.


For more information about all of the parameters that are available for this command, see [ibmcloud iam authorization-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_role_create).


For example, to create a demo custom role, you can run the following command:

Create a role to perform any Cloud Logs action:
```bash
ibmcloud iam role-create demo --display-name "Demo custom role" --service-name logs --actions logs.data-api.read,logs.livetail.read
```
{: codeblock}



## Creating custom roles by using Terraform
{: #iam-custom-roles-4}
{: terraform}

Before you can create custom roles by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Use the following steps to create custom roles:

1. Create an argument in your `main.tf` file. The following example creates a custom role by using the `ibm_iam_custom_role` resource, where `name` is a unique name to identify the custom role. You must add at least one service-defined `action` to successfully create the new role.

   ```terraform
   resource "ibm_iam_custom_role" "customrole" {
    name         = "Role1"
    display_name = "Role1"
    description  = "This is a custom role"
    service      = "logs"
    actions      = ["logs.data-api.read"]
   }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_custom_role){: external} page.

2. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

3. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   2. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}
