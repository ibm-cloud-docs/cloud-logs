---

copyright:
  years:  2023, 2024
lastupdated: "2024-11-26"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Generating a Trusted Profile for ingestion
{: #iam-ingestion-trusted-profile}

You can use a Trusted Profile (TP) to send logs from a compute resource in {{site.data.keyword.cloud_notm}} to an {{site.data.keyword.logs_full_notm}} instance by using the {{site.data.keyword.agent}}.
{: shortdesc}


## Creating a Trusted Profile for ingestion
{: #iam-ingestion-trusted-profile-create}

Complete the following steps to create a Trusted Profile:


1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Access (IAM) > Trusted profiles**. Then, click **Create profile**.

2. Describe your profile by providing a name and a description. Then, click **Continue**.

3. Establish trust. Select the trusted profile entity **Compute resources**.

5. Create a trust relationship.

    - Select a *Compute service type*. For example, choose **Kubernetes**.

    - In the *Select compute resource* section, click **Specific resources> Add a resource**. Then, choose your resource. For a Kubernetes compute resource, you must choose the Kubernetes cluster where you plan to deploy the agent.

    - Click **Continue**.

6. Assign access. Select **Access policy**.

    The role that is required for sending logs to {{site.data.keyword.logs_full_notm}} is `Sender`. For more information, see [Setting up IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-agent-iam-permissions).

    - Select the service **Cloud Logs**. Then, click **Next**.

    - In *Resources*, select **Specific resources**. Choose the {{site.data.keyword.logs_full_notm}} instance where you plan to send the logs. Then, click **Next**.

    - In the **Roles and actions**, select the service access **Sender**. Then, click **Next**.

    - Click **Add > Create**.

For more information about the fields that are used to create conditions for trusted profiles, see IAM condition properties. {: tip}
