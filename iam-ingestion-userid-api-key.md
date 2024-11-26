---

copyright:
  years:  2023, 2024
lastupdated: "2024-11-26"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Generating an API Key for ingestion by using a user ID for authentication
{: #iam-ingestion-userid-api-key}

You can use a user ID API key to send logs by using the Ingestion REST API.
{: shortdesc}

The API key is used to open a secure web socket to the {{site.data.keyword.logs_full_notm}} ingestion endpoint to authenticate the API request with the {{site.data.keyword.logs_full_notm}} service.

A federated user or non-federated user can create an API key to use in the CLI or as part of automation to log in as your user identity.

The API key inherits all assigned access for the user identity for which it is created, and the access is not limited to just the account where the API key is created because it inherits any policies that are assigned to the user. Because the API key that is associated with your user identity has all of the access you're entitled to across any account that you are a member of, you must be cautious with how you use your API key. For more information, see [Managing user API keys](/docs/account?topic=account-userapikey).

You can use the console, CLI, or API to manage your {{site.data.keyword.cloud_notm}} API keys by listing your keys, creating keys, updating keys, or deleting keys.

- [Creating an API key](/docs/account?topic=account-userapikey&interface=ui#create_user_key).
- [Updating an API Key](/docs/account?topic=account-userapikey&interface=ui#update_user_key).
- [Deleting an API key](/docs/account?topic=account-userapikey&interface=ui#delete_user_key).


## Generating an API Key by using the CLI
{: #iam-ingestion-userid-api-key-cli}

Complete the following steps to generate an API key by using the CLI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

    After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Add an IAM policy for your user ID that grants access to send logs.

    ```sh
    ibmcloud iam user-policy-create <USER_ID> --service-name logs --roles Sender
    ```
    {: pre}

3. Create an API key for the logged-in account.

    Make sure to log in as the identity with the `Sender` role.{: note}

    ```sh
    export INGESTION_API_KEY=`ibmcloud iam api-key-create logs-ingestion --output json | jq -r '.apikey'`
    ```
    {: pre}
