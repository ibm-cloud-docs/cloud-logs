---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Granting access to {{site.data.keyword.logs_full_notm}}
{: #iam-assign-access}

Access to {{site.data.keyword.cloud_notm}} configuration resources for users and applications in your account is controlled by {{site.data.keyword.iamlong}} (IAM). Every user or application that accesses the {{site.data.keyword.logs_full_notm}} service in your account must be assigned an access policy with an IAM role. Review the following roles, actions, and more to help determine the best way to assign access to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

You can assign access to {{site.data.keyword.logs_full_notm}} by using any of the following methods:

* Access policies per user

* Access groups

    Access groups are used to streamline access management by assigning access to a group once, then you can add or remove users as needed from the group to control their access.

    An access group can be created to organize a set of users, service IDs, and trusted profiles into a single entity that makes it easy for you to assign access. You can assign a single policy to the group instead of assigning the same access multiple times for an individual user or service ID. For more information, see [Setting up access groups](/docs/account?topic=account-groups).

    To organize a set of users and service IDs into a single entity that makes it easy for you to manage IAM permissions, use access groups. You can assign a single policy to the group instead of assigning the same access multiple times per individual user or service ID.
    {: tip}

* Trusted profiles

    You can use trusted profiles to grant different {{site.data.keyword.cloud}} identities access to resources in your account. Automatically grant federated users access to your account with conditions based on SAML attributes from your corporate directory. Or, use trusted profiles to set up fine-grained authorization for applications that are running in compute resources. This way, you aren't required to create service IDs or API keys for the compute resources. You can also establish trust with {{site.data.keyword.cloud_notm}} services or service IDs in another account to grant cross-account access. For more information, see [Creating trusted profiles](/docs/account?topic=account-create-trusted-profile).

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned.
{: important}


## Assigning access to {{site.data.keyword.logs_full_notm}} in the console
{: #iam-assign-access-ui}
{: ui}

There are two common ways to assign access to {{site.data.keyword.logs_full_notm}} in the console:

* Access groups. You can manage access groups and their access from the **Manage** > **Access (IAM)** > **Access groups** page in the console. For more information, see [Assigning access to a group in the console](/docs/account?topic=account-groups&interface=ui#access_ag).

* Access policies per user. You can manage access policies per user from the **Manage** > **Access (IAM)** > **Users** page in the console. For information about the steps to assign IAM access, see [Managing access to resources](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console).



## Assigning access to {{site.data.keyword.logs_full_notm}} in the CLI
{: #iam-assign-access-cli}
{: cli}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the CLI](/docs/account?topic=account-assign-access-resources&interface=cli#access-resources-cli). The following example shows a command for assigning the `Viewer` role for {{site.data.keyword.logs_full_notm}}:

Use `logs` for the service name. Also, use quotations around role names that are more than one word.
{: tip}

```bash
ibmcloud iam user-policy-create name@example.com --service-name logs --roles "Viewer"
```
{: pre}

## Assigning access to {{site.data.keyword.logs_full_notm}} by using the API
{: #iam-assign-access-api}
{: api}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the API](/docs/account?topic=account-assign-access-resources&interface=api) or the [Create a policy API docs](/apidocs/iam-policy-management#create-policy). Role cloud resource names (CRN) in the following table are used to assign access with the API.


| Role name | Role CRN |
|---------------|-----------------|
| Viewer                 | `crn:v1:bluemix:public:logs::::serviceRole:Viewer`        |
| Operator               | `crn:v1:bluemix:public:logs::::serviceRole:Operator`      |
| Editor                 | `crn:v1:bluemix:public:logs::::serviceRole:Editor`        |
| Administrator          | `crn:v1:bluemix:public:logs::::serviceRole:Administrator` |
{: caption="Role ID values for API use" caption-side="bottom"}

The following example is for assigning the `Viewer` role for {{site.data.keyword.logs_full_notm}}:

Use `logs` for the service name, and refer to the Role ID values table to ensure that you're using the correct value for the CRN.
{: tip}

```curl
curl -X POST 'https://iam.cloud.ibm.com/v1/policies' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -d '{
  "type": "access",
  "description": "Viewer role for IBM Cloud Logs",
  "subjects": [
    {
      "attributes": [
        {
          "name": "iam_id",
          "value": "IBMid-123453user"
        }
      ]
    }
  ],
  "roles":[
    {
      "role_id": "crn:v1:bluemix:public:logs::::serviceRole:Viewer"
    }
  ],
  "resources":[
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "$ACCOUNT_ID"
        },
        {
          "name": "serviceName",
          "value": "logs"
        }
      ]
    }
  ]
}'
```
{: curl}
{: codeblock}

```java
SubjectAttribute subjectAttribute = new SubjectAttribute.Builder()
      .name("iam_id")
      .value("IBMid-123453user")
      .build();

PolicySubject policySubjects = new PolicySubject.Builder()
      .addAttributes(subjectAttribute)
      .build();

PolicyRole policyRoles = new PolicyRole.Builder()
      .roleId("crn:v1:bluemix:public:logs::::serviceRole:Viewer")
      .build();

ResourceAttribute accountIdResourceAttribute = new ResourceAttribute.Builder()
      .name("accountId")
      .value("ACCOUNT_ID")
      .operator("stringEquals")
      .build();

ResourceAttribute serviceNameResourceAttribute = new ResourceAttribute.Builder()
      .name("serviceName")
      .value("logs")
      .operator("stringEquals")
      .build();

PolicyResource policyResources = new PolicyResource.Builder()
      .addAttributes(accountIdResourceAttribute)
      .addAttributes(serviceNameResourceAttribute)
      .build();

CreatePolicyOptions options = new CreatePolicyOptions.Builder()
      .type("access")
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
        name: 'iam_id',
        value: 'IBMid-123453user',
      },
    ],
  },
];
const policyRoles = [
  {
    role_id: 'crn:v1:bluemix:public:logs::::serviceRole:Viewer',
  },
];
const accountIdResourceAttribute = {
  name: 'accountId',
  value: 'ACCOUNT_ID',
  operator: 'stringEquals',
};
const serviceNameResourceAttribute = {
  name: 'serviceName',
  value: 'logs',
  operator: 'stringEquals',
};
const policyResources = [
  {
    attributes: [accountIdResourceAttribute, serviceNameResourceAttribute]
  },
];
const params = {
  type: 'access',
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
  attributes=[SubjectAttribute(name='iam_id', value='IBMid-123453user')])
policy_roles = PolicyRole(
  role_id='crn:v1:bluemix:public:logs::::serviceRole:Viewer')
account_id_resource_attribute = ResourceAttribute(
  name='accountId', value='ACCOUNT_ID')
service_name_resource_attribute = ResourceAttribute(
  name='serviceName', value='logs')
policy_resources = PolicyResource(
  attributes=[account_id_resource_attribute,
        service_name_resource_attribute])

policy = iam_policy_management_service.create_policy(
  type='access',
  subjects=[policy_subjects],
  roles=[policy_roles],
  resources=[policy_resources]
).get_result()

print(json.dumps(policy, indent=2))
```
{: python}
{: codeblock}

```go
subjectAttribute := &iampolicymanagementv1.SubjectAttribute{
  Name:  core.StringPtr("iam_id"),
  Value: core.StringPtr("IBMid-123453user"),
}
policySubjects := &iampolicymanagementv1.PolicySubject{
  Attributes: []iampolicymanagementv1.SubjectAttribute{*subjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
  RoleID: core.StringPtr("crn:v1:bluemix:public:logs::::serviceRole:Viewer"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("accountId"),
  Value:    core.StringPtr("ACCOUNT_ID"),
  Operator: core.StringPtr("stringEquals"),
}
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("serviceName"),
  Value:    core.StringPtr("logs"),
  Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
  Attributes: []iampolicymanagementv1.ResourceAttribute{
    *accountIDResourceAttribute, *serviceNameResourceAttribute}
}

options := iamPolicyManagementService.NewCreatePolicyOptions(
  "access",
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

## Assigning access to {{site.data.keyword.logs_full_notm}} by using Terraform
{: #iam-assign-access-terraform}
{: terraform}

The following example is for assigning the `Viewer` role for {{site.data.keyword.logs_full_notm}}:

Use `logs` for the service name.
{: note}

```terraform
resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@example.com"
  roles  = ["Viewer"]

  resources {
    service = "logs"
  }
}
```
{: codeblock}

For more information, see the terraform resource [ibm_iam_user_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_user_policy){: external}.
