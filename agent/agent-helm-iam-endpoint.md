---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configure the IAM endpoint by using Helm
{: #agent-helm-iam-endpoint}

When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to set `env.iamEnvironment` to control the IAM endpoint that is used by the agent to exchange the tokens.

The default value is `Production`.

Valid values are: `Production`, `PrivateProduction` and `Custom`.

Update the file named `logs-values.yaml` that you use to deploy or upgrade the agent with the following content:

- Set `Production` to use the `iam.cloud.ibm.com` default endpoint

    Sample `logs-values.yaml` file looks as follows:

    ```yaml
    env:
      iamEnvironment: "Production"
    ```
    {: codeblock}

- Set `PrivateProduction` to use the `private.iam.cloud.ibm.com` endpoint

    Sample `logs-values.yaml` file looks as follows:

    ```yaml
    env:
      iamEnvironment: "PrivateProduction"
    ```
    {: codeblock}

- Set `Custom` to use a custom IAM endpoint (for example `private.eu-de.iam.cloud.ibm.com`). You must also set `env.iamHost`.

    Sample `logs-values.yaml` file looks as follows:

    ```yaml
    env:
      iamEnvironment: "Custom"
      iamHost: "private.eu-de.iam.cloud.ibm.com"
    ```
    {: codeblock}


After you modify the `logs-values.yaml`, you can [Upgrade the agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update) or continue modifying the file before applying all the changes.
