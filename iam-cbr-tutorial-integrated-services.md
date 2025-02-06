---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-06"


keywords: tutorials, cbr, firewall, allowlist, rules
subcollection: cloud-logs
content-type: tutorial
completion-time: 10m

---

{{site.data.keyword.attribute-definition-list}}

# Restricting access to integrated services from {{site.data.keyword.logs_full_notm}} using context-based restrictions
{: #iam-cbr-tutorial-integrated-services}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

In this tutorial, you will set up [context-based restrictions](/docs/cloud-logs?topic=cloud-logs-iam-cbr) that will allow access to the following integrated services: {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.en_short}}, but only for requests originating from an {{site.data.keyword.logs_full_notm}} service instance.
{: shortdesc}

## Before you begin
{: #iam-cbr-tutorial-integrated-services-prereqs}

Before you use [context-based restrictions](/docs/cloud-logs?topic=cloud-logs-iam-cbr) with integrated services to only allow requests from an {{site.data.keyword.logs_full_notm}} service you need:

- An instance of your targeted service
- An instance of {{site.data.keyword.logs_full_notm}}
- A role of `Administrator` for context-based restrictions

## Navigate to the context-based restrictions console
{: #iam-cbr-tutorial-integrated-services-console}
{: step}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click **Manage** > **Context-based restrictions**.

## Create a network zone
{: #iam-cbr-tutorial-integrated-services-nw-zone}
{: step}

First, create a network zone with the {{site.data.keyword.logs_full_notm}} service as a service reference. This network zone will allowlist all {{site.data.keyword.logs_full_notm}} service IPs either for specific locations or for all locations (default).

1. Click **Network Zones**
2. Give a meaningful name to your zone.
3. Scroll down to the **Reference a service** section and select {{site.data.keyword.logs_full_notm}} from the services menu. 
4. Optionally, you can choose to allow access only for a specific location or for multiple locations from the locations menu.
5. Click **+** to add the service reference.
6. Click **Next**, then click **Create**.
 
## Create a new rule
{: #iam-cbr-tutorial-integrated-services-rule}
{: step}

Next, create the rule for the targeted service.

1. Click **Rules**.
2. In the service section, select either **{{site.data.keyword.cos_full_notm}}**, **{{site.data.keyword.en_short}}** or **{{site.data.keyword.messagehub}}** from the menu.
3. In the APIs section, select **All**.

## Scope the rule
{: #iam-cbr-tutorial-integrated-services-scope}
{: step}

Now, you can choose the resources where you want to apply the context-based restrictions. You can specify a particular instance, or you can apply the restrictions to all instances.

1. In the resources section, select **specific resources**.
2. Select the service instance that you want the rule to apply to.
3. Click **Continue**.

Now, select the network zone created in the previous steps.

1. Select the network zone and click **Add**.
2. Click **Continue**.


## Describe your rule
{: #iam-cbr-tutorial-integrated-services-describe-rule}
{: step}

In the final step, you can add a description for the rule and choose how you want to enforce it. Once done, click **Create** to activate your new rule.

After you create, enforce, or disable enforcement of a rule, it might take up to 10 minutes for the change to take effect.
{: note}

## Verify the rule
{: #iam-cbr-tutorial-integrated-services-verify}
{: step}

An easy way to verify whether the rule is working as expected is to try accessing your integrated **{{site.data.keyword.cos_full_notm}}**, **{{site.data.keyword.en_short}}** or **{{site.data.keyword.messagehub}}** instances through the IBM Cloud console. Since we've restricted access to these services from {{site.data.keyword.logs_full_notm}} service only, you should be blocked from accessing the instance through the console.

To access your service instance from the console, you can edit the network zone created earlier and add your IP address to the allowed list.
{: tip}

To verify if the {{site.data.keyword.logs_full_notm}} service can access the {{site.data.keyword.cos_full_notm}} service, check whether you are able to see the {{site.data.keyword.cos_full_notm}} instance buckets, where the rule was applied, in the list of buckets that can be attached to your {{site.data.keyword.logs_full_notm}} instance.

![Verify configured buckets](/images/logs-cbr-tutorial/cbr_6.png){: caption="{{site.data.keyword.cos_full_notm}} buckets are listed in the bucket list while configuring the storage for your {{site.data.keyword.logs_full_notm}} instance"}

Similarly, to verify whether the {{site.data.keyword.logs_full_notm}} service can access the {{site.data.keyword.en_short}} service, try sending a test notification from your allowed {{site.data.keyword.logs_full_notm}} instance. For detailed instructions on setting up this integration, see [Configuring an outbound integration to connect {{site.data.keyword.logs_full_notm}} with {{site.data.keyword.en_short}}](/docs/cloud-logs?topic=cloud-logs-event-notifications-configure).

![Sending a test notification](/images/logs-cbr-tutorial/cbr_5.png){: caption="Sending a test notification via {{site.data.keyword.logs_full_notm}}"}

Similarly, to verify whether the {{site.data.keyword.logs_full_notm}} service can access the {{site.data.keyword.messagehub}} service, try sending a test stream from your allowed {{site.data.keyword.logs_full_notm}} instance. For detailed instructions on setting up this integration, see [Integrating {{site.data.keyword.logs_full_notm}} with {{site.data.keyword.messagehub}}](/docs/cloud-logs?topic=cloud-logs-streaming-config)

![Verify using CBR with Event Streams](/images/logs-cbr-tutorial/cbr_event_stream.png){: caption="Sending a sample test stream via {{site.data.keyword.logs_full_notm}}"}
