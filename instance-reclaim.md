---

copyright:
  years:  2024
lastupdated: "2024-10-09"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Recovering a deleted instance
{: #instance-reclaim}

When an {{site.data.keyword.logs_full_notm}} instance is deleted, it is put in a suspend state for 7 days after which its removed from {{site.data.keyword.cloud_notm}}.
{: shortdesc}

The deleted instance can be recovered within 7 days of deletion by following the following steps:

## Prereqs
{: #instance-reclaim-prereqs}

The user must be logged into their {{site.data.keyword.cloud_notm}} account to be able to recover an instance.

## Listing instances available for recovery
{: #instance-reclaim-list}
{: step}

Use the following command to list the deleted instances that are available for reclamation:

```sh
ibmcloud resource reclamations [--g RESOURCE_GROUP_NAME]
```
{: codeblock}

where
- `RESOURCE_GROUP_NAME` is the name of the resource group where you want to list the deleted instances that can be reclaimed and restored.


For example, to list the instances that can be reclaimed in your account, run the following command:

```sh
ibmcloud resource reclamations
List all resource reclamations
OK
ID                                     Resource Instance ID                   Entity CRN                                                                                                                         State            Target Time
835bdb40-b33b-43b4-a1f6-e234433334   d670d057-34c2-4430-8071-bafb0dfddse108   crn:v1:bluemix:public:logs:us-south:a/9999999114b2d2esddf59d2d01:88888888-34c2-4430-8071-ba23443108::   SCHEDULED        2021-10-27T14:08:22Z
```
{: screen}





## Recovering the deleted the instance
{: #instance-reclaim-recover}
{: step}

Use the following command to recover a deleted service instance:

```sh
ibmcloud resource reclamation-restore RESOURCE_INSTANCE_ID  [--g RESOURCE_GROUP_NAME]
```
{: codeblock}

where
- `RESOURCE_GROUP_NAME` is the name of the resource group where the deleted instance was provisioned before being deleted.
- `RESOURCE_INSTANCE_ID` is the ID of the resource instance ID that you plan to restore.

For example, run the following command:

```sh
ibmcloud resource reclamation-restore "835bdb40-b33b-43b4-a1f6-e234433334"
Submitting request to restore resource reclamation 835bdb40-b33b-43b4-a1f6-e234433334 under account xxxxxx
OK
Request to restore reclamation 835bdb40-b33b-43b4-a1f6-e234433334 was submitted
```
{: screen}

Issuing a `ibmcloud resource reclamations` will show the service instance in a **RESTORING** state until it is fully restored.

Once the service instance has been restored, it will show in the {{site.data.keyword.cloud_notm}} console.
