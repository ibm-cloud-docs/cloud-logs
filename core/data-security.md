---

copyright:
  years: 2024
lastupdated: "2024-06-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Securing your data in {{site.data.keyword.logs_full_notm}} (WIP)
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.logs_full_notm}}, it is important to know exactly what data is stored and encrypted, and how you can delete any stored personal data.
{: shortdesc}

## How your data is stored and encrypted in {{site.data.keyword.logs_full_notm}}
{: #data-storage}

{{site.data.keyword.logs_full_notm}} collects and aggregates logs and metrics.

- Connections use TLS/SSL encryption for data in transit. The current supported version of this encryption is TLS 1.2.
- The storage where the configuration is stored is encrypted with LUKS using AES-256.


### Data location
{: #data_storage_location}

Log data is hosted on the {{site.data.keyword.cloud_notm}}.

Data is collocated in the location where the {{site.data.keyword.logs_full_notm}} instance is provisioned. For example, log data sent to an instance that is provisioned in `Eu-De` is hosted in the `Eu-De` region.


### Data encryption
{: #data_storage_encryption}

All the data that is hosted in a {{site.data.keyword.cloud_notm}} instance is encrypted at rest using **AES 256**.
{: note}

When a {{site.data.keyword.cloud_notm}} agent sends data to a {{site.data.keyword.cloud_notm}} instance, data is encrypted in transit over HTTPS.

When a user queries the data, it is encrypted during transit.

Connections use TLS/SSL encryption for data in transit. The current supported version of this encryption is TLS 1.2.
{: note}

### Data retention
{: #data_storage_retention}

The retention period that you choose for an {{site.data.keyword.logs_full_notm}} instance defines the number of days that data is stored and retained.

For example, if you choose the *Standard* plan with 7 day retention period, data is stored for 7 days and you have access to it through the {{site.data.keyword.cloud_notm}} Web UI.



## Deleting your data in {{site.data.keyword.logs_full_notm}}
{: #data-delete}

### Deleting {{site.data.keyword.logs_full_notm}} instances
{: #service-delete}

To delete data that is stored in {{site.data.keyword.cloud_notm}} instance, such as views, alerts, dashboards, [delete your {{site.data.keyword.cloud_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-remove&interface=cli#remove_cli).

### Restoring deleted data for {{site.data.keyword.logs_full_notm}}
{: #data-restore}

When you delete a {{site.data.keyword.cloud_notm}} instance from the console or with the CLI, it is soft deleted and can be restored. You must restore your instance within 7 days or it is permanently deleted.

Discover instances that are soft deleted by using the reclamation list command.

```text
ibmcloud resource reclamations
```

Example output:

```txt
List all resource reclamations under account ...
OK

ID                                     Resource Instance ID                   Entity CRN                                                                                                   State       Target Time
c0c6aca5-22ab-4b11-9089-6e92d47e7069   152da244-dc91-4a91-b351-a2ad3680e657   crn:v1:bluemix:public:logs:eu-de:a/4448261269a14562b839e0a3019ed980:152da244-dc91-4a91-b351-a2ad3680e657::   SCHEDULED   2024-06-13T10:40:20Z
236b63ab-1599-4e12-bfc4-d2ab1dac4896   8df85af4-aa90-4704-af3d-f1f5cb7614c6   crn:v1:bluemix:public:logs:eu-de:a/4448261269a14562b839e0a3019ed980:8df85af4-aa90-4704-af3d-f1f5cb7614c6::   SCHEDULED   2024-06-17T07:53:45Z
```

Use the reclamation restore command to restore a soft deleted instance to an active state. The following example restores the {{site.data.keyword.cloud_notm}} instance and its data.
```text
ibmcloud resource reclamation-restore RECLAMATION_ID
```
Example output:
```txt
Submitting request to restore resource reclamation c0c6aca5-22ab-4b11-9089-6e92d47e7069  under account..
OK
Request to restore reclamation c0c6aca5-22ab-4b11-9089-6e92d47e7069  was submitted
```
