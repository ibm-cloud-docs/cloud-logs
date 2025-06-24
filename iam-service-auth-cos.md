---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-24"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a S2S authorization to grant {{site.data.keyword.logs_full_notm}} access to a bucket
{: #iam-service-auth-cos}

Use {{site.data.keyword.iamlong}} (IAM) to create an authorization that grants {{site.data.keyword.logs_full_notm}} access to an {{site.data.keyword.cos_full_notm}} bucket.
{: shortdesc}



## Before you begin
{: #iam-service-auth-cos-prereqs}

- Read about [Managing authorizations to grant access between services](/docs/cloud-logs?topic=cloud-logs-iam-service-auth).

- You must have access to the target service to manage authorization between services. For more information, see [Permissions to manage authorizations](/docs/cloud-logs?topic=cloud-logs-iam-service-auth#iam-service-auth-permissions).

- The target service is located always in the account where the authorization is created.

- The autorization that you define for the {{site.data.keyword.logs_full_notm}} service requires that you have `Administrator` role for the {{site.data.keyword.cos_full_notm}} target.

- If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account ID. 

## Service access roles
{: #iam-service-auth-cos-roles}

You must grant `Writer` role to grant permissions to work with buckets.


## Creating an authorization through the console
{: #iam-service-auth-cos-create-ui}
{: ui}

Complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Authorizations**.
2. Click **Create**.
3. Select a source account.

    If the source service that needs access to the target service is in this account, select **This account**.

    If the source service that needs access to the target service is in a different account, select **Other account**. Then, enter the account ID of the source account.

4. Select `Cloud Logs` as the source service. Then, set the scope of the access.

    Select **All resources** to grant access for all instances in the account.

    Select **Source service instance** to grant access to a single {{site.data.keyword.logs_full_notm}} instance.

5. Select **Cloud Object Storage** as the target service. Then, set the scope of the access.

    To grant access to all instances and resources in the account, select **All resources**.

    To grant access to a specific instance, select single instance by configuring **Resources based on selected attributes** &gt; **Service Instance**.

    To grant access to a single bucket, select single instance by configuring **Resources based on selected attributes** &gt; **Service Instance**. Then, set **Resource ID** with the name of the bucket, and **Resource type** to *bucket*.

6. In the *Service Access* section, select **Writer** to assign access to the source service that accesses the target service.

7. Click **Authorize**.

If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account number. 
{: note}

## Creating an authorization by using the CLI
{: #iam-service-auth-cos-create-cli}
{: cli}


Run the following command to create an authorization for the {{site.data.keyword.logs_full_notm}} service.

```sh
ibmcloud iam authorization-policy-create logs cloud-object-storage "Writer" [--source-service-instance-name SOURCE_SERVICE_INSTANCE_NAME | --source-service-instance-id SOURCE_SERVICE_INSTANCE_ID] [--target-service-instance-name TARGET_SERVICE_INSTANCE_NAME | --target-service-instance-id TARGET_SERVICE_INSTANCE_ID] [--target-resource-type RESOURCE_TYPE] [--target-resource RESOURCE]
```
{: codeblock}

Where you can set the following parameters to grant access to a single bucket:
- `TARGET_SERVICE_INSTANCE_NAME`: CRN of the {{site.data.keyword.cos_full_notm}} instance.
- `RESOURCE_TYPE`: Must be set to **bucket**.
- `RESOURCE`: CRN of the bucket


For more information about all of the parameters that are available for this command, see [ibmcloud iam authorization-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create).


## Creating an authorization by using Terraform
{: #iam-service-auth-cos-create-terra}
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
     target_service_name = "cloud-object-storage"
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
      target_service_name         = "cloud-object-storage"
      target_resource_instance_id = ibm_resource_instance.instance2.guid
      roles                       = ["Writer"]
    }
    ```
    {: codeblock}

    The `ibm_iam_authorization_policy` resource requires the source service, target service, and role. The source service is granted access to the target service, and the role is the level of permission that the access allows. Optionally, you can add a description for the authorization and a transaction ID.
    {: note}

    - You can provide a `target_resource_instance_id` to scope an {{site.data.keyword.cos_full_notm}} target instance.

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
{: #iam-service-auth-cos-create-api}
{: api}

To authorize a source service access to a target service, use the [IAM Policy Management API](/apidocs/iam-policy-management#create-policy). See the following API example for create a policy method with the `type=authorization` specified for a `cloud-object-storage` bucket as the target.

The supported attributes for creating an authorization policy depend on what each service supports.
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
            "role_id": "crn:v1:bluemix:public:cloud-object-storage::::serviceRole:Writer"
        }
    ],
    "resources": [
        {
            "attributes": [
                {
                    "name": "serviceName",
                    "value": "cloud-object-storage"
                },
                {
                    "name": "serviceInstance",
                    "value": "$COS_INSTANCE_CRN",
                    "operator": "stringEquals"
                },
                {
                    "name": "resourceType",
                    "value": "bucket",
                    "operator": "stringEquals"
                },
                {
                    "name": "resource",
                    "value": "$BUCKET_CRN",
                    "operator": "stringEquals"
                }
            ]
        }
    ]
}'
```
{: curl}
{: codeblock}
