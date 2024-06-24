---

copyright:
  years:  2024
lastupdated: "2024-04-01"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Removing authorizations between services
{: #iam-service-auth-remove-auth}

Use {{site.data.keyword.iamlong}} (IAM) to remove an authorization that removes {{site.data.keyword.logs_full_notm}} access to work with other services.
{: shortdesc}



## Removing an authorization in the console
{: #iam-service-auth-remove-auth-ui}
{: ui}

You can remove any authorization between services in the account if you are assigned the `Administrator` role on the target service. If you remove any access policies created by the source service for its dependent services, the source service is unable to complete the workflow or access the target service.

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** &gt; **Access (IAM)**, and select **Authorizations**.
2. Identify the row for the authorization that you want to remove from the account.
3. Click the **Actions** icon ![Actions icon](/icons/action-menu-icon.svg "Actions") > **Remove**.
4. Select **Remove**.

If the source service is removed from the account, any policies that are created by that service for its dependent services are deleted automatically. Similarly, if the dependent service is removed from the account, any access policies that are delegated to that service are also deleted.
{: note}

## Removing an authorization by using the CLI
{: #iam-service-auth-remove-auth-cli}
{: cli}

You can remove any authorization between services in the account if you are assigned the `Administrator` role on the target service. If you remove any access policies created by the source service for its dependent services, the source service is unable to complete the workflow or access the target service.

The following sample deletes an authorization policy:

```text
ibmcloud iam authorization-policy-delete AUTHORIZATION_POLICY_ID
```
{: codeblock}

For more information about all of the parameters that are available for this command, see [ibmcloud iam authorization-policy-delete](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_delete).

If the source service is removed from the account, any policies that are created by that service for its dependent services are deleted automatically. Similarly, if the dependent service is removed from the account, any access policies that are delegated to that service are also deleted.
{: note}

## Removing an authorization by using the API
{: #iam-service-auth-remove-auth-api}
{: api}

You can remove any authorization between services in the account if you are assigned the `Administrator` role on the target service. If you remove any access policies created by the source service for its dependent services, the source service is unable to complete the workflow or access the target service.

To delete an authorization policy, use the [IAM Policy Management API](/apidocs/iam-policy-management#delete-policy) as in the following sample request:

```bash
curl -X DELETE 'https://iam.cloud.ibm.com/v1/policies/$POLICY_ID' \
-H 'Authorization: Bearer $TOKEN' \
-H 'Content-Type: application/json'
```
{: curl}
{: codeblock}

```java
DeletePolicyOptions options = new DeletePolicyOptions.Builder()
        .policyId(examplePolicyId)
        .build();

service.deletePolicy(options).execute();
```
{: java}
{: codeblock}

```javascript
const params = {
  policyId: examplePolicyId,
};

iamPolicyManagementService.deletePolicy(params)
  .then(res => {
    console.log(JSON.stringify(res, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: javascript}
{: codeblock}

```python
response = iam_policy_management_service.delete_policy(
  policy_id=example_policy_id
).get_result()

print(json.dumps(response, indent=2))
```
{: python}
{: codeblock}

```go
options := iamPolicyManagementService.NewDeletePolicyOptions(
  examplePolicyID,
)

response, err := iamPolicyManagementService.DeletePolicy(options)
if err != nil {
  panic(err)
}
```
{: go}
{: codeblock}

If the source service is removed from the account, any policies that are created by that service for its dependent services are deleted automatically. Similarly, if the dependent service is removed from the account, any access policies that are delegated to that service are also deleted.
{: note}

## Removing an authorization by using Terraform
{: #iam-service-auth-remove-auth-tf}
{: terraform}

If you want to remove an authorization by using Terraform, you need to delete the `ibm_iam_authorization_policy` resource from the `main.tf` file. After you delete the resource, provision your file by using the following steps:

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}
