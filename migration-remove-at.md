---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Removing Legacy Activity Tracker instances
{: #migration-remove-at}

Use this topic as guidance to remove legacy Activity Tracker instances in the account.

## Prereqs
{: #migration-remove-at-prereqs}

Complete the followign steps:

- Review the Activity Tracker Event Routing configuration and verify events are routed to your `cloud_logs` targets.

- [ ]  Check Activity Tracker instances across all regions are migrated.

- [ ] Get the details of each Activity Tracker instance in the account. Run the following command: `resource service-instance --id InstanceCRN -o JSON`

- [ ] For alerting, check the integration between each Cloud Logs instance and the Event Notifications instance that you use for alerting. For more information, see [Test your connection](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-next).

- [ ] Check that permissions on the new Cloud Logs instances are in place and working per your requirements.


## Steps to remove Activity Tracker instances
{: #migration-remove-at-steps}

Complete the following steps to remove legacy Activity Tracker instances:

- [ ] In Activity Tracker Event Routing, remove routes and targets to legacy Activity Tracker instances.

    - [ ] Remove in Activity Tracker Event Routing the routes that send events to legacy Activity Tracker instances.

    - [ ] Remove in Activity Tracker Event Routing the targets that define the legacy Activity Tracker instances.

- [ ] In IAM (access management), remove the policies that grant permissions to work with Activity Tracker instances in the account.

    - [ ] Remove policies from access groups

    - [ ] Remove policies from users

    - [ ] Remove policies from service Ids

    - [ ] Remove policies from trusted profiles

- [ ] Delete the Activity Tracker instances.
