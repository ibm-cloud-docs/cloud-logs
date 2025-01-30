---

copyright:
  years:  2024, 2025
lastupdated: "2025-01-30"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Verifying your API key has correct permissions to send logs to {{site.data.keyword.logs_full_notm}}
{: #verify-key}

When sending logs to {{site.data.keyword.logs_full}}, your API key must have the correct permissions. You can check whether your API key has the correct permissions by following a few steps.
{: shortdesc}

1. [Create a Service ID with `sender` permission to {{site.data.keyword.logs_full_notm}}.](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions&interface=ui)

2. [Create an API key for this service ID.](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key&interface=ui)

3. Log in to {{site.data.keyword.cloud_notm}} using the API key.

   ```text
   ibmcloud login --apikey <API_KEY_VALUE>
   ```
   {: pre}

4. Generate a bearer token.

   ```sh
   export IAM_TOKEN=`ibmcloud iam oauth-tokens --output json | jq -r '.iam_token'`
   ```
   {: pre}

5. Send a test log using the API. Make sure you use the [ingress endpoint](/docs/cloud-logs?topic=cloud-logs-endpoints_ingress&interface=ui) for your {{site.data.keyword.logs_full_notm}} instance.

   ```sh
   curl -v --location "https://<InstanceID>.ingress.eu-es.logs.cloud.ibm.com/logs/v1/singles" --header "Content-Type: application/json" --header "Authorization: $IAM_TOKEN" --data '[{
      "applicationName": "myapp",
      "subsystemName": "mysubsystem",
      "text": {"key":"value"}
    }]'
   ```
   {: pre}

6. [Access your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch&interface=ui)

7. Verify that you can see the sample log line you sent in the {{site.data.keyword.logs_full_notm}} UI.

If the sample log line is displayed, then the API key has the correct permissions. If the log line is not displayed, then the Service ID and associated API key does not have the correct permissions.

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned. 
{: important}

