---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-25"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Generating an API Key for ingestion by using a service ID for authentication
{: #iam-ingestion-serviceid-api-key}

You can use a service ID API key to send logs by using the {{site.data.keyword.agent}}.
{: shortdesc}

An individual user ID API key should only be used for non-production environments. If the user creating the API key is no longer an authorized IBM Cloud user, individual user ID API keys associated with that user will no longer be authorized and ingestion will be stopped. Production environments should be configured using [Service ID API keys](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key) or [Trusted Profiles](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-trusted-profile).
{: important}


The API key is used to open a secure web socket to the {{site.data.keyword.logs_full_notm}} ingestion endpoint to authenticate the {{site.data.keyword.agent}}.

API keys are used to authenticate as a particular service ID and are granted the access that is associated with that specific service ID. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys).

Make sure the user who grants the policy has the `Sender` role permissions.
{: important}

Make sure to grant the service ID the `Sender` role before generating the API key.
{: note}

- [Creating an API key for a service ID](/docs/account?topic=account-serviceidapikeys&interface=ui#create_service_key).
- [Updating an API key for a service ID](/docs/account?topic=account-serviceidapikeys&interface=ui#update_service_key).
- [Deleting an API key for a service ID](/docs/account?topic=account-serviceidapikeys&interface=ui#delete_service_key).


## Generating an API Key by using the CLI
{: #iam-ingestion-serviceid-api-key-cli}

Complete the following steps to generate an API key for a service ID by using the CLI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

    After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Create a service ID that is used for the IAM policies and API key credentials.

    Be sure to give the service ID a description that helps you retrieve the service ID later.

    ```sh
    ibmcloud iam service-id-create logs-svc-id --description "Service ID for IBM Cloud Logs"
    ```
    {: pre}

3. Add an IAM policy for your service ID that grants access to send logs.

    ```sh
    ibmcloud iam service-policy-create <SERVICE_ID> --service-name logs --roles Sender
    ```
    {: pre}

4. Create an API key for the service ID.

    Be sure to give the API key a description that helps you retrieve the key later. Save your API key in a secure location. You can't retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` option.

    ```sh
    ibmcloud iam service-api-key-create logs-ingestion-key <SERVICE_ID> --description "API key for service ID <SERVICE_ID> with permissions to send logs to the IBM Cloud Logs service"
    ```
    {: pre}
