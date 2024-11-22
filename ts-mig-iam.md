---

copyright:
  years:  2024
lastupdated: "2024-11-22"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# I am getting an error when migrating while trying to apply the IAM Terraform configuration
{: #ts-mig-iam}
{: troubleshoot}
{: support}

When running the {{site.data.keyword.logs_full}} migration tool version 0.1.26 using Terraform to apply the {{site.data.keyword.iamlong}} (IAM) configuration, an error is returned and the IAM configuration changes are not applied.
{: shortdesc}

You get an error message similar to the following:
{: tsSymptoms}

```text
Error: Duplicate resource "ibm_iam_access_group_policy" configuration

  on roles.tf line 46:
  46: resource "ibm_iam_access_group_policy" "policy_1" {

A ibm_iam_access_group_policy resource named "policy_1" was already declared at roles.tf:35,1-50. Resource names must be unique per type in each module.
```
{: screen}


This error can result if the policy permissions were created previously using the UI or by running the migration tool using the API method.
{: tsCauses}

Resolve this issue by one of the following methods:
{: tsResolve}

* Remove the existing policy permissions, for example, by using the UI if they were created using the UI, and apply the Terraform by running `terraform init` and `terriform apply`.

* Edit the `roles.tf` file and changes the name of the duplicate policy to another name and apply the Terraform by running `terraform init` and `terriform apply`. In the example message the policy name is `policy_1`.
