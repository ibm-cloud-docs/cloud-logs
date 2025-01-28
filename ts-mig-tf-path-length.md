---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-28"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# I am getting a "failed to install provider" error when running `terraform init` on Windows
{: #ts-mig-tf-path-length}
{: troubleshoot}
{: support}

When using the migration tool on Windows to migrate {{site.data.keyword.at_full}} or {{site.data.keyword.la_full_notm}} instances, an error is returned when running `terraform init`.
{: shortdesc}

You get an error message similar to the following:
{: tsSymptoms}

```text
Error: Failed to install provider
```
{: screen}

Terraform fails to download the `provider.exe` file if the local path exceeds the Windows 260 character (`MAX_PATH`) default path limit.
{: tsCauses}

This issue can be resolved in one of the following ways:
{: tsResolve}

* Place the directory with your Terraform files in a shallower path on your system and run `terraform init` from that location.

* Set the `TF_DATA_DIR` environment value to a directory in a shallower path to place the Terraform plug-in cache and working directory in a separate working directory from the {{site.data.keyword.logs_full_notm}} migration Terraform files and run `terraform init` again from the location of the {{site.data.keyword.logs_full_notm}} migration Terraform files.
