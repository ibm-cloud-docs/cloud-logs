---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}

# Configuring multiple {{site.data.keyword.logs_full_notm}} destinations
{: #multi-icl-config}

When multiple different workloads are running in the same environment,
the {{site.data.keyword.logs_routing_full_notm}} agent can be configured to separate their logs and send them to different {{site.data.keyword.logs_full_notm}} destinations.
{: shortdes}

Most of the configuration is done in the agent itself.
Since the {{site.data.keyword.logs_full_notm}} output plug-in can only be used once,
logs destined for the second {{site.data.keyword.logs_full_notm}} instance must be routed through {{site.data.keyword.logs_routing_full_notm}} first.

## Before you begin
{: #multi-icl-prereqs}

Be sure that you have completed the following steps:

1. Have already created two {{site.data.keyword.logs_full_notm}} destination instances.
2. Have authentication, either using an API key or trusted profile, for both your {{site.data.keyword.logs_full_notm}} instances, as well as for  {{site.data.keyword.logs_routing_full_notm}} in your environment
3. Have already deployed the {{site.data.keyword.logs_routing_full_notm}} agent and are ready to modify its configuration.
   - For more information, see [managing the agent for Openshift](/docs/logs-router?topic=logs-router-agent-openshift) for deploying to Openshift clusters.
   - For more information, see [managing the agent for Kubernetes](/docs/logs-router?topic=logs-router-agent-std-cluster) for deploying to Kubernetes clusters.
   - For more information, see [managing the agent for Linux](/docs/logs-router?topic=logs-router-agent-linux) for deploying on Linux.

## Load the {{site.data.keyword.logs_full_notm}} output plug-in
{: #multi-icl-plugin-load}

Modify the `plugins.conf` file of your {{site.data.keyword.logs_routing_full_notm}} agents to include both the {{site.data.keyword.logs_routing_full_notm}} output plug-in as well as the {{site.data.keyword.logs_full_notm}} output plug-in as follows:

```text
[PLUGINS]
    Path    /fluent-bit/bin/logs-router-agent-plugin.so
    Path    /fluent-bit/bin/logs-router-icl-output-plugin.so
```
{: codeblock}

## Configuring tags for the input plug-ins
{: #multi-icl-input-plugins}

In this example, `dummy` input plug-ins are used. An actual configuration will use `tail` or similar plug-ins.

The relevant part for a multi target use case is the `Tag` parameter.
This parameter configures events from various inputs to be directed to specific output and filter plug-ins.
In this case, the two input plug-ins have distinct tags so that they can be routed to different targets.

```text
[INPUT]
    Name       dummy
    Alias      dummy-multi-direct
    Dummy      {"message": "test message multi-target direct"}
    Tag        dummy.multi.direct
    Rate       1

[INPUT]
    Name       dummy
    Alias      dummy-multi-iclr
    Dummy      {"message": "test message multi-target through iclr"}
    Tag        dummy.multi.iclr
    Rate       1
```
{: codeblock}

## Configuring the output plug-in for {{site.data.keyword.logs_full_notm}}
{: #multi-icl-output-icl}

For the output, the first plug-in will be the {{site.data.keyword.logs_full_notm}} output plug-in
configured for your first {{site.data.keyword.logs_full_notm}} instance destination.

For details about configuring the {{site.data.keyword.logs_full_notm}} agent output plug-in, see [plug-in parameters](/docs/logs-router?topic=logs-router-logs-plugin-parameters).

The `Match` parameter corresponds to one of the tags previously specified in the input plug-ins.
{: note}

```conf
[OUTPUT]
    Name                logger-icl-output-plugin
    Id                  logger-icl-output-plugin
    Match               dummy.multi.direct

    # Connection
    Target_Host         <ICL_INSTANCE_ENDPOINT>
    Target_Port         443
    Target_Path         /logs/v1/singles

    # Authentication
    Authentication_Mode IAMAPIKey
    IAM_Environment     Production
```
{: codeblock}

When using an API key, you also need to provide this API key as an environment variable named `IAM_API_KEY`.

## Creating the {{site.data.keyword.logs_routing_full_notm}} tenant
{: #multi-icl-onbord-iclr}

To send to your second {{site.data.keyword.logs_full_notm}} instance,
you need to create an {{site.data.keyword.logs_full_notm}} tenant for {{site.data.keyword.logs_routing_full_notm}} with the other {{site.data.keyword.logs_full_notm}} target instance. For more information, see [creating a tenant](/docs/logs-router?topic=logs-router-onboard-cloud-logs-tenant).

## Configuring the output plug-in for {{site.data.keyword.logs_routing_full_notm}}
{: #multi-icl-output-iclr}

You need to configure an output plug-in to send to the {{site.data.keyword.logs_routing_full_notm}} tenant created in the previous step.

For details about configuring the {{site.data.keyword.logs_routing_full_notm}} agent output plug-in, see [plug-in parameters](/docs/logs-router?topic=logs-router-routing-plugin-parameters).

Similar to the {{site.data.keyword.logs_full_notm}} output plug-in, the {{site.data.keyword.logs_routing_full_notm}} agent output plug-in also specifies a `Match` parameter corresponding to the other input plug-in.

```text
[OUTPUT]
    Name                logger-agent-plugin
    Alias               test-output-multi-target-iclr
    Id                  test-output-multi-target-iclr
    Match               dummy.multi.iclr
    Retry_Limit         8

    # Connection
    Target_Host         ingester.private.<REGION>.logs-router.cloud.ibm.com
    Target_Port         443
    Target_Path         /v1/logs/ws

    # Authentication
    Authentication_Mode TrustedProfile
    IAM_Environment     Production
    Trusted_Profile_ID  <TRUSTED_PROFILE_ID>
    CR_Token_Mount_Path /var/run/secrets/tokens/vault-token
```
{: codeblock}
