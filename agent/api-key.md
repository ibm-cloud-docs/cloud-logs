---

copyright:
  years:  2023, 2024
lastupdated: "2024-09-02"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}

# Generating an API Key for ingestion
{: #api-key}

When you are using a user account or a service ID, you must generate an API key to open a secure web socket to the ingestion endpoint to authenticate the Logging agent with the {{site.data.keyword.logs_full_notm}} service.
{: shortdesc}

When you are using a user account or service ID, an API key must be created to authenticate the agent. For authentication with trusted profiles, an API key is not required.
{: note}


## Generating an API Key for user authentication
{: #api-key-for-user-id}

A federated user or non-federated user can create an API key to use in the CLI or as part of automation to log in as your user identity.

The API key inherits all assigned access for the user identity for which it is created, and the access is not limited to just the account where the API key is created because it inherits any policies that are assigned to the user. Because the API key that is associated with your user identity has all of the access you're entitled to across any account that you are a member of, you must be cautious with how you use your API key. For more information, see [Managing user API keys](/docs/account?topic=account-userapikey).

You can use the console, CLI, or API to manage your {{site.data.keyword.cloud_notm}} API keys by listing your keys, creating keys, updating keys, or deleting keys.

- [Creating an API key](/docs/account?topic=account-userapikey&interface=ui#create_user_key).
- [Updating an API Key](/docs/account?topic=account-userapikey&interface=ui#update_user_key).
- [Deleting an API key](/docs/account?topic=account-userapikey&interface=ui#delete_user_key).


For example, complete the following steps to generate an API key by using the CLI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

    After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Create an API key for the logged-in account.

    Make sure to log in as the identity with the `Writer` role.{: note}

    ```sh
    export INGESTION_API_KEY=`ibmcloud iam api-key-create logs-router-ingestion --output json | jq -r '.apikey'`
    ```
    {: pre}



## Generating an API Key for service ID authentication
{: #api-key-for-service-id}

You can create a service ID to enable access to the {{site.data.keyword.logs_routing_full_notm}} service by the Logging agent. The agent can be hosted both inside and outside of {{site.data.keyword.cloud}}.

API keys are used by the agent to authenticate as a particular service ID and are granted the access that is associated with that specific service ID. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys).

Make sure to grant the service ID the `Writer` role.
{: note}

- [Creating an API key for a service ID](/docs/account?topic=account-serviceidapikeys&interface=ui#create_service_key).
- [Updating an API key for a service ID](/docs/account?topic=account-serviceidapikeys&interface=ui#update_service_key).
- [Deleting an API key for a service ID](/docs/account?topic=account-serviceidapikeys&interface=ui#delete_service_key).


For example, complete the following steps to generate an API key for a service ID by using the CLI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

    After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Create a service ID that is used for the IAM policies and API key credentials.

    Be sure to give the service ID a description that helps you retrieve the service ID later.

    ```sh
    ibmcloud iam service-id-create logs-router-svc-id --description "Service ID for Logs Router"
    ```
    {: pre}

3. Add an IAM policy for your service ID that grants access to send logs.

    ```sh
    ibmcloud iam service-policy-create <SERVICE_ID> --service-name logs-router --roles Writer
    ```
    {: pre}

4. Create an API key for the service ID.

    Be sure to give the API key a description that helps you retrieve the key later. Save your API key in a secure location. You can't retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` option.

    ```sh
    ibmcloud iam service-api-key-create logs-router-ingestion-key <SERVICE_ID> --description "API key for service ID <SERVICE_ID> with permissions to send logs to the IBM Cloud Logs Routing service"
    ```
    {: pre}
