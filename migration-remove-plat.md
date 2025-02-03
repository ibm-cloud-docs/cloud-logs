---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Removing deprecated {{site.data.keyword.la_full_notm}} instances with platform logs enabled
{: #migration-remove-plat}

After you have migrated to {{site.data.keyword.logs_full}} you will want to remove your deprecated {{site.data.keyword.la_full_notm}} instances with platform logs enabled in the account.
{: shortdesc}

As of 28 March 2024 the {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} services are deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}}, which replaces these two services, prior to 30 March 2025.
{: deprecated}

## Prereqs
{: #migration-remove-plat-prereqs}

Complete the following steps:

- [ ] Review the {{site.data.keyword.logs_routing_full_notm}} configuration and verify that your platform logs are routed to your `cloud_logs` targets.

- [ ]  Check that your {{site.data.keyword.la_full_notm}} instances across all regions are migrated.

- [ ] Get the details of each {{site.data.keyword.la_full_notm}} instance in your account by running the following command: `resource service-instance --id InstanceCRN -o JSON`

- [ ] For alerting, check the integration between each {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance that you use for alerting. For more information, see [Test your connection](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-next).

- [ ] Check that permissions on the new {{site.data.keyword.logs_full_notm}} instances are in place and working for your requirements.


## Steps to remove {{site.data.keyword.la_full_notm}} instances
{: #migration-remove-plat-steps}

Complete the following steps to remove your {{site.data.keyword.la_full_notm}} instances with platform logs enabled:

- [ ] In {{site.data.keyword.logs_routing_full_notm}}, for each region where you operate, remove the `Log Analysis` target configured for the region.

- [ ] If you have other sources, such as Linux services or Kubernetes clusters, for each source that is configured to send logs to {{site.data.keyword.la_full_notm}} in the account, remove the configuration. For example,

    - [ ] Remove `logDNA` agents from sources.

    - [ ] Clean up your rsyslog configuration.

    - [ ] Modify your custom apps that send logs directly by using the REST API.

- [ ] In {{site.data.keyword.iam_full_notm}} (IAM), remove the policies that grant permissions to work with {{site.data.keyword.la_full_notm}} instances in the account.

    - [ ] Remove policies from access groups.

    - [ ] Remove policies from users.

    - [ ] Remove policies from service IDs.

    - [ ] Remove policies from trusted profiles.

- [ ] Delete the {{site.data.keyword.la_full_notm}} instances.
