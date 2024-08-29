---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_full_notm}} plug-in parameters
{: #logs-plugin-parameters}


List of parameters that you can configure when using the {{site.data.keyword.logs_routing_full_notm}} agent to send logs directly to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

These parameters only apply when you configure the agent with the `--send-directly-to-icl` flag specified to send logs directly to {{site.data.keyword.logs_full_notm}}. See [{{site.data.keyword.logs_routing_full_notm}} plug-in parameters](/docs/logs-router?topic=logs-router-routing-plugin-parameters) if you are not specifying the `--send-directly-to-icl` flag.
{: important}

## FluentBit parameters
{: #icl-fluentbit}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
| `Name`   |  Name of the plug-in. Must be set to `logger-icl-output-plugin` | n/a  |  `logger-icl-output-plugin` | true  |
| `Id`     |  Unique ID for the plug-in. |  n/a |  any string  | true  |
| `Match`  |  Use to specify how to match events. |  n/a |  any string  | true  |
| `Retry_Limit` |  Retry processing if the plug-in fails to send data to the ingester.  \n Set to `False` if you want to retry forever, otherwise set to an Integer value.  \n For more information about how to configure retries, see [configuring retries](https://docs.fluentbit.io/manual/administration/scheduling-and-retries#configuring-retries){: external} |  1 |  `False` or N >= 1  | true  |
{: caption="Table 1. Fluentbit parameters" caption-side="bottom"}


## Connection parameters
{: #icl-connection_parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Target_Host` |  Specify the host for {{site.data.keyword.logs_full_notm}} ingestion (found in the `Endpoints` section of your {{site.data.keyword.logs_full_notm}} instance `Overview`). Make sure you use the ingress endpoint. |  n/a |  any URL endpoint  | true  |
|  `Target_Port` |  Port number for the connection |  `443` |  any port number  | false  |
|  `Target_Path` |  URL path to be used for the connection |  `/logs/v1/singles` |  any string  | false  |
{: caption="Table 2. Connection parameters" caption-side="bottom"}

## Logging parameters
{: #icl-logging_parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Logging_Level` |  Specify the log level to be used in the plug-in |  `info` |  `debug`  \n `info`  \n `error`  | false  |
|  `Package_Size` | Specify the package size in KB or MB | `2` | any number followed by a unit, for example, `2MB`, `10KB`. Must be less than `2MB` | false |
{: caption="Table 3. Logging parameters" caption-side="bottom"}


## Authentication parameters
{: #icl-authentication_parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Authentication_Mode` |  Specify the authentication mode |  `TrustedProfile` | `TrustedProfile`  \n `IAMAPIKey`  | false  |
|  `IAM_Environment` |  Specify the IAM environment for authentication |  `Production` |  `Production` specifies the public endpoint `iam.cloud.ibm.com`  \n `PrivateProduction` specifies the private endpoint `private.iam.cloud.ibm.com` | false  |
|  `CR_Token_Mount_Path` |  Path where the CRToken is present |  `/var/run/secrets/tokens/vault-token` | any string  | false - Only used when Authentication_Mode is set to TrustedProfile  |
|  `Trusted_Profile_ID` |  ID of the Trusted Profile to be used |  n/a |  any string	  | true - Only used when Authentication_Mode is set to TrustedProfile |
{: caption="Table 4. Authentication parameters" caption-side="bottom"}


