---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-19"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Removing deprecated {{site.data.keyword.la_full_notm}} instances
{: #migration-remove-la}

After you have migrated to {{site.data.keyword.logs_full}} you will want to remove your deprecated {{site.data.keyword.la_full_notm}} instances in the account.
{: shortdesc}

As of 28 March 2024 the {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} services are deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}}, which replaces these two services, prior to 30 March 2025.
{: deprecated}

## Prereqs
{: #migration-remove-la-prereqs}

Complete the following steps:

- [ ]  Check that {{site.data.keyword.la_full_notm}} instances across all regions are migrated.

- [ ] Get the details of each {{site.data.keyword.la_full_notm}} instance in your account by running the following command: `resource service-instance --id InstanceCRN -o JSON`

- [ ] For alerting, check the integration between each {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_full_notm}} instance that you use for alerting. For more information, see [Test your connection](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure#event-notifications-configure-next).

- [ ] Check that the permissions on the new {{site.data.keyword.logs_full_notm}} instances are in place and working for your requirements.


## Steps to remove {{site.data.keyword.la_full_notm}} instances
{: #migration-remove-la-steps}

Complete the following steps to remove {{site.data.keyword.la_full_notm}} instances:

- [ ] For each source that is configured to send logs to an {{site.data.keyword.la_full_notm}} instance in the account, remove the configuration. For example,

    - [ ] Remove `logDNA` agents from sources.

    - [ ] Clean up your rsyslog configuration.

    - [ ] Modify your custom apps that send logs directly by using the REST API.

    - [ ] If you were sending logs from a Kubernetes cluster to {{site.data.keyword.la_full_notm}}, [detach the logging agent from the cluster](/docs/log-analysis?topic=log-analysis-detach_agent).

- [ ] In {{site.data.keyword.iamlong}} (IAM), remove the policies that grant permissions to work with {{site.data.keyword.la_full_notm}} instances in the account.

    - [ ] Remove policies from access groups.

    - [ ] Remove policies from users.

    - [ ] Remove policies from service IDs.

    - [ ] Remove policies from trusted profiles.

- [ ] Remove any alert configurations or integrations (for example, PagerDuty) between the {{site.data.keyword.la_full_notm}} instance and the destination service.

- [ ] Delete your {{site.data.keyword.la_full_notm}} instances.
