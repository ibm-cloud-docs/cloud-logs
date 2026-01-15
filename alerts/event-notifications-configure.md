---

copyright:
  years:  2024, 2026
lastupdated: "2026-01-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Configuring an outbound integration to connect {{site.data.keyword.logs_full_notm}} with {{site.data.keyword.en_full_notm}}
{: #event-notifications-configure}

To send events that are generated when an alert is triggered in an {{site.data.keyword.logs_full_notm}} instance, you must connect your {{site.data.keyword.logs_full_notm}} instance to {{site.data.keyword.en_short}} by configuring an outbound integration.
{: shortdesc}

## Prereqs
{: #event-notifications-configure-prereqs}

- Learn about alerts in {{site.data.keyword.logs_full_notm}}. For more information, see [Alerting](/docs/cloud-logs?topic=cloud-logs-alerts).
- Learn about {{site.data.keyword.en_full_notm}}. For more information, see [What is {{site.data.keyword.en_full_notm}}?](/docs/event-notifications?topic=event-notifications-en-about).
- Before you can enable notifications for {{site.data.keyword.logs_full_notm}}, be sure that you have an [{{site.data.keyword.en_short}} instance](/catalog/services/event-notifications){: external} and permisions to configure resources in the {{site.data.keyword.en_short}} instance.


## Step 1. Define a service to service authorization
{: #event-notifications-configure-step1}

A service to service authorization is used in the {{site.data.keyword.cloud_notm}} account to authorize the {{site.data.keyword.logs_full_notm}} service to send events to the {{site.data.keyword.en_short}} service.

You must configure a service to service authorization between the {{site.data.keyword.logs_full_notm}} instance and the {{site.data.keyword.en_short}} instance. For more information, see [Creating a S2S authorization to work with the IBM Cloud Event Notifications service](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-en).


## Step 2. Configuring an outbound integration by using the API
{: #event-notifications-configure-step2-api}
{: api}

You can only define via API the integration between an {{site.data.keyword.logs_full_notm}} instance and an {{site.data.keyword.en_short}} instance that is located in a different account. For information about the API method, see [Create an outbound integration](https://cloud.ibm.com/apidocs/logs-service-api#create-outgoing-webhook){: external}.

For example, you can use the following cURL command to create an integration via API:

```bash
curl -X POST "https://API-ENDPOINT/v1/outgoing_webhooks" \
 -H "Authorization: ${IAM_TOKEN}" \
 -H "Accept: application/json" \
 -H "Content-Type: application/json" \
 -d '{
  "type": "ibm_event_notifications",
  "name": "<NAME>",
  "ibm_event_notifications": {
   "event_notifications_instance_id": "<EventNotificationsInstanceID>",
   "region_id": "<Region-of-EventNotifications-Instance>",
   "endpoint_type": "default_or_public"
  }
 }'
```
{: codeblock}

Where
- `API-ENDPOINT`: Set the API endpoint for the {{site.data.keyword.logs_full_notm}} instance.
- `type`: Defines the type of integration. Set to **ibm_event_notifications**.
- `name`: Enter a name for this resource definition.
- `IAM_TOKEN`: Enter the IAM_TOKEN. You can run the following command to get the IAM token: `export IAM_TOKEN=`ibmcloud iam oauth-tokens --output json | jq -r '.iam_token'``
- `event_notifications_instance_id`: Set to the {{site.data.keyword.en_short}} instance ID.
- `region_id`: Set to the region where the {{site.data.keyword.en_short}} instance is available.
- `endpoint_type`: Define whether the integration goes through the public or the private network. Valid values are: `default_or_public`,or `private`

## Step 2. Configuring an outbound integration in the UI
{: #event-notifications-configure-step2-ui}
{: ui}

Complete the following steps to configure an outbound integration:

1. In the console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Resource list**.
2. Select your instance of {{site.data.keyword.logs_full_notm}}.
3. In the {{site.data.keyword.logs_full_notm}} navigation, click the **Integrations** icon ![Integrations icon](../icons/integrations.svg) > **Outbound integrations**.
4. In the outbound integrations section, find {{site.data.keyword.en_short}} and click **Add**.
5. On the *Integrations* page, click **Add new**.
6. If an IAM authorization between {{site.data.keyword.logs_full_notm}} and {{site.data.keyword.en_short}} doesn't exist in your account, you must configure one by clicking **IAM Authorizations**. Follow the prompts to grant access between the services. For more information, see [Creating a S2S authorization to work with the IBM Cloud Event Notifications service](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-en).
7. Enter a name for the integration.
8. Select the {{site.data.keyword.en_short}} service instance that you want to connect to your {{site.data.keyword.logs_full_notm}} instance.
9. Select the **Endpoint Type** as public or private. For more information, see [Service endpoints for Event Notifications](/docs/event-notifications?topic=event-notifications-en-regions-endpoints#en-service-endpoints)
10. To confirm the connection, click **Save**.

An {{site.data.keyword.en_full_notm}} *source* is created with the following name:

```
IBM Cloud Logs - <CLOUD_LOGS_INSTANCE_ID>
```
{: codeblock}

For example, the source name in {{site.data.keyword.en_full_notm}} looks as follows:

```
IBM Cloud Logs - rfdt3147-484f-4dee-b3c7-ab0c85a8e5c7
```
{: codeblock}

The name of the outbound integration is not used to name the source in the {{site.data.keyword.en_full_notm}} instance.
{: note}

## Test your connection
{: #event-notifications-configure-next}

After you enable notifications for {{site.data.keyword.logs_full_notm}}, test your connection to ensure that the events that are generated by {{site.data.keyword.logs_full_notm}} are being forwarded to {{site.data.keyword.en_short}}.

First, complete the following steps in the {{site.data.keyword.en_short}} instance:
1. Verify the source with name `IBM Cloud Logs - <CLOUD_LOGS_INSTANCE_ID>`, that matches your integration name, is created in the {{site.data.keyword.en_full_notm}} instance.

    1. Select **Sources**.
    2. Look for the source with name `IBM Cloud Logs - <CLOUD_LOGS_INSTANCE_ID>`.

2. Create a topic that specifies this Cloud Logs instance as the source and "Event type" scoped to "Test Event".

    1. Select **Topics**. Then, click **Create**.
    2. Enter a topic name, for example, `CloudLogsInstance-test`.
    3. Select the source `IBM Cloud Logs - <CLOUD_LOGS_INSTANCE_ID>` for the instance whose integration you want to test.
    4. Select the *Event type* **Test Event**.
    4. Select **Add a condition > Save source**.
    6. Click **Create**.

3. Create a destination and [verify the destination is configured](/docs/event-notifications?topic=event-notifications-en-test-destination#en-test-destinations). For example, you can configure a Slack destination or an email.

4. Create a Subscription pairing the topic and the destination.
    1. Enter a name, for example, `Test integration`.
    2. Select the topic `CloudLogsInstance-test`.
    3. Select a destination.
    4. Click **Create**.

Next, in the {{site.data.keyword.logs_full_notm}} UI, complete the following steps:
1. Edit the outbound integration.
2. Click **Test**.
3. Check your chosen destination and verify the test event has been sent.
