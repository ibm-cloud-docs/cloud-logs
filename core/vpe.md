---

copyright:
  years: 2024
lastupdated: "2024-05-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.logs_full_notm}}
{: #vpe-connection}

{{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for VPC enables you to connect to {{site.data.keyword.logs_full_notm}} from your VPC network by using the IP addresses of your choosing, allocated from a subnet within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally, is redundant and highly available, and spans all availability zones of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and {{site.data.keyword.cloud}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addressing within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

To connect to {{site.data.keyword.logs_full_notm}} by using a virtual private endpoint, you must use the API or CLI. The {{site.data.keyword.logs_full_notm}} dashboard in the IBM Cloud console must be accessed through the public network from your VPC.

Integrations with {{site.data.keyword.cos_full_notm}} buckets and {{site.data.keyword.en_full_notm}} instances can use public interfaces, based on the configuration of the integration.

## Before you begin
{: #prereq-service-endpoint}

Before you target a virtual private endpoint for {{site.data.keyword.logs_full_notm}} you must complete the following tasks.

* Ensure that a [Virtual Private Cloud is created](/docs/vpc?topic=vpc-getting-started).
* Make a plan for your [virtual private endpoints](/docs/vpc?topic=vpc-planning-considerations).
* Ensure that [correct access controls](/docs/vpc?topic=vpc-configure-acls-sgs-endpoint-gateways) are set for your virtual private endpoint.
* Understand the [limitations](/docs/vpc?topic=vpc-limitations-vpe) of having a virtual private endpoint.
* Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) about a virtual private endpoint.

## Setting up a VPE for {{site.data.keyword.logs_full_notm}}
{: #endpoint-setup}



When you create a VPE gateway by using the CLI or API, you must specify the [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) of the {{site.data.keyword.logs_full_notm}} instance as the target.

### Configuring an endpoint gateway
{: #endpoint-gateway-cloud-logs}

To configure a virtual private endpoint gateway, follow these steps:

1. List the available services, including {{site.data.keyword.cloud_notm}} infrastructure services available (by default) for all VPC users.
2. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for {{site.data.keyword.logs_full_notm}} that you want to be privately available to the VPC.
3. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
4. View the created VPE gateways associated with the {{site.data.keyword.logs_full_notm}}. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can access your {{site.data.keyword.logs_full_notm}} instance privately through it.

## Using your VPE for {{site.data.keyword.logs_full_notm}}
{: #using-cloud-logs-vpe}

After you create an endpoint gateway for {{site.data.keyword.logs_full_notm}}, follow these steps:

### Using the VPE with the CLI
{: #vpe-cli}
{: cli}

Use the following steps to update to the latest version of the CLI and the {{site.data.keyword.logs_full_notm}} plug-in.

1. Update the {{site.data.keyword.cloud_notm}} CLI to the latest version:

   ```sh
   ibmcloud update
   ```
   {: pre}

2. Update the {{site.data.keyword.logs_full_notm}} CLI plug-in:

   ```sh
   ibmcloud plugin install cloud-logs
   ```
   {: pre}
   
3. Either set the service-url for all commands:

   ```sh
   ibmcloud logs config set service-url https://<instance_ID>.api.private.<region>.logs.cloud.ibm.com
   ```
   {: pre}

   or add it as a parameter for a specific command with `--service-url https://<instance_ID>.api.private.<region>.logs.cloud.ibm.com`
   

### Using the VPE with the API
{: #vpe-api}
{: api}

After creating an endpoint gateway for the {{site.data.keyword.logs_full_notm}} service, use the service endpoints FQDN `<instance_ID>.api.private.<region>.logs.cloud.ibm.com` in the URL to access the service.

### Using the VPE with the SDK
{: #vpe-sdk}
{: api}

After creating an endpoint gateway for {{site.data.keyword.logs_full_notm}}, you must use the private endpoint's FQDN when setting the serviceURL `<instance_ID>.api.private.<region>.logs.cloud.ibm.com`.


### Using the VPE with Terraform
{: #vpe-terraform}
{: terraform}

If you plan to access the {{site.data.keyword.logs_full_notm}} service using Terraform, make sure to set the `IBMCLOUD_LOGS_API_ENDPOINT` environment variable to the private FQDN `<instance_ID>.api.private.<region>.logs.cloud.ibm.com`. For example:

```sh
export IBMCLOUD_LOGS_API_ENDPOINT=<instance_ID>.api.private.<region>.logs.cloud.ibm.com
```
{: pre}
