---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-24"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a S2S authorization to grant {{site.data.keyword.logs_routing_full_notm}} access to send logs to {{site.data.keyword.logs_full_notm}}
{: #iam-service-auth-logs-routing}

Use {{site.data.keyword.iamlong}} (IAM) to create an authorization that grants {{site.data.keyword.logs_routing_full_notm}} access to {{site.data.keyword.logs_full_notm}} so the {{site.data.keyword.logs_routing_full_notm}} service can send logs to your tenant.
{: shortdesc}

You must configure the service to service (S2S) authorization in the {{site.data.keyword.cloud_notm}} account where the {{site.data.keyword.logs_full_notm}} instance is located.
{: important}

## Before you begin
{: #iam-service-auth-logs-routing-prereqs}

- Read about [Managing authorizations to grant access between services](/docs/cloud-logs?topic=cloud-logs-iam-service-auth).

- You must have access to the target service to manage authorization between services. For more information, see [Permissions to manage authorizations](/docs/cloud-logs?topic=cloud-logs-iam-service-auth#iam-service-auth-permissions).

- The target service is located always in the account where the authorization is created.

- The authorization that you define for the {{site.data.keyword.logs_routing_full_notm}} service requires that you have `Administrator` role for the {{site.data.keyword.logs_full_notm}} target.

- If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account ID. 


## Service access roles
{: #iam-service-auth-logs-routing-roles}

You must grant `Sender` role to grant permissions to send data to the {{site.data.keyword.logs_full_notm}} instance.

## Creating an authorization in the console
{: #iam-service-auth-logs-routing-create-ui}
{: ui}

Complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Authorizations**.
2. Click **Create**.
3. Select a source account.

    If the source service that needs access to the target service is in this account, select **This account**.

    If the source service that needs access to the target service is in a different account, select **Other account**. Then, enter the account ID of the source account.

4. Select **Logs Routing** as the source service. Then, set the scope of the access to **All resources**.

5. Select **Cloud Logs** as the target service. Then, set the scope of the access to **All resources** or a single instance by configuring **Resources based on selected attributes** &gt; **Service Instance**.

    Other attributes are not supported for this type of authorization.

6. In the *Service Access* section, select **Sender** to assign access to the source service that accesses the target service.

7. Click **Authorize**.

If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account number. 
{: note}

## Creating an authorization by using the CLI
{: #iam-service-auth-logs-routing-create-cli}
{: cli}


Run the following command to create an authorization for the {{site.data.keyword.logs_full_notm}} service.

```sh
ibmcloud iam authorization-policy-create logs-router logs Sender
```
{: codeblock}

You can scope a specific {{site.data.keyword.logs_full_notm}} target instance by using `[--target-service-instance-name TARGET_SERVICE_INSTANCE_NAME | --target-service-instance-id TARGET_SERVICE_INSTANCE_ID]`. Do not provide any other scope options.

For more information about all of the parameters that are available for this command, see [ibmcloud iam authorization-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create).


## Creating an authorization by using Terraform
{: #iam-service-auth-logs-routing-create-terra}
{: terraform}


Before you can create an authorization by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Use the following steps to create an authorization by using Terraform:

1. Create an authorization policy between services by using the `ibm_iam_authorization_policy` resource argument in your `main.tf` file.

   The following example creates an authorization between services:
   ```terraform
   resource "ibm_iam_authorization_policy" "policy" {
     source_service_name = "logs-router"
     target_service_name = "logs"
     roles               = ["Sender"]
     description         = "Authorization Policy"
     transaction_id     = "terraformAuthorizationPolicy"
   }
   ```
   {: codeblock}

   The `ibm_iam_authorization_policy` resource requires the source service, target service, and role. The source service is granted access to the target service, and the role is the level of permission that the access allows. Optionally, you can add a description for the authorization and a transaction ID.
   {: note}

   - You can provide a `target_resource_instance_id` to scope an {{site.data.keyword.logs_full_notm}} target instance.
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
{: #iam-service-auth-logs-routing-create-api}
{: api}

You must have access to the target service to create an authorization between services. You can grant only the level of access that you have as a user of the target service. The autorization that you define for the {{site.data.keyword.logs_routing_full_notm}} service requires that you have `Administrator` role for the {{site.data.keyword.logs_full_notm}} target service.
{: important}

To authorize a source service access to a target service, use the [IAM Policy Management API](/apidocs/iam-policy-management#create-policy).

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
                    "value": "logs-router"
                }
            ]
        }
    ],
    "roles": [
        {
            "role_id": "crn:v1:bluemix:public:logs::::serviceRole:Sender"
        }
    ],
    "resources": [
        {
            "attributes": [
                {
                    "name": "serviceName",
                    "value": "logs"
                },
                {
                    "name": "serviceInstance",
                    "value": "$LOGS_SERVICE_INSTANCE_CRN",
                    "operator": "stringEquals"
                }
            ]
        }
    ]
}'
```
{: curl}
{: codeblock}

```java
SubjectAttribute accountSubjectAttribute = new SubjectAttribute.Builder()
      .name("accountId")
      .value(exampleAccountId)
      .build();

SubjectAttribute serviceNameSubjectAttribute = new SubjectAttribute.Builder()
      .name("serviceName")
      .value("logs-router")
      .build();

PolicySubject policySubjects = new PolicySubject.Builder()
      .addAttributes(accountSubjectAttribute)
      .addAttributes(serviceNameSubjectAttribute)
      .build();

PolicyRole policyRoles = new PolicyRole.Builder()
      .roleId("crn:v1:bluemix:public:logs::::serviceRole:Sender")
      .build();

ResourceAttribute accountIdResourceAttribute = new ResourceAttribute.Builder()
      .name("accountId")
      .value(exampleAccountId)
      .operator("stringEquals")
      .build();

ResourceAttribute serviceNameResourceAttribute = new ResourceAttribute.Builder()
      .name("serviceName")
      .value("logs")
      .operator("stringEquals")
      .build();

ResourceAttribute serviceInstanceResourceAttribute = new ResourceAttribute.Builder()
      .name("serviceInstance")
      .value(exampleTargetInstanceId)
      .operator("stringEquals")
      .build();

ResourceAttribute resourceTypeResourceAttribute = new ResourceAttribute.Builder()
      .name("resourceType")
      .value(exampleResourceType)
      .operator("stringEquals")
      .build();

ResourceAttribute resourceResourceAttribute = new ResourceAttribute.Builder()
      .name("resource")
      .value(exampleResourceId)
      .operator("stringEquals")
      .build();

PolicyResource policyResources = new PolicyResource.Builder()
      .addAttributes(accountIdResourceAttribute)
      .addAttributes(serviceNameResourceAttribute)
      .build();

CreatePolicyOptions options = new CreatePolicyOptions.Builder()
      .type("authorization")
      .subjects(Arrays.asList(policySubjects))
      .roles(Arrays.asList(policyRoles))
      .resources(Arrays.asList(policyResources))
      .build();

Response<Policy> response = service.createPolicy(options).execute();
Policy policy = response.getResult();

System.out.println(policy);
```
{: java}
{: codeblock}

```javascript
const policySubjects = [
  {
    attributes: [
      {
        name: 'accountId',
        value: exampleAccounId,
      },
      {
        name: 'serviceName',
        value: "logs-router",
      }
    ],
  },
];
const policyRoles = [
  {
    role_id: 'crn:v1:bluemix:public:logs::::serviceRole:Sender',
  },
];
const accountIdResourceAttribute = {
  name: 'accountId',
  value: exampleAccountId,
  operator: 'stringEquals',
};
const serviceNameResourceAttribute = {
  name: 'serviceName',
  value: "logs",
  operator: 'stringEquals'
};

const policyResources = [
  {
    attributes: [
      accountIdResourceAttribute,
      serviceNameResourceAttribute
    ],
  },
];
const params = {
  type: 'authorization',
  subjects: policySubjects,
  roles: policyRoles,
  resources: policyResources,
};

iamPolicyManagementService.createPolicy(params)
  .then(res => {
    examplePolicyId = res.result.id;
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: javascript}
{: codeblock}

```python
policy_subjects = PolicySubject(
    attributes=[SubjectAttribute(name='accountId', value=example_account_id),
                SubjectAttribute(name='serviceName', value="logs-router")
                ])
policy_roles = PolicyRole(
    role_id='crn:v1:bluemix:public:logs::::serviceRole:Sender')
account_id_resource_attribute = ResourceAttribute(
    name='accountId', value=example_account_id)
service_name_resource_attribute = ResourceAttribute(
    name='serviceName', value="logs")
policy_resources = PolicyResource(
    attributes=[account_id_resource_attribute,
                service_name_resource_attribute])

policy = iam_policy_management_service.create_policy(
    type='authorization',
    subjects=[policy_subjects],
    roles=[policy_roles],
    resources=[policy_resources]
).get_result()

print(json.dumps(policy, indent=2))
```
{: python}
{: codeblock}

```go
accountSubjectAttribute := &iampolicymanagementv1.SubjectAttribute{
    Name:  core.StringPtr("accountId"),
    Value: &exampleAccountID,
    Operator: core.StringPtr("stringEquals"),
}
serviceNameSubjectAttribute := &iampolicymanagementv1.SubjectAttribute{
    Name:  core.StringPtr("serviceName"),
    Value: "logs-router",
    Operator: core.StringPtr("stringEquals"),
}
policySubjects := &iampolicymanagementv1.PolicySubject{
    Attributes: []iampolicymanagementv1.SubjectAttribute{*accountSubjectAttribute,
        *serviceNameSubjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
    RoleID: core.StringPtr("crn:v1:bluemix:public:logs::::serviceRole:Sender"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
    Name:     core.StringPtr("accountId"),
    Value:    core.StringPtr(exampleAccountID),
    Operator: core.StringPtr("stringEquals"),
}
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
    Name:     core.StringPtr("serviceName"),
    Value:    core.StringPtr("logs"),
    Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
    Attributes: []iampolicymanagementv1.ResourceAttribute{
        *accountIDResourceAttribute, *serviceNameResourceAttribute},
}

options := iamPolicyManagementService.NewCreatePolicyOptions(
    "authorization",
    []iampolicymanagementv1.PolicySubject{*policySubjects},
    []iampolicymanagementv1.PolicyRole{*policyRoles},
    []iampolicymanagementv1.PolicyResource{*policyResources},
)

policy, response, err := iamPolicyManagementService.CreatePolicy(options)
if err != nil {
    panic(err)
}
b, _ := json.MarshalIndent(policy, "", "  ")
fmt.Println(string(b))
```
{: go}
{: codeblock}
