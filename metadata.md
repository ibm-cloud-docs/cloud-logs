---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-23"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Metadata fields
{: #metadata}

{{site.data.keyword.logs_full_notm}} includes metadata fields that can be used to catalog and filter logs, grant user permissions and access to data, create log templates and template branches, and track anomalies.
{: shortdesc}

## Application name
{: #md-app-name}

The application name is the environment that produces and sends logs to {{site.data.keyword.logs_full_notm}}.

The following are samples of application names based on the log source:

| Source                                           | Application Name            |
|--------------------------------------------------|-----------------------------|
| Activity tracking events                         | `ibm-audit-event` |
| Platform logs                                    | `ibm-platform-logs`|
| {{site.data.keyword.openshiftlong_notm}} cluster | `kubernetes.namespace_name`  |
| {{site.data.keyword.containerlong_notm}} cluster | `kubernetes.namespace_name` |
| Linux server                                     | `${HOSTNAME}` |
| Windows server                                   | `${COMPUTERNAME}` |
| {{site.data.keyword.cis_full}} logs `[*]` | `ibm-platform-log` |
{: caption="Application names" caption-side="bottom"}


`[*]` - For information about {{site.data.keyword.cis_full}} logs, see [Creating a Logpush job to send logs to {{site.data.keyword.logs_full_notm}}](/docs/cis?topic=cis-logpush&interface=api#logpush-setup-cloud-logs-api).


## Subsystem name
{: #md-sys-name}

The subsystem name is the service or application that produces and sends logs to {{site.data.keyword.logs_full_notm}}.

The following are samples of subsystem names based on the log source:

| Source                                           | Subsystem Name |
|--------------------------------------------------|-------|
| Activity tracking events                         | `CRNserviceName:instanceID` |
| VPC Activity tracking events                     | `is:resourceType` |
| Platform logs                                    | `CRNserviceName:instanceID`|
| VPC Platform logs                                | `is:resourceType`|
| {{site.data.keyword.openshiftlong_notm}} cluster | `kubernetes.container_name`  |
| {{site.data.keyword.containerlong_notm}} cluster | `kubernetes.container_name`  |
| Linux server                                     |  |
| Windows server                                   | `ProviderName` |
| {{site.data.keyword.cis_full}} logs `[*]` | `internet-svcs:instanceID` |
{: caption="Subsystem names" caption-side="bottom"}


`[*]` - For information about {{site.data.keyword.cis_full}} logs, see [Creating a Logpush job to send logs to {{site.data.keyword.logs_full_notm}}](/docs/cis?topic=cis-logpush&interface=api#logpush-setup-cloud-logs-api).
