---

copyright:
  years:  2024
lastupdated: "2024-10-09"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Navigating to the UI
{: #instance-launch}

After you provision an instance of the {{site.data.keyword.logs_full}} service in the {{site.data.keyword.cloud_notm}}, and configure a logging agent for a log data source, you can view, monitor, and manage logs through the {{site.data.keyword.logs_full_notm}} UI.
{: shortdesc}


## Granting IAM policies to a user to launch the UI
{: #instance-launch-iam}

Users in your account need permissions to launch the UI.

You must be an administrator of the {{site.data.keyword.logs_full_notm}} service, an administrator of an {{site.data.keyword.logs_full_notm}} instance, or have account IAM permissions to grant other users policies.
{: note}

The following table lists the minimum policies that a user must have to be able to launch the UI and view data:

| Service                              | Role                      | Permission granted       |
|--------------------------------------|---------------------------|---------------------|
| `{{site.data.keyword.logs_full_notm}}` | Platform role: Viewer     | Allows the user to view the list of service instances in the Observability Logging Instances dashboard. |
| `{{site.data.keyword.logs_full_notm}}` | Service role: Reader      | Allows the user to launch the UI and view logs.    |
{: caption="IAM policies" caption-side="top"}

For more information on how to configure these policies for a user, see [Granting permissions to a user to view logs](/docs/cloud-logs?topic=cloud-logs-iam-assign-access&interface=ui).


## Launching the UI through the {{site.data.keyword.cloud_notm}} UI
{: #instance-launch-cloud-ui}

You launch the logging UI within the context of an {{site.data.keyword.logs_full_notm}} instance, from the {{site.data.keyword.cloud_notm}} console.

Complete the following steps to launch the UI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](/icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Logging**. By default **Instances** are displayed. 

4. Click the **Cloud Logs** tab.

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

   If the instances are not displayed, click **Instances** > **Cloud Logs** to display the list of logging instances.

4. Click **Open dashboard** for your selected instance.

The UI opens in a new browser tab.
