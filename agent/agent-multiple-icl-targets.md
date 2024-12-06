---

copyright:
  years:  2024
lastupdated: "2024-12-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Configuring multiple {{site.data.keyword.logs_full_notm}} destinations
{: #multi-icl-config}

When multiple different workloads are running in the same environment, the {{site.data.keyword.agent}} can be configured to separate their logs and send them to different {{site.data.keyword.logs_full_notm}} destinations.
{: shortdesc}

Most of the configuration is done in the agent itself.
It is possible to set up multiple output instances of the {{site.data.keyword.logs_full_notm}} output plug-in.

## Before you begin
{: #multi-icl-prereqs}

Be sure that you have completed the following steps:

1. Have already created two {{site.data.keyword.logs_full_notm}} destination instances.
2. Have authentication, either using an API key or trusted profile, for both your {{site.data.keyword.logs_full_notm}} instances.
3. Have already deployed the {{site.data.keyword.agent}} and are ready to modify its configuration.
   - For more information, see [managing the agent for Openshift](/docs/cloud-logs?topic=cloud-logs-agent-openshift) for deploying to Openshift clusters.
   - For more information, see [managing the agent for Kubernetes](/docs/cloud-logs?topic=cloud-logs-agent-std-cluster) for deploying to Kubernetes clusters.
   - For more information, see [managing the agent for Linux](/docs/cloud-logs?topic=cloud-logs-agent-linux) for deploying on Linux.
   - For more information, see [managing the agent for Windows](/docs/cloud-logs?topic=cloud-logs-agent-windows) for deploying on Windows systems.


## Configuring tags for the input plug-ins
{: #multi-icl-input-plugins}

In this example, `dummy` input plug-ins are used. An actual configuration will use `tail` or similar plug-ins.

The relevant part for a multi target use case is the `Tag` parameter.
This parameter configures events from various inputs to be directed to specific output and filter plug-ins.
In this case, the two input plug-ins have distinct tags so that they can be routed to different targets.

```text
[INPUT]
    Name       dummy
    Alias      icl-instance-one
    Dummy      {"message": "test message for ICL instance one"}
    Tag        dummy.multi.instance.one
    Rate       1

[INPUT]
    Name       dummy
    Alias      icl-instance-two
    Dummy      {"message": "test message for ICL instance two"}
    Tag        dummy.multi.instance.two
    Rate       1
```
{: codeblock}

## Configuring the output plug-in for {{site.data.keyword.logs_full_notm}}
{: #multi-icl-output-icl}

For the output, the plug-in will be the {{site.data.keyword.logs_full_notm}} output plug-in configured for your {{site.data.keyword.logs_full_notm}} instance destinations.

For details about configuring the {{site.data.keyword.logs_full_notm}} agent output plug-in, see [plug-in parameters](/docs/cloud-logs?topic=cloud-logs-agent-plugin-parameters).

The `Match` parameter corresponds to one of the tags previously specified in the input plug-ins. The ID must be unique for each [OUTPUT] section.
{: note}

```conf
[OUTPUT]
    Name                logger-icl-output-plugin
    Id                  logger-icl-output-plugin-instance-one
    Match               dummy.multi.instance.one

    # Connection
    Target_Host         <ICL_INSTANCE_ENDPOINT>
    Target_Port         443
    Target_Path         /logs/v1/singles

    # Authentication
    Authentication_Mode IAMAPIKey
    IAM_Environment     Production
    IAM_API_key         ${ENV_VAR_API_KEY_INSTANCE_1}

[OUTPUT]
    Name                logger-icl-output-plugin
    Id                  logger-icl-output-plugin-instance-two
    Match               dummy.multi.instance.two

    # Connection
    Target_Host         <ICL_INSTANCE_ENDPOINT>
    Target_Port         443
    Target_Path         /logs/v1/singles

    # Authentication
    Authentication_Mode IAMAPIKey
    IAM_Environment     Production
    IAM_API_key         ${ENV_VAR_API_KEY_INSTANCE_2}
```
{: codeblock}

When using an API key, you need to provide this API key in the [OUTPUT] stanza it belongs to.
This can also be used to work with multiple {{site.data.keyword.logs_full_notm}} instances located in different accounts.
To not persist the API key in a configuration file for security reasons, it is strongly recommended to provide the API key in a unique environment variable and refer to it with the following notation: `IAM_API_key ${NAME_OF_ENV_VARIABLE_WHERE_API_KEY_IS_STORED}`.
{: tip}
