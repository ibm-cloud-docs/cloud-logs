## Prereqs
{: #alerts-config-tf-prereqs}
{: terraform}

- Learn about alerts in {{site.data.keyword.logs_full_notm}}. For more information, see [Alerting](/docs/cloud-logs?topic=cloud-logs-alerts).

- Check that you have an [{{site.data.keyword.en_short}} instance](/catalog/services/event-notifications){: external} that is in the same account as your {{site.data.keyword.logs_full_notm}} instance and permisions to configure resources in the {{site.data.keyword.en_short}} instance.

- Check that the outbound integration between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_short}} instance is configured. For more information, see [Configuring an outbound integration to connect](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure).

- Make sure that you have the [required access](/docs/cloud-logs?topic=cloud-logs-iam) to create and work with {{site.data.keyword.logs_full_notm}} resources.

- Install the Terraform CLI and configure the IBM Cloud Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
