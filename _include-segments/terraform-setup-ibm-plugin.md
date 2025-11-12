
## Set up the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #terraform-setup-ibm-plugin}
{: step}
{: terraform}

After the Terraform CLI installation is complete, you must set up the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform so that you can start working with resources and services in IBM Cloud.

For a list of supported versions, see the [{{site.data.keyword.cloud_notm}} Provider plug-in releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.

Make sure that you use the latest {{site.data.keyword.cloud_notm}} Provider plug-in release.
{: tip}

Create a `versions.tf` file and specify the {{site.data.keyword.cloud_notm}} Provider plug-in version that you want to use with the `version` parameter.

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
  required_providers {
    ibm = {
      source  = "IBM-Cloud/ibm"
      version = ">=1.80.0"
    }
  }
}
```
{: codeblock}


