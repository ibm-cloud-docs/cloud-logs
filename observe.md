---

copyright:
  years:  2023, 2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Managing logging instances in the account through the Observability UI
{: #observe}

You can manage your {{site.data.keyword.logs_full}} instances through the `Observability` dashboard in the {{site.data.keyword.cloud_notm}}.
{: shortdesc}


## Launching the Logging instances UI 
{: #observe-cloud-ui}

You launch the Logging instances UI from the {{site.data.keyword.cloud_notm}} console.

Complete the following steps to launch the UI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](/icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Logging**. By default **Instances** are displayed. You might need to click the **Cloud Logs** tab to see your {{site.data.keyword.logs_full_notm}} instances.

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

   If the instances are not displayed, click **Instances** to display the list of logging instances.


## Managing {{site.data.keyword.logs_full}} logging instances
{: #observe_manage}

On the **Logging instances** page, you can manage your {{site.data.keyword.logs_full_notm}} instances.

* You can view all instances across all locations.

   For each instance, you can view the following information:

   * The status of an instance.
   * The resource group that is associated with an instance.
   * The region where the instance is provisioned.
   * The service plan of an instance.

* You can filter the list of instances:

   * By resource groups.
   * By regions.
   * By searching for a specific string.

   Only resource groups and regions that have configured instances in your account will be available for filtering.
   {: note}
   
* You can [create new instances](/docs/cloud-logs?topic=cloud-logs-instance-provision&interface=ui#instance-provision-ui).

Using the **Actions** icon ![Actions icon](/icons/action-menu-icon.svg "Actions") associated with your {{site.data.keyword.logs_full}} instances, you can also:

* View the endpoints associated with the instance.
* View the {{site.data.keyword.logs_full_notm}} documentation.
* View an access report including the list of users, access groups, and service IDs that have access to the instance.
* Manage access to the instance.
* Delete the instance.


