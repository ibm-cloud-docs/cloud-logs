---

copyright:
  years:  2024
lastupdated: "2024-08-27"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Configuring streaming data rules
{: #streaming_rules}

You can define rules by using the DataPrime eXpression Language (DPXL) to filter what data is streamed to {{site.data.keyword.messagehub_full}} from an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

For more information about the DataPrime eXpression Language, see the [DataPrime Expression Language (DPXL) reference](/docs/cloud-logs?topic=cloud-logs-dpxl_ref).

You can only define rules that define conditions based on the value of 1 or more fields.
{: important}

You might need a parsing rule that extracts specific values such as the service name from the `logSourceCRN` if you want to filter by service name. 
{: important}

The following sections show samples of different types of rules that you can configure.

Note that some examples include the `<v1>` prefix. This prefix is automatically included when using the UI and does not need to be specified. However, a DPXL expression used in an API must start with the `<v1>` prefix.
{: tip}

## Streaming all data
{: #streaming_rules_1}

Do not define a DataPrime rule when you configure streaming.

## Streaming data that contains free text
{: #streaming_rules_1b}

To stream data that includes free text, you must set up the rule as follows:

```text
$d.msg.contains('ENTER_FREE_TEXT')
```
{: codeblock}

For example, to search for `Error 1234`, you can include the following in your rule:


```text
$d.msg.contains('Error1234')
```
{: codeblock}


## Stream data for 1 or more applications
{: #streaming_rules_2}

In an {{site.data.keyword.logs_full_notm}} instance, you can collect data from multiple applications.

When you configure streaming, you can define custom rules to stream selected data.


### Streaming auditing events
{: #streaming_rules_3}

To stream all auditing events, define the following DataPrime rule:

```text
<v1> $l.applicationname =='ibm-audit-event'
```
{: codeblock}

### Streaming platform logs
{: #streaming_rules_4}

To stream all platform logs, define the following DataPrime rule:

```text
<v1> $l.applicationname =='ibm-platform-logs'
```
{: codeblock}


### Streaming logs by applicationName
{: #streaming_rules_5}

To stream logs by applicationName for selected applications, define a DataPrime rule. For example, to stream data from 3 applications, you can use:

```text
<v1> $l.applicationname =='app1' || $l.applicationname =='app2' || $l.applicationname =='app3'
```
{: codeblock}

Use `||` to indicate `OR`.



## Stream data for 1 or more subsystems
{: #streaming_rules_6}

To stream logs by subsystemName, define a DataPrime rule. For example, to stream data from 3 subsystems, you can use:

```text
<v1> $l.subsystemname =='subsystem1' || $l.subsystemname =='subsystem2' || $l.subsystemname =='subsystem3'
```
{: codeblock}

Use `||` to indicate `OR`.



## Stream data based on multiple values for a field that is included in the log record
{: #streaming_rules_7}

If you are interested in streaming some data based on the value of a field in your log record, you can define a rule as follows:

This sample shows how to define a rule for 3 different values of a field in the log record:

```text
<v1> $d.<FIELD_NAME> =='value1' || $d.<FIELD_NAME> =='value2' || $d.<FIELD_NAME> =='value3'
```
{: codeblock}

## Stream data based on the values of 1 or more fields that are included in the log record
{: #streaming_rules_8}

If you are interested in streaming some data based on the value of 1 or more fields in your log record, you can define a rule as follows:


```text
<v1> $d.<FIELD_NAME_1> =='value1' && $d.<FIELD_NAME_2> =='value2'
```
{: codeblock}

## Stream data based on 2 conditions
{: #streaming_rules_9}

To stream data based on 2 conditions where the value of 1 field is the same but the value of the other field can have different values, for example, you can define the rule as follows:

```text
<v1> ( $d.<FIELD_NAME_1> =='value1' && $d.<FIELD_NAME_2> =='value2' ) || ( $d.<FIELD_NAME_1> =='value1' && $d.<FIELD_NAME_2> =='value3' )
```
{: codeblock}


For example, to filter auditing events with different severity values from selected services, you can define a query as follows:

```text
<v1> ( ( $l.applicationname =='ibm-audit-event' && ( $d.serviceName =='iam-am' ||  $d.serviceName =='cloud-object-storage' ) && $d.severity =='critical') )
|| ( $l.applicationname =='ibm-audit-event' && $d.serviceName =='iam-identity' && $d.severity =='normal')
```
{: codeblock}

## Validate a rule
{: #streaming_rules_validate}

To verify the streaming rule, in the left-hand navigation, click **Explore logs > Logs**. Select **DataPrime** query, and change the query as follows:


```text
filter 'PASTE_YOUR_CONDITION'
```
{: codeblock}

The output of the query should give you the list of log records that would be streamed once you enable the streaming configuration.

For example, change `<v1> $l.applicationname =='ibm-audit-event'` to:

```text
filter $l.applicationname =='ibm-audit-event'
```
{: codeblock}
