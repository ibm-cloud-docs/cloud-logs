---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-20"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Retrieving an access token
{: #retrieve-access-token}

You must get an {{site.data.keyword.iamlong}} (IAM) access token to authenticate your requests to the {{site.data.keyword.logs_routing_full}} service.
{: shortdesc}

## Retrieving an access token with the CLI
{: #retrieve-token-cli}
{: cli}

You can use the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external} to quickly generate your personal Cloud IAM [access token](#x2113001){: term}.

1. Log in to {{site.data.keyword.cloud_notm}} with the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external}.

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time pass code.
    {: note}

2. Run the following command to retrieve your {{site.data.keyword.cloud_notm}} IAM access token and export it as an environment variable by running the following command:

    ```sh
    export IAM_TOKEN=`ibmcloud iam oauth-tokens --output json | jq -r '.iam_token'`
    ```
    {: pre}

## Retrieving an access token with the API
{: #retrieve-token-api}
{: api}

You can also retrieve your access token programmatically by first creating a [service ID API key](/docs/account?topic=account-serviceidapikeys){: external} for your application, and then exchanging your API key for an {{site.data.keyword.cloud_notm}} IAM token.

1. Create a [service ID API key](/docs/account?topic=account-serviceidapikeys){: external}.

2. Call the [IAM Identity Services API](/apidocs/iam-identity-token-api){: external} to retrieve your access token.

    ```sh
    $ curl -X POST \
        "https://iam.cloud.ibm.com/identity/token" \
        -H "content-type: application/x-www-form-urlencoded" \
        -H "accept: application/json" \
        -d 'grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>' > token.json
    ```
    {: codeblock}

    In the request, replace `<API_KEY>` with the API key that you created in the previous step. The following truncated example shows the contents of the `token.json` file:

    ```json
    {
        "access_token": "b3VyIGZhdGhlc...",
        "expiration": 1512161390,
        "expires_in": 3600,
        "refresh_token": "dGhpcyBjb250a...",
        "token_type": "Bearer"
    }
    ```
    {: screen}

Access tokens are valid for 1 hour, but you can regenerate them as needed.
{: note}
