---

copyright:
  years:  2024
lastupdated: "2024-08-29"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Ingress endpoints
{: #endpoints_ingress}

Logs can be sent to {{site.data.keyword.logs_full_notm}} by using the listed endpoints for each supported {{site.data.keyword.cloud_notm}} [location](/docs/cloud-logs?topic=cloud-logs-regions).
{: shortdesc}

The endpoints can be found on the [service instance details page](/docs/cloud-logs?topic=cloud-logs-observe&interface=ui#observe-cloud-ui).
{: important}

## Public endpoints
{: #ingress-public-endpoints}

Public endpoints can be accessed from the public internet.

| Geography | Region                           | Endpoint |
|-----------|----------------------------------|---------------------|
| Asia Pacific  | Osaka (`jp-osa`) | `<service-instance-guid>.ingress.jp-osa.logs.cloud.ibm.com` |
| Asia Pacific  | Sydney (`au-syd`) | `<service-instance-guid>.ingress.au-syd.logs.cloud.ibm.com` |
| Asia Pacific  | Tokyo (`jp-tok`) | `<service-instance-guid>.ingress.jp-tok.logs.cloud.ibm.com` |
| Europe  | Frankfurt (`eu-de`) | `<service-instance-guid>.ingress.eu-de.logs.cloud.ibm.com` |
| Europe  | London (`eu-gb`) | `<service-instance-guid>.ingress.eu-gb.logs.cloud.ibm.com` |
| Europe  | Madrid (`eu-es`) | `<service-instance-guid>.ingress.eu-es.logs.cloud.ibm.com` |
| North America  | Toronto (`ca-tor`) | `<service-instance-guid>.ingress.ca-tor.logs.cloud.ibm.com` |
| North America  | Dallas (`us-south`) | `<service-instance-guid>.ingress.us-south.logs.cloud.ibm.com` |
| North America  | Washington (`us-east`) | `<service-instance-guid>.ingress.us-east.logs.cloud.ibm.com` |
| South America  | Sao Paulo (`br-sao`) | `<service-instance-guid>.ingress.br-sao.logs.cloud.ibm.com` |
{: caption="Table 1. List of {{site.data.keyword.logs_full_notm}} ingress endpoints" caption-side="top"}

## Private endpoints
{: #ingress-private-endpoints}

Private endpoints restrict access to the {{site.data.keyword.cloud_notm}} private network. After creation, a service instance can be accessed using private endpoints.

| Geography | Region                           | Endpoint | Purpose |
|-----------|----------------------------------|---------------------|--------------------|
| Asia Pacific  | Osaka (`jp-osa`) | `<service-instance-guid>.ingress.private.jp-osa.logs.cloud.ibm.com` |
| Asia Pacific  | Sydney (`au-syd`) | `<service-instance-guid>.ingress.private.au-syd.logs.cloud.ibm.com` |
| Asia Pacific  | Tokyo (`jp-tok`) | `<service-instance-guid>.ingress.private.jp-tok.logs.cloud.ibm.com` |
| Europe  | Frankfurt (`eu-de`) | `<service-instance-guid>.ingress.private.eu-de.logs.cloud.ibm.com` |
| Europe  | London (`eu-gb`) | `<service-instance-guid>.ingress.private.eu-gb.logs.cloud.ibm.com` |
| Europe  | Madrid (`eu-es`) | `<service-instance-guid>.ingress.private.eu-es.logs.cloud.ibm.com` |
| North America  | Toronto (`ca-tor`) | `<service-instance-guid>.ingress.private.ca-tor.logs.cloud.ibm.com` |
| North America  | Dallas (`us-south`) | `<service-instance-guid>.ingress.private.us-south.logs.cloud.ibm.com` |
| North America  | Washington (`us-east`) | `<service-instance-guid>.ingress.private.us-east.logs.cloud.ibm.com` |
| South America  | Sao Paulo (`br-sao`) | `<service-instance-guid>.ingress.private.br-sao.logs.cloud.ibm.com` |
{: caption="Table 2. List of {{site.data.keyword.logs_full_notm}} private ingress endpoints" caption-side="top"}


To connect to private endpoints, use a [VPE](/docs/cloud-logs?topic=cloud-logs-vpe-connection&interface=cli).
{: important}
