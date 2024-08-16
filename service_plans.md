---

copyright:
  years:  2024
lastupdated: "2024-08-16"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Service plans and pricing
{: #service_plans}

One pricing plan is available when provisioning an {{site.data.keyword.logs_full}} instance.
{: shortdesc}

The`Standard` plan is the pricing plan available when provisioning an {{site.data.keyword.logs_full_notm}} instance. When provision an instance, the initial default is 7-days retention in {{site.data.keyword.frequent-search}}. Alternative retention periods can be selected in the console or as a parameter in the CLI or Terraform provider.

You can adjust the consumption tier values using the [TCO Optimizer](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines) feature within the {{site.data.keyword.logs_full_notm}} instance. Policies can be configured to process log and event data using the consumption tiers. You can select to process everything through 1 tier or define policies to configure a mix of consumption tiers to optimize the level of {{site.data.keyword.logs_full_notm}} processing for your log and event data.

Data is metered by the service per gigabytes ingested. You can configure [data usage metrics](/docs/cloud-logs?topic=cloud-logs-data-usage-metrics) to monitor your data usage.

| Consumption tier | Cost per gigabyte |
|---------------|-------------------|
| {{site.data.keyword.compliance}} | $0.48 USD |
| {{site.data.keyword.monitoring}} | $0.75 USD |
| {{site.data.keyword.frequent-search}} - 7 days | $1.20 USD |
| {{site.data.keyword.frequent-search}} - 14 days | $1.75 USD |
| {{site.data.keyword.frequent-search}} - 30 days | $2.25 USD |
| {{site.data.keyword.frequent-search}} - 60 days | $2.75 USD |
| {{site.data.keyword.frequent-search}} - 90 days | $3.25 USD |
{: caption="Data cost per consumption tier" caption-side="bottom"}

## Changing the retention period
{: #change_retention_period}

After creating an {{site.data.keyword.logs_full}} instance, you cannot change the retention period. If you need to change the retention period, open a [support ticket.](/docs/cloud-logs?topic=cloud-logs-getting-help)


