---

copyright:
  years:  2024
lastupdated: "2024-09-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migration tool limitations
{: #migration-limitations}

The {{site.data.keyword.logs_full}} migration tool is a command line tool that you can use to migrate your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance configuration to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

## Using the tool
{: #limitations-migration-tool}

- The migration tool fails creating instances automatically due to the service plan when you run `ibmcloud logging migrate create-resources --api`. If you use the Terraform option `ibmcloud logging migrate create-resources --terraform -f`, change the service plan from `beta` to `standard` before you apply the Terraform scripts.

    This issue is fixed in the migration tool plugin v0.1.10. 
    {: note}

## Custom roles
{: #mig-customroles}

You cannot migrate custom roles that have conflicting permissions when you migrate from {{site.data.keyword.la_full_notm}} and {{site.data.keyword.at_full_notm}} into {{site.data.keyword.logs_full_notm}}.

The exception report indicates when custom roles are identified in the account as part of the migration process.


## {{site.data.keyword.cos_full_notm}} buckets
{: #mig-cos}

* The Migration tool cannot provision and configure [data buckets and metrics buckets](/docs/cloud-logs?topic=cloud-logs-buckets) outside of {{site.data.keyword.cloud_notm}}.

* The migration tool cannot provision and configure [data buckets and metrics buckets](/docs/cloud-logs?topic=cloud-logs-buckets) across {{site.data.keyword.cloud_notm}} accounts.

* The migration tool does not automatically migrate lifecycle policies. Currently, you cannot attach a bucket that has a lifecycle policy configured.

## Custom catalog
{: #mig-customcat}

You must manually update custom catalogs.



## Instance subresources
{: #mig-subresources}

### Data usage configuration
{: #mig-datausage}

You cannot migrate an {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} data usage configuration.

{{site.data.keyword.logs_full_notm}} offers a *Data Usage Report* and a *Detailed Data Usage Report* as part of the service. You must manually enable these features.

    The *Data Usage Report* offers a view of your account usage for the previous 90 days.

    The *Detailed Data Usage Report* offers a view of your data consumtion in a given period of time for either the current month or retroactively 30 or 90 days.



### Integration with PagerDuty
{: #mig-pd}

* Integration with PagerDuty must be done after migration.

### Integration with email
{: #mig-email}

* A user that has been configured to receive emails must accept the invitation to receive emails from the service.


### Dashboards
{: #mig-dashboards}

- The migration tool migrates plots by using the API. Creation via Terraform fails.
- The migration tool does not create views within folders. You must manually drag the dashboard to the created folder.
- The migration tool fails when 2 categories have similar names but differ by 1 or more characters.


### Views
{: #mig-views}


- Creation of views with an empty query fails when using Terraform.

- View folders must have unique names. If you have duplicate category names, views within duplicated categories are not migrated.

### Parsing rules
{: #mig-parsing-rules}

- The migration tool reports the fields that are extracted from current logs. You must manually create extract parsing rules to create new fields from logs.
- If a new field relies on the value of an extracted field, if you use the UI to configure the field, you must first add the field providing the extracted value. Check that the field providing the value to the new field is created, then add the new field.

### Alerts
{: #mig-alerts}

- The migration tool only creates 1 topic that includes all of the alert conditions.


## Platform logs
{: #mig-platform-logs}

- The migration tool only automates the migration of platform logs that are sent to the {{site.data.keyword.la_full_notm}} instance with the platform flag enabled to the migrated {{site.data.keyword.logs_full_notm}} instance. You must manually configure {{site.data.keyword.logs_routing_full_notm}} to send platform logs to the {{site.data.keyword.la_full_notm}} instance.



## Agent migration
{: #mig-agent}

* If you used tags in your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance, you need to configure new tags in the agents that send data to {{site.data.keyword.logs_full_notm}}. You also need to migrate any queries that filter by tag values. For more information, see [About the IBM Cloud Logs Routing agent](/docs/cloud-logs?topic=cloud-logs-agent-about).
