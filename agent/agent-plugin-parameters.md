---

copyright:
  years:  2024
lastupdated: "2024-09-16"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Output plug-in parameters to send data to an {{site.data.keyword.logs_full_notm}} instance
{: #agent-plugin-parameters}


List of parameters that you can use to configure the output plugin to send data to an {{site.data.keyword.logs_full_notm}} instance in the {{site.data.keyword.agent}}.
{: shortdesc}

## FluentBit parameters
{: #agent-plugin-parameters-fluentbit}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
| `Name`   |  Name of the plug-in. Must be set to `logger-icl-output-plugin` | n/a  |  `logger-icl-output-plugin` | true  |
| `Id`     |  Unique ID for the plug-in. |  n/a |  any string  | true  |
| `Match`  |  Use to specify how to match events. |  n/a |  any string  | true  |
| `Retry_Limit` |  Retry processing if the plug-in fails to send data to Cloud Logs.  \n Set `False` if you want to retry forever, otherwise set to an Integer value.  \n For more information about how to configure retries, see [here](https://docs.fluentbit.io/manual/administration/scheduling-and-retries#configuring-retries){: external} |  1 |  `False` or N >= 1  | true  |
{: caption="Table 1. Fluentbit parameters" caption-side="bottom"}


## Connection parameters
{: #agent-plugin-parameters-connection-parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Target_Host` |  Ingest hostname to be used for connection |  n/a |  any url endpoint  | true  |
|  `Target_Port` |  Ingest Port to be used for connection |  `443` |  any port number  | false  |
|  `Target_Path` |  URL path to be used for connection |  `/logs/v1/singles` |  any string  | false  |
{: caption="Table 2. Connection parameters" caption-side="bottom"}

## Logging parameters
{: #agent-plugin-parameters-logging-parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Logging_Level` |  Specify the log level to be used in the plug-in |  `info` |  `debug`  \n `info`  \n `error`  | false  |
|  `Package_Size` | Specify the package size in KB or MB | `2` | any number followed by a unit, for example, `2MB`, `10KB`. Must be less than `2MB` | false |
{: caption="Table 3. Logging parameters" caption-side="bottom"}


## Authentication parameters
{: #agent-plugin-parameters-authentication-parms}

|  Key   |  Description |  Default | Value Choices  | Required  |
|--------|---|---|---|---|
|  `Authentication_Mode` |  Specify the authentication mode |  `TrustedProfile` | `TrustedProfile`  \n `IAMAPIKey`  | false  |
|  `IAM_Environment` |  Specify the IAM environment for authentication |  `Production` |  `Production` specifies the public endpoint `iam.cloud.ibm.com`  \n `PrivateProduction` specifies the private endpoint `private.iam.cloud.ibm.com` | false  |
|  `CR_Token_Mount_Path` |  Path where the CRToken is present |  `/var/run/secrets/tokens/vault-token` | any string  | false - Only used when Authentication_Mode is set to TrustedProfile  |
|  `Trusted_Profile_ID` |  ID of the Trusted Profile to be used |  n/a |  any string	  | true - Only used when Authentication_Mode is set to TrustedProfile |
{: caption="Table 4. Authentication parameters" caption-side="bottom"}

When `Authentication_Mode` is set to `IAMAPIKey`, consider the following information:

- The API key must be specified in an environment variable called IAM_API_KEY.
- If no value is provided in the IAM_API_KEY variable, the plug-in initialization will fail.
