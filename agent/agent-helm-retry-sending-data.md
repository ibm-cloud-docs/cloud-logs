---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configure the number of retries sending data if an error occurs
{: #agent-helm-retry-sending-data}

When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to set `retryLimit` and indicate whether the agent should retry sending the data to an {{site.data.keyword.logs_full_notm}} instance.

Valid values are:
- `false` to indicate that there is no limit for the number of retries that the scheduler can do. This is the default value.

    The entry in the `logs-values.yaml` file looks as follows:

    ```yaml
    retryLimit: false
    ```
    {: codeblock}

- An integer N value greater or equal to 1.

    The entry in the `logs-values.yaml` file looks as follows:

    ```yaml
    retryLimit: 8
    ```
    {: codeblock}

- *no_retries* to indicate that data is not sent to the destination if it failed the first time.

    The entry in the `logs-values.yaml` file looks as follows:

    ```yaml
    retryLimit: "no_retries"
    ```
    {: codeblock}

For more information, see the [Fluentbit documentation about retries](https://docs.fluentbit.io/manual/administration/scheduling-and-retries) to understand the implications of setting this value.

In some situations, this setting could lead to log data being discarded by the agent due to the inability to send.
