---

copyright:
  years:  2024
lastupdated: "2024-11-26"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# I am getting an error when enabling data usage metrics using Terraform
{: #ts-mig-views}
{: troubleshoot}
{: support}

When the {{site.data.keyword.logs_full}} migration tool attempts to enable data usage metrics, an error is returned.
{: shortdesc}

You get an error message similar to the following:
{: tsSymptoms}

```text
ibm_logs_data_usage_metrics.data_usage-1732165028701161: Creating...
╷
│ Error: ---
│ id: terraform-xxxxx
│ summary: 'UpdateDataUsageMetricsExportStatusWithContext failed: Configuration requirements
│   to enable data usage export not met: FAILED_PRECONDITION: not found: metrics bucket
│   configuration for company 12744'
│ severity: error
│ resource: ibm_logs_data_usage_metrics
│ operation: create
 
```
{: screen}


The [{{site.data.keyword.logs_full_notm}} metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket) is not available, or the {{site.data.keyword.logs_full_notm}} instance is still in the process of attaching to the metrics bucket.
{: tsCauses}

After attaching the metrics bucket, the migration tool might attempt to configure data usage metrics before the {{site.data.keyword.logs_full_notm}} instance has had time to refresh and be aware that the metrics bucket is available.

Verify that a metrics bucket is attached to the {{site.data.keyword.logs_full_notm}} instance and run `terraform init` and `terraform apply` to create the data usage metrics.
{: tsResolve}

