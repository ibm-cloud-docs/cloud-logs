---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_routing_full_notm}} plug-in parameters
{: #routing-plugin-parameters}


List of parameters that you can configure for a {{site.data.keyword.logs_routing_full_notm}} agent.
{: shortdesc}

These parameters only apply if the agent is configured without specifying the the `--send-directly-to-icl` flag. See [{{site.data.keyword.logs_full_notm}} plug-in parameters](/docs/logs-router?topic=logs-router-logs-plugin-parameters) if you specified the `--send-directly-to-icl` flag to route logs directly to {{site.data.keyword.logs_full_notm}}.
{: important}

## FluentBit parameters
{: #fluentbit}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
| `Name`   |  Name of the plug-in. Must be set to `logger-agent-plugin` | n/a  |  `logger-agent-plugin` | true  |
| `Id`     |  Unique ID for the plug-in. |  n/a |  any string  | true  |
| `Match`  |  Use to specify how to match events. |  n/a |  any string  | true  |
| `Retry_Limit` |  Retry processing if the plug-in fails to send data to the ingester.  \n Set `False` if you want to retry forever, otherwise set to an Integer value.  \n For more information about how to configure retries, see [here](https://docs.fluentbit.io/manual/administration/scheduling-and-retries#configuring-retries){: external} |  1 |  `False` or N >= 1  | true  |
{: caption="Table 1. Fluentbit parameters" caption-side="bottom"}


## Connection parameters
{: #connection_parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Target_Host` |  Ingest hostname to be used for connection |  n/a |  any url endpoint  | true  |
|  `Target_Port` |  Ingest Port to be used for connection |  `443` |  any port number  | false  |
|  `Target_Path` |  URL path to be used for connection |  `/v1/logs/ws` |  any string  | false  |
|  `Insecure_TLS` |  Allow insecure TLS connections |  `false` |  any bool  | false  |
|  `Is_Ack_Enabled` |  Enables per message acknowledgements |  `false` |  any bool  | false  |
{: caption="Table 2. Connection parameters" caption-side="bottom"}

## Logging parameters
{: #logging_parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Logging_Level` |  Specify the log level to be used in the plug-in |  `info` |  `debug`  \n `info`  \n `error`  | false  |
{: caption="Table 3. Logging parameters" caption-side="bottom"}


## Authentication parameters
{: #authentication_parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Authentication_Mode` |  Specify the authentication mode |  `TrustedProfile` | `TrustedProfile`  \n `IAMAPIKey`  | false  |
|  `IAM_Environment` |  Specify the IAM environment for authentication |  `Production` |  `Production` specifies the public endpoint `iam.cloud.ibm.com`  \n `PrivateProduction` specifies the private endpoint `private.iam.cloud.ibm.com` | false  |
|  `CR_Token_Mount_Path` |  Path where the CRToken is present |  `/var/run/secrets/tokens/vault-token` | any string  | false - Only used when Authentication_Mode is set to TrustedProfile  |
|  `Trusted_Profile_ID` |  ID of the Trusted Profile to be used |  n/a |  any string	  | true - Only used when Authentication_Mode is set to TrustedProfile |
{: caption="Table 4. Authentication parameters" caption-side="bottom"}
