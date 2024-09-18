---

copyright:
  years:  2024
lastupdated: "2024-09-12"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Streaming platform logs from selected services
{: #streaming_platform_data_select}

Stream platform logs that are generated by selected {{site.data.keyword.cloud}} services from an {{site.data.keyword.logs_full_notm}} instance to other corporate tools such as Security Information and Event Management (SIEM) tools by integrating {{site.data.keyword.logs_full}} and {{site.data.keyword.messagehub}}.
{: shortdesc}


## Prereqs
{: #streaming_platform_data_select_prereqs}

- An {{site.data.keyword.messagehub_full}} instance is provisioned in the same account as the {{site.data.keyword.logs_full_notm}} instance from where you plan to stream data.

    Check the limitations of the service plans. For more information, see [Limits and quotas](/docs/EventStreams?topic=EventStreams-kafka_quotas).{: important}

- You have permissions to create a topic in the {{site.data.keyword.messagehub_full}} instance.

    To create a topic in {{site.data.keyword.messagehub}}, you must have the **manager** role for the {{site.data.keyword.messagehub}} instance. This role includes the **messagehub.topic.manage** IAM action role that allows an app or user to create or delete topics.

- You route the platform logs that you want to stream to the {{site.data.keyword.logs_full}} instance.

- You have permissions to configure streaming in your {{site.data.keyword.logs_full}} instance.

    You must have the **manager** service role.

- You might need a parsing rule that extracts specific values such as the service name from the `logSourceCRN` if you want to filter by service name. {: important}

## Define a streaming rule
{: #streaming_platform_data_select_1}
{: step}

You can define rules that filter the platform logs that you stream to {{site.data.keyword.messagehub_full}}.


The following table shows some rules that you can configure:

| Rule description | Rule |
|------------------|------|
| Stream all platform logs | `<v1> $l.applicationname =='ibm-platform-logs'` |
| Stream platform logs from 1 service | `<v1> $l.applicationname =='ibm-platform-logs' && $d.serviceName =='REPLACE_WITH_CRN_SERVICE_NAME'` |
| Stream platform logs from 2 services | `<v1> $l.applicationname =='ibm-platform-logs' && ( $d.serviceName =='REPLACE_WITH_CRN_SERVICE_NAME_1' \|\| $d.serviceName =='REPLACE_WITH_CRN_SERVICE_NAME_2'` ) |
| Stream platform logs that have a critical severity | `<v1> $l.applicationname =='ibm-platform-logs' && $d.severity =='REPLACE_WITH_SEVERITY_VALUE'`  \n  \n Valid severity values are: `normal`, `warning`, and `critical`. |
| Stream platform logs with different severity values from selected services | `<v1> ( ( $l.applicationname =='ibm-platform-logs' && ( $d.serviceName =='REPLACE_WITH_CRN_SERVICE_NAME_1' \|\|  $d.serviceName =='REPLACE_WITH_CRN_SERVICE_NAME_2' ) && $d.severity =='REPLACE_WITH_SEVERITY_VALUE') ) \|\| ( $l.applicationname =='ibm-platform-logs' && $d.serviceName =='iam-identity' && $d.severity =='REPLACE_WITH_SEVERITY_VALUE')`  \n  \n Valid severity values are: `normal`, `warning`, and `critical`.|
| Stream platform logs based on data in the `requestData` or `responseData` sections | `$d.requestData.REPLACE_WITH_FIELD_NAME`  \n  \n For example, for a field `requestId`, you can configure `<v1> $d.requestData.requestId` |
{: caption="Example rules" caption-side="bottom"}


For more information, see [Configuring streaming data rules](/docs/cloud-logs?topic=cloud-logs-streaming_rules).


Note that some examples include the `<v1>` prefix. This prefix is automatically included when using the UI and does not need to be specified. However, a DPXL expression used in an API must start with the `<v1>` prefix.
{: tip}

For example, to filter platform logs with different severity values from selected services, you can define a query as follows:

```text
<v1> ( ( $l.applicationname =='ibm-platform-logs' && ( $d.serviceName =='iam-am' ||  $d.serviceName =='cloud-object-storage' ) && $d.severity =='critical') )
|| ( $l.applicationname =='ibm-platform-logs' && $d.serviceName =='iam-identity' && $d.severity =='normal')
```
{: codeblock}

## Validate a streaming rule
{: #streaming_platform_data_select_1b}
{: step}

To verify the streaming rule, in the left-hand navigation, click **Explore logs > Logs**. Select **DataPrime** query, and change the query as follows:


```text
filter 'PASTE_YOUR_CONDITION'
```
{: codeblock}

The output of the query should give you the list of log records that would be streamed once you enable the streaming configuration.

For example, change `<v1> $l.applicationname =='ibm-platform-logs'` to:

```text
filter $l.applicationname =='ibm-platform-logs'
```
{: codeblock}

## Configure streaming for platform logs
{: #streaming_platform_data_select_2}
{: step}

To configure streaming, see [Integrating {{site.data.keyword.logs_full_notm}} with {{site.data.keyword.messagehub}}](/docs/cloud-logs?topic=cloud-logs-streaming-config).