---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-30"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a S2S authorization to grant {{site.data.keyword.logs_full_notm}} access to {{site.data.keyword.messagehub_full}}
{: #iam-service-auth-es}

Use {{site.data.keyword.iamlong}} (IAM) to create an authorization that grants {{site.data.keyword.logs_full_notm}} access to the {{site.data.keyword.messagehub_full}} service.
{: shortdesc}



## Before you begin
{: #iam-service-auth-es-prereqs}

- Read about [Managing authorizations to grant access between services](/docs/cloud-logs?topic=cloud-logs-iam-service-auth).

- You must have access to the target service to manage authorization between services. For more information, see [Permissions to manage authorizations](/docs/cloud-logs?topic=cloud-logs-iam-service-auth#iam-service-auth-permissions).

- The target service is located always in the account where the authorization is created.

- The autorization that you define for the {{site.data.keyword.logs_full_notm}} service requires that you have `Administrator` role for the {{site.data.keyword.messagehub_full}} target.



## Service access roles
{: #iam-service-auth-es-roles}

You must grant `Writer` role to handle source integration with the {{site.data.keyword.messagehub_full}} service.


## Creating an authorization through the console
{: #iam-service-auth-es-create-ui}
{: ui}

Complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Authorizations**.
2. Click **Create**.
3. Select a source account by doing one of the following.

    * If the source service that needs access to the target service is in this account, select **This account**.

    * If the source service that needs access to the target service is in a different account, select **Other account**. Then, enter the account ID of the source account.

4. Select `Cloud Logs` as the source service. Then, set the scope of the access by doing one of the following.

    * Select **All resources** to grant access for all instances in the account.

    * Select **Source service instance** to grant access to 1 {{site.data.keyword.logs_full_notm}} instance.

5. Select **Event Streams** as the target service. Then, set the scope of the access by doing one of the following.

    * To grant access to all {{site.data.keyword.messagehub_full}} instances and resources in the account, select **All resources**.

    * To grant access to a specific instance, select single instance by configuring **Resources based on selected attributes** &gt; **Service Instance**.

6. In the *Service Access* section, select the role to assign access to the source service that accesses the target service.

    Select **Writer** to authorize streaming to {{site.data.keyword.messagehub_full}}.

    If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned.
    {: important}

7. Click **Authorize**.

If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account number. 
{: note}

## Creating an authorization by using the CLI
{: #iam-service-auth-es-create-cli}
{: cli}



Run the following command to create an authorization for the {{site.data.keyword.logs_full_notm}} service.

```sh
ibmcloud iam authorization-policy-create logs messagehub "Writer" [--source-service-instance-name SOURCE_SERVICE_INSTANCE_NAME | --source-service-instance-id SOURCE_SERVICE_INSTANCE_ID] [--target-service-instance-name TARGET_SERVICE_INSTANCE_NAME | --target-service-instance-id TARGET_SERVICE_INSTANCE_ID]
```
{: codeblock}


For more information about all of the parameters that are available for this command, see [ibmcloud iam authorization-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create).


## Creating an authorization by using Terraform
{: #iam-service-auth-es-create-terra}
{: terraform}


Before you can create an authorization by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Use the following steps to create an authorization by using Terraform:

1. Create an authorization policy between services by using the `ibm_iam_authorization_policy` resource argument in your `main.tf` file.

    The following example creates an authorization between 2 services:

    ```terraform
    resource "ibm_iam_authorization_policy" "policy" {
     source_service_name = "logs"
     target_service_name = "messagehub"
     roles               = ["Writer"]
     description         = "Authorization Policy"
     transaction_id     = "terraformAuthorizationPolicy"
    }
    ```
    {: codeblock}

    The following example creates an authorization between 2 specific service instances:

    ```terraform
    resource "ibm_iam_authorization_policy" "policy" {
      source_service_name         = "logs"
      source_resource_instance_id = ibm_resource_instance.instance1.guid
      target_service_name         = "messagehub"
      target_resource_instance_id = ibm_resource_instance.instance2.guid
      roles                       = ["Writer"]
    }
    ```
    {: codeblock}

    The `ibm_iam_authorization_policy` resource requires the source service, target service, and role. The source service is granted access to the target service, and the role is the level of permission that the access allows. Optionally, you can add a description for the authorization and a transaction ID.
    {: note}

    - You can provide a `target_resource_instance_id` to scope an {{site.data.keyword.messagehub_full}} target instance.

    - For more examples, see the [Terraform documentation for authorization resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_authorization_policy){: external}.

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

## Creating an authorization by using the API
{: #iam-service-auth-es-create-api}
{: api}


To authorize a source service access to a target service, use the [IAM Policy Management API](/apidocs/iam-policy-management#create-policy). See the following API example for create a policy method with the `type=authorization` specified for a `event-notifications` target.

The supported attributes for creating an authorization policy depend on what each service supports. For more information about the supported attributes for each service, see the documentation for the services that you're using.
{: note}

```bash
curl --request POST \
  --url https://iam.cloud.ibm.com/v1/policies \
  --header 'Authorization: Bearer <token>' \
  --header 'Content-Type: application/json' \
  --data '{
    "type": "authorization",
    "subjects": [
        {
            "attributes": [
                {
                    "name": "accountId",
                    "value": "<account-id>"
                },
                {
                    "name": "serviceName",
                    "value": "logs"
                }
            ]
        }
    ],
    "roles": [
        {
            "role_id": "crn:v1:bluemix:public:event-notifications::::serviceRole:Reader"
        }
    ],
    "resources": [
        {
            "attributes": [
                {
                    "name": "serviceName",
                    "value": "messagehub"
                }
            ]
        }
    ]
}'
```
{: curl}
{: codeblock}
