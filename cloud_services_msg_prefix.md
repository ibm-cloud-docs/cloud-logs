---

copyright:
  years:  2024
lastupdated: "2024-10-09"

keywords: 

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Cloud services message ID prefixes
{: #cloud_services_msg_prefix}

List of prefixes that {{site.data.keyword.cloud}} services use when they send logs to {{site.data.keyword.logs_full_notm}}:
{: shortdesc}

## Message format
{: #cloud_services_msg_format}

A message ID is made up of the following parts:

```text
<crn-service-name>.####<severity>
```
{: codeblock}

* The CRN service-name value.
* 4 digit numeric code.
* Severity code I, E, W for the type of message: informational, error, or warning.



## VPC infrastructure
{: #cloud_services_msg_format_vpc_infrastructure_msg_prefix}

The following table lists message ID prefixes for the [{{site.data.keyword.vpc_full}}](/docs/vpc?topic=vpc-getting-started) infrastructure service that send logs to {{site.data.keyword.logs_full_notm}}:

| Service                                             | CRN service name  \n `crn-service-name`  | Message ID format      | Sample |
|-----------------------------------------------------|-------------------------------------------|---------------------------|------------------|
| [Dedicated host](/docs/vpc?topic=vpc-creating-dedicated-hosts-instances)  | `dedicated-host`    | `<crn-service-name>.#####<severity>` | `dedicated-host.00001` |
| [Flow Logs for VPC](/docs/vpc?topic=vpc-flow-logs)  | `is.flow-log-collector`                   | `<crn-service-name>.#####<severity>` | `is.flow-log-collector.00001E` |
{: caption="VPC infrastructure service" caption-side="top"}





## Developer tools
{: #cloud_services_msg_format_developer_tools_msg_prefix}

The following table lists message ID prefixes for the developer tools services that send logs to {{site.data.keyword.logs_full_notm}}:

| Service                                             | CRN service name  \n `crn-service-name`  | Message ID format      | Sample |
|-----------------------------------------------------|-------------------------------------------|---------------------------|------------------|
| {{site.data.keyword.en_full}}  | `event-notifications`    | `<crn-service-name>.#####<severity>` | `event-notifications.00001E` |
{: caption="Developer tools services" caption-side="top"}
