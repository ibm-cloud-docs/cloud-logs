---

copyright:
  years:  2024
lastupdated: "2024-04-01"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with {{site.data.keyword.logs_full_notm}}
{: #getting-started}

{{site.data.keyword.logs_full}} is a scalable logging service that persists logs and provides users with capabilities for querying, tailing, and visualizing logs.
{: shortdesc}

Logs are comprised of events that are typically human-readable and have different formats, for example, unstructured text, JSON, delimiter-separated values, key-value pairs, and so on. The {{site.data.keyword.logs_full_notm}} service can manage general purpose application logs, platform logs, or structured audit events. {{site.data.keyword.logs_full_notm}} can be used with logs from both {{site.data.keyword.cloud_notm}} services and customer applications.

The following steps guide you in creating an {{site.data.keyword.logs_full_notm}} service instance, reviewing the UI, and sending logs to the service instance. These steps will let you create an environment for evaluation purposes only.

## Before you begin
{: #gs-prereqs}

You must have a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Registration](https://{DomainName}/login){: external}.

## Step 1. Managing access to {{site.data.keyword.logs_full_notm}} service
{: #gs-iam}

To access and manage the {{site.data.keyword.logs_full_notm}} service, users and service IDs must be assigned access policies. An access policy maps a user or a service ID to certain [IAM roles](/docs/cloud-logs?topic=cloud-logs-iam) where these IAM roles define the actions that the user or the service ID can do with the {{site.data.keyword.logs_full_notm}} service.

Follow the steps in [Granting access to {{site.data.keyword.logs_full_notm}} service](/docs/cloud-logs?topic=cloud-logs-iam-assign-access&interface=ui) to set up access to the {{site.data.keyword.logs_full_notm}} service.

## Step 2. Creating {{site.data.keyword.cos_full_notm}} buckets or using an existing {{site.data.keyword.cos_full_notm}} buckets
{: #gs-creating-cos-bucket}

You need two dedicated {{site.data.keyword.cos_full_notm}} buckets that will be used by your {{site.data.keyword.logs_full_notm}} service instance to store log artifacts.

* A [data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket&interface=cli)
* A [metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket&interface=cli)

Follow the steps in [Create some buckets to store your data](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets) to create new {{site.data.keyword.cos_full_notm}} buckets if you do not already have buckets. If you already have {{site.data.keyword.cos_full_notm}} buckets that you will use with {{site.data.keyword.logs_full_notm}} you can skip this step.

## Step 3. Creating an {{site.data.keyword.logs_full_notm}} service instance
{: #gs-creating-instance}

Next, create an {{site.data.keyword.logs_full_notm}} service. An {{site.data.keyword.logs_full_notm}} instance is created using the {{site.data.keyword.cloud_notm}} catalog.

Follow the steps in [Provisioning an instance](/docs/cloud-logs?topic=cloud-logs-instance-provision&interface=cli) to set up an {{site.data.keyword.logs_full_notm}} instance.


## Step 4. Accessing the {{site.data.keyword.logs_full_notm}} UI
{: #gs-access-ui}

Once you instance is provisioned, you can explore the {{site.data.keyword.logs_full_notm}} UI.

1. [Launch the {{site.data.keyword.logs_full_notm}} UI.](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)
{: #launch-ui}

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

When initially provisioned, you might not see data flowing to the instance, so all dashboards and views might be blank.
{: note}


## Step 5. Routing logs to your {{site.data.keyword.logs_full_notm}} instance
{: #gs-route-logs}

You can configure {{site.data.keyword.logs_routing_full_notm}} in your account to route platform logs to {{site.data.keyword.logs_full_notm}}. 

You can also configure {{site.data.keyword.logs_routing_full_notm}} to route log data from applications on your [{{site.data.keyword.containerlong_notm}}](/docs/containers) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift) clusters to your {{site.data.keyword.logs_full_notm}} instance.

For information on {{site.data.keyword.logs_routing_full_notm}}, see [Getting started with {{site.data.keyword.logs_routing_full_notm}}](/docs/logs-router?topic=logs-router-getting-started).

## Cleaning up
{: #gs-cleaning}

After you have evaluated {{site.data.keyword.logs_full_notm}} and you want to clean up your environment, you can [delete your instance](/docs/cloud-logs?topic=cloud-logs-instance-remove&interface=cli) to remove the {{site.data.keyword.logs_full_notm}} service you created for evaluation.
