---
copyright:
  years:  2024, 2025
lastupdated: "2025-10-28"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Configuring the ordering of {{site.data.keyword.tco-optimizer}} policy processing
{: #tco-optimizer-ordering}

How you order policy definitions in the {{site.data.keyword.logs_full}} {{site.data.keyword.tco-optimizer}} determines how those policies are processed and affects how data is injested and processed by {{site.data.keyword.logs_full_notm}}. Incorrect ordering of policies can result in unintended processing, data that is sent to unintended pipelines, or data that is dropped.
{: shortdesc}

Policy ordering is supported so you have the flexibility to add, update, or delete policies while you maintain the intended execution order. Ordering is essential for consistency and predictability in policy enforcement.

For TCO policies, the sequence directly influences the logic and outcome of applying policies.

TCO policies need to be ordered correctly so they are processed as intended. Policy ordering can be done by using the UI, API, CLI, or Terraform.

## Order TCO policies by using the UI
{: #tco-optimizer-ordering-ui}
{: ui}

To manage the execution order of TCO policies in the UI:

1. Open the {{site.data.keyword.logs_full_notm}} dashboard for your [logging instance](https://cloud.ibm.com/observability/logging){: external}.

2. Click the **Data Pipeline** icon ![Data Pipeline](/icons/data-pipeline.svg "Data Pipeline").

3. Click **TCO Optimizer**.

4. Drag the policies to reorder the list of policies. The policy execution order is changed to reflect the new sequence. The execution order of policies in the list corresponds to their visual arrangement in the UI.


## Order TCO policies by using the API
{: #tco-optimizer-ordering-api}
{: api}

In the API, policy ordering is done by using the request payload argument `before` in the [policy create](/apidocs/logs-service-api#create-policy) or [policy update](/apidocs/logs-service-api#update-policy) methods.

The `before` argument determines the unique ID of the policy before which the policy is created or updated.

- If `before` is provided with a valid unique ID of an existing policy, the policy is created or updated and placed in processing order before the policy with the provided ID.

- If `before` is Empty(`""`), the policy is added as the last policy in the processing list.

- If `before` is provided with ID of policy that doesn't exist, the API returns an error.

The [`order`](/apidocs/logs-service-api#create-policy-response) value in the API response returns the policy's order in the processing list. To get a list of all defined policies and their order values, use the [Get policies method](/apidocs/logs-service-api#get-company-policies).


The following JSON is an example of the `before` field:

```json
    "before": {
        "id": "uuid of policy"
    }
```
{: codeblock}

The following curl example assumes that you have a single existing {{site.data.keyword.logs_full_notm}} policy `A` with the ID `9fab83da-98ce-4f18-a7ba-c6f0435cd673`. The example creates a policy that is named `example_policy` before policy `A`, which creates the `example_policy` order as `1` and the order of policy `A` is updated to `2`.

```sh
curl -X POST --location --header "Authorization: Bearer ${iam_token}" --header "Accept: application/json" --header "Content-Type: application/json" --data   '{
    "application_rule": {
      "name": "policy-test",
      "rule_type_id": "is"
    },
    "before": {
      "id": "9fab83da-98ce-4f18-a7ba-c6f0435cd673"
    },
    "deleted": false,
    "description": "Example policy description",
    "enabled": true,
    "log_rules": {
      "severities": ["error"]
    },
    "name": "example_policy",
    "order": 2,
    "priority": "type_high",
    "subsystem_rule": {
      "name": "policy-test",
      "rule_type_id": "is"
    }
  }' "${base_url}/v1/policies"
```
{: pre}

## Order TCO policies by using the CLI
{: #tco-optimizer-ordering-cli}
{: cli}

Before you begin, [follow the steps](/docs/cloud-logs?topic=cloud-logs-cloud-logs-cli-temp#logs-cli-prereq-temp) to set your {{site.data.keyword.logs_full_notm}} instance API endpoint.

To order TCO policies by using the {{site.data.keyword.logs_full_notm}} CLI plug-in, run the **`ibmcloud cloud-logs policy-create`** command and specify the `before` argument.

For example, the following CLI command assumes that you have a single existing {{site.data.keyword.logs_full_notm}} policy `A` with the ID `9fab83da-98ce-4f18-a7ba-c6f0435cd673`. The example creates a policy that is named `example_policy` before policy `A`, which creates the `example_policy` order as `1` and the order of policy `A` is updated to `2`.

```text
ibmcloud cloud-logs policy-create \
--prototype '{"name": "example_policy", "before": {"id": "9fab83da-98ce-4f18-a7ba-c6f0435cd673"}, "description": "example policy decription", "priority": "type_high", "application_rule": {"rule_type_id": "is", "name": "test"}, "subsystem_rule": {"rule_type_id": "is", "name": "test"},"enabled": true, "log_rules": {"severities": ["critical"]}}'
```
{: pre}


## Order TCO policies by using Terraform
{: #tco-optimizer-ordering-tf}
{: terraform}

Ordering of TCO policies is done in Terraform by using the `before` argument of the [ibm_logs_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/logs_policy){: external} resource.

For example, the following Terraform resource assumes that you have a single existing {{site.data.keyword.logs_full_notm}} policy `A` with the ID `9fab83da-98ce-4f18-a7ba-c6f0435cd673`. The example creates a policy that is named `example_policy` before policy `A`, which creates the `example_policy` order as `1` and the order of policy `A` is updated to `2`.

```terraform
resource "ibm_logs_policy" "logs_policy_instance" {
  instance_id = "<guid of cloud logs instance>"
  region      = "<region of cloud logs instance>"
  name        = "example_policy"
  description = "example policy decription"
  priority    = "type_medium"
  application_rule {
    name         = "otel-links-test"
    rule_type_id = "start_with"
  }
  log_rules {
    severities = ["info"]
  }
  before {
    id =  "9fab83da-98ce-4f18-a7ba-c6f0435cd673"
  }
}
```
{: codeblock}

## State differences
{: #tco-optimizer-ordering-tf-considerations}
{: terraform}

When you order TCO policies by using Terraform, you need to consider state differences.

Terraform shows state differences during a subsequent `apply` if there is an update to the `before` field by the API due to the creation or modification of policies during a previous `terraform apply`.

For example, consider where you try to create `policy3` between `policy1` and `policy2`. When `policy3` is inserted between `policy1` and `policy2`:

- The `order` value of `policy1` is `1` and `policy2` is updated from `2` to `3` by the API.

- The `before` value of `policy1` is updated to `id of policy3` and the `before` value of `policy2` remains same as it is since it is still the last policy.

- Since `order` is a response attribute in the API and in the Terraform resource, the state is updated without any diff. 

- However, `before` is a request parameter, which is something the user provides in their resource block.
  
  During subsequent runs of `plan` and `apply`, Terraform refreshes the state and the `before` of `policy1` is updated to `id of policy3`.
  
  Therefore, Terraform `apply` shows state diff since the user has `before` of `policy1` as `id of policy2` in their Terraform resource but state has the `id of policy3`.

   You need to update your TF file and update your resources with the correct `before` value before you run `apply` again to avoid state differences. Otherwise, Terraform recognizes a state difference and tries to apply unexpected changes.

An error is not returned when a state difference occurs because it is not possible to reliably determine whether the detected change is intentional or a side effect of a previous `apply` operation. Since updates are applied based on the `before` state, differences between expected modifications and unintended drift cannot be determined. Instead of an error, a state difference (diff) is returned instead.
