---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-22"

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

## Public endpoints
{: #public-endpoints}

Public endpoints can be accessed from the public internet.

| Geography | Region                           | Endpoint | Purpose |
|-----------|----------------------------------|---------------------|--------------------|
| Asia Pacific  | Osaka (`jp-osa`) | `<service-instance-guid>.api.jp-osa.logs.cloud.ibm.com` | Query logs and manage the instance |
| Asia Pacific  | Osaka (`jp-osa`) | `dashboard.jp-osa.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| Asia Pacific  | Sydney (`au-syd`) | `<service-instance-guid>.api.au-syd.logs.cloud.ibm.com` | Query logs and manage the instance |
| Asia Pacific  | Sydney (`au-syd`) | `dashboard.au-syd.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| Asia Pacific  | Tokyo (`jp-tok`) | `<service-instance-guid>.api.jp-tok.logs.cloud.ibm.com` | Query logs and manage the instance |
| Asia Pacific  | Tokyo (`jp-tok`) | `dashboard.jp-tok.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| Europe  | Frankfurt (`eu-de`) | `<service-instance-guid>.api.eu-de.logs.cloud.ibm.com` | Query logs and manage the instance |
| Europe  | Frankfurt (`eu-de`) | `dashboard.eu-de.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| Europe  | London (`eu-gb`) | `<service-instance-guid>.api.eu-gb.logs.cloud.ibm.com` | Query logs and manage the instance |
| Europe  | London (`eu-gb`) | `dashboard.eu-gb.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| Europe  | Madrid (`eu-es`) | `<service-instance-guid>.api.eu-es.logs.cloud.ibm.com` | Query logs and manage the instance |
| Europe  | Madrid (`eu-es`) | `dashboard.eu-es.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| North America  | Toronto (`ca-tor`) | `<service-instance-guid>.api.ca-tor.logs.cloud.ibm.com` | Query logs and manage the instance |
| North America  | Toronto (`ca-tor`) | `dashboard.ca-tor.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| North America  | Dallas (`us-south`) | `<service-instance-guid>.api.us-south.logs.cloud.ibm.com` | Query logs and manage the instance |
| North America  | Dallas (`us-south`) | `dashboard.us-south.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| North America  | Washington (`us-east`) | `<service-instance-guid>.api.us-east.logs.cloud.ibm.com` | Query logs and manage the instance |
| North America  | Washington (`us-east`) | `dashboard.us-east.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
| South America  | Sao Paulo (`br-sao`) | `<service-instance-guid>.api.br-sao.logs.cloud.ibm.com` | Query logs and manage the instance |
| South America  | Sao Paulo (`br-sao`) | `dashboard.br-sao.logs.cloud.ibm.com/<service-instance-guid>` | Access to the dashboard |
{: caption="List of {{site.data.keyword.logs_full_notm}} public endpoints" caption-side="top"}

These endpoints are proxied using {{site.data.keyword.cis_full}}, which uses IP address described in [CIS allowlisted IP addresses](/docs/cis?topic=cis-cis-allowlisted-ip-addresses).

## Private endpoints
{: #private-endpoints}

Private endpoints restrict access to the {{site.data.keyword.cloud_notm}} private network. After creation, a service instance can be accessed using private endpoints.

| Geography | Region                           | Endpoint | Purpose |
|-----------|----------------------------------|---------------------|--------------------|
| Asia Pacific  | Osaka (`jp-osa`) | `<service-instance-guid>.api.private.jp-osa.logs.cloud.ibm.com` | Query logs and manage the instance |
| Asia Pacific  | Sydney (`au-syd`) | `<service-instance-guid>.api.private.au-syd.logs.cloud.ibm.com` | Query logs and manage the instance |
| Asia Pacific  | Tokyo (`jp-tok`) | `<service-instance-guid>.api.private.jp-tok.logs.cloud.ibm.com` | Query logs and manage the instance |
| Europe  | Frankfurt (`eu-de`) | `<service-instance-guid>.api.private.eu-de.logs.cloud.ibm.com` | Query logs and manage the instance |
| Europe  | London (`eu-gb`) | `<service-instance-guid>.api.private.eu-gb.logs.cloud.ibm.com` | Query logs and manage the instance |
| Europe  | Madrid (`eu-es`) | `<service-instance-guid>.api.private.eu-es.logs.cloud.ibm.com` | Query logs and manage the instance |
| North America  | Toronto (`ca-tor`) | `<service-instance-guid>.api.private.ca-tor.logs.cloud.ibm.com` | Query logs and manage the instance |
| North America  | Dallas (`us-south`) | `<service-instance-guid>.api.private.us-south.logs.cloud.ibm.com` | Query logs and manage the instance |
| North America  | Washington (`us-east`) | `<service-instance-guid>.api.private.us-east.logs.cloud.ibm.com` | Query logs and manage the instance |
| South America  | Sao Paulo (`br-sao`) | `<service-instance-guid>.api.private.br-sao.logs.cloud.ibm.com` | Query logs and manage the instance |
{: caption="List of {{site.data.keyword.logs_full_notm}} private endpoints" caption-side="top"}



When connecting to a private endpoint using a [VPE](/docs/cloud-logs?topic=cloud-logs-vpe-connection&interface=cli), use port 443. When connecting to a private endpoint using a [CSE](/docs/account?topic=account-service-endpoints-overview), use port 3443.
{: important}
