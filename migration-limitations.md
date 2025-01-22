---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-22"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Migration tool limitations
{: #migration-limitations}

The {{site.data.keyword.logs_full}} migration tool is a command line tool that you can use to migrate your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance configuration to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}


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


### Integration with email
{: #mig-email}

* A user that has been configured to receive emails must accept the invitation to receive emails from the service.


### Dashboards
{: #mig-dashboards}

- The migration tool migrates plots by using the API. Creation via Terraform fails.
- The migration tool does not create views within folders. You must manually drag the dashboard to the created folder.
- The migration tool fails when 2 categories have similar names but differ by 1 or more characters.


### Parsing rules
{: #mig-parsing-rules}

- The migration tool reports the fields that are extracted from current logs. You must manually create extract parsing rules to create new fields from logs.
- If a new field relies on the value of an extracted field, if you use the UI to configure the field, you must first add the field providing the extracted value. Check that the field providing the value to the new field is created, then add the new field.


## Agent migration
{: #mig-agent}

* If you used tags in your {{site.data.keyword.la_full_notm}} or {{site.data.keyword.at_full_notm}} instance, you need to configure new tags in the agents that send data to {{site.data.keyword.logs_full_notm}}. You also need to migrate any queries that filter by tag values. For more information, see [About the {{site.data.keyword.agent}} agent](/docs/cloud-logs?topic=cloud-logs-agent-about).
