---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configure the authentication method by uysing Helm
{: #agent-helm-iam-authentication}

When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to include the `env.iamMode` so you choose the authentication method to use by the agent when sending logs to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

You can choose an IAM APIKey or a Trusted Profile configuration.

Valid values are: `TrustedProfile` and `IAMAPIKey`.


Consider the following information when setting this parameter:

- If `env.iamMode: "TrustedProfile"` is set, then the `env.trustedProfileID` variable must also be provided.

- If `env.iamMode: "IAMAPIKey"` is set, then the configuration expects a secret to be defined that contains an IAM Apikey with permissions.

    If the `secret.iamAPIKey` variable is provided on the helm command (for example `--set secret.iamAPIKey=<your iamAPIKey>`), then the helm chart will create the Kubernetes secret.

    Alternatively, you can create the secret ahead of time with the command: (Make sure you are connected to your cluster.)

    ```sh
    kubectl create secret generic <helm install-name> -n ibm-observe --from-literal=IAM_API_KEY=<apikey>
    ```
    {: codeblock}


Update the file named `logs-values.yaml` that you use to deploy or upgrade the agent with the following content:

- For the value `TrustedProfile`, enter:

    ```yaml
    env:
      iamMode: "TrustedProfile"
      trustedProfileID: "Profile-yyyyyyyy-xxxx-xxxx-yyyy-zzzzzzzzzzzz"
    ```
    {: codeblock}

- For the value `IAMAPIKey`, enter:

    ```yaml
    env:
      iamMode: "IAMAPIKey"
    ```
    {: codeblock}


After you modify the `logs-values.yaml` file, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
