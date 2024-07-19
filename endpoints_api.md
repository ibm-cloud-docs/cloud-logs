---

copyright:
  years:  2024
lastupdated: "2024-07-19"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Service API endpoints
{: #endpoints_api}

Access {{site.data.keyword.logs_full_notm}} by using the listed endpoints for each supported {{site.data.keyword.cloud_notm}} [location](/docs/cloud-logs?topic=cloud-logs-regions).
{: shortdesc}

The endpoints can be found on the [service instance details page](/docs/cloud-logs?topic=cloud-logs-observe&interface=ui#observe-cloud-ui).
{: important}

## Public Endpoints
{: #public-endpoints}

Public endpoints can be accessed from the public internet.

| Geography | Region                           | Endpoint | Purpose |
|-----------|----------------------------------|---------------------|--------------------|
| Europe  | Madrid (`eu-es`) | `<service-instance-guid>.api.eu-es.logs.cloud.ibm.com` | Query logs and manage the instance |
| Europe  | Madrid (`eu-es`) | `dashboard.eu-es.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| Europe  | Frankfurt (`eu-de`) | `<service-instance-guid>.api.eu-de.logs.cloud.ibm.com` | Query logs and manage the instance |
| Europe  | Frankfurt (`eu-de`) | `dashboard.eu-de.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
{: caption="Table 1. List of {{site.data.keyword.logs_full_notm}} public endpoints" caption-side="top"}

## Private Endpoints
{: #private-endpoints}

Private endpoints restrict access to the {{site.data.keyword.cloud_notm}} private network. After creation, a service instance can be accessed using private endpoints.

| Geography | Region                           | Endpoint | Purpose |
|-----------|----------------------------------|---------------------|--------------------|
| Europe  | Madrid (`eu-es`) | `<service-instance-guid>.api.private.eu-es.logs.cloud.ibm.com` | Query logs and manage the instance |
| Europe  | Frankfurt (`eu-de`) | `<service-instance-guid>.api.private.eu-de.logs.cloud.ibm.com` | Query logs and manage the instance |
{: caption="Table 2. List of {{site.data.keyword.logs_full_notm}} private endpoints" caption-side="top"}


To connect to private endpoints, use a [VPE](/docs/cloud-logs?topic=cloud-logs-vpe-connection&interface=cli).
{: important}
