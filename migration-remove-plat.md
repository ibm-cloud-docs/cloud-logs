---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Removing Legacy Log Analysis instances with platform logs enabled
{: #migration-remove-plat}

Use this topic as guidance to remove legacy Log Analysis instances with platform logs enabled in the account.

## Prereqs
{: #migration-remove-plat-prereqs}

Complete the followign steps:

- Review the IBM Cloud Logs Routing configuration and verify platform logs are routed to your `cloud_logs` targets.

- [ ]  Check Log Analysis instances across all regions are migrated.

- [ ] Get the details of each Log Analysis instance in the account. Run the following command: `resource service-instance --id InstanceCRN -o JSON`

- [ ] For alerting, check the integration between each Cloud Logs instance and the Event Notifications instance that you use for alerting. For more information, see [Test your connection](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-next).

- [ ] Check that permissions on the new Cloud Logs instances are in place and working per your requirements.


## Steps to remove Log Analysis instances
{: #migration-remove-plat-steps}

Complete the following steps to remove Log Analysis instances with platform logs enabled:

- [ ] In IBM Cloud Logs Routing, for each region that you operate, remove the `Log Analysis` target configured for the region.

- [ ] If you have other sources such as Linux servoces or Kubernetes clusters, for each source that is configured to send logs to a Log Analysis in the account, remove the configuration. For example,

    - [ ] Remove logDNA agents from sources.

    - [ ] Clean up your rsyslog configuration.

    - [ ] Modify your custom apps that send logs directly by using the REST API.

- [ ] In IAM (access management), remove the policies that grant permissions to work with Log Analysis instances in the account.

    - [ ] Remove policies from access groups

    - [ ] Remove policies from users

    - [ ] Remove policies from service Ids

    - [ ] Remove policies from trusted profiles

- [ ] Delete the Log Analysis instances.
