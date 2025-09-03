---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Configuring the agent to set custom values for applicationName and subsystemName metadata fields
{: #agent-set-appsubname}

You can configure the {{site.data.keyword.agent}} to send logs to the {{site.data.keyword.logs_full_notm}} service.
{: shortdesc}

Logs that you send must include a value for the `applicationName` and `subsystemName` metadata fields.

By default, when you configure the {{site.data.keyword.agent}}, the agent sets default values for these fields. You can configure your own custom values to replace the default values. For more information on default values, see [Metadata fields](/docs/cloud-logs?topic=cloud-logs-metadata).


In {{site.data.keyword.logs_full_notm}}, you can use the `applicationName` and `subsystemName` metadata fields to configure any of the following features:
- TCO policies
- Parsing rules
- Data usage reports
- Alerts
- Views
- Dashboards
- Events to metrics
- Loggregation

For information about {{site.data.keyword.logs_full_notm}}, see the [{{site.data.keyword.logs_full_notm}} documentation](/docs/cloud-logs?topic=cloud-logs-getting-started).

## Configuring the agent to set custom values
{: #agent-set-appsubname-1}

You can configure the {{site.data.keyword.agent}} with custom values for the `applicationName` and `subsystemName` metadata fields by specifying API options.

- Use `-a` to specify the `applicationName` that you want to use.

    By default, the `applicationName` defaults to the namespace name `kubernetes.namespace_name` in the {{site.data.keyword.openshiftlong_notm}} or {{site.data.keyword.containerlong_notm}} cluster.

    You can also use variables from the environment to set custom values, for example `'${POD_NAMESPACE}'`.

- Use `-s` to specify the `susbsystemName` that you want to use.

    By default, the `subsystemName` defaults to the container name `kubernetes.container_name` in {{site.data.keyword.openshiftlong_notm}} or {{site.data.keyword.containerlong_notm}} clusters.

    You can also use variables from the environment, for example `'${POD_NAME}'`.

When setting these metadata fields you have the following options:
- You can set the value to a fixed string. For example, you can use `-s 'production'`.
- You can use variables from the environment, for example `-a '${POD_NAMESPACE}'`.
- You can combine a fixed string with variables from the environment, for example `-a 'mycluster:${POD_NAME}'`.

You can set `applicatioName`, `subsystemName`, or both. If a value is not set, the default value is applied. For information about the default values that are set for the `applicationName` and `subsystemName` metadata fields, see [Metadata](/docs/cloud-logs?topic=cloud-logs-metadata){: external}.
{: note}

### Example: Configuring dynamic values
{: #agent-set-appsubname-3}

To configure the {{site.data.keyword.agent}} with custom dynamic values for the `applicationName` and `subsystemName` metadata fields, you can deploy the agent as follows in a Kubernetes cluster:

```sh
curl -sSL https://ibm.biz/logs-router-setup | bash -s --   -v 1.1.1   -m IAMAPIKey    -k xxxx   -t Kubernetes   -r eu-es   -p 3443 -s '${POD_NAME}' -a '${POD_NAMESPACE}'
```
{: codeblock}

### Example: Configuring a value that combines a fixed value and a dynamic value
{: #agent-set-appsubname-4}

To configure the {{site.data.keyword.agent}} with custom values for the `applicationName` and `subsystemName` metadata fields, you can deploy the agent as follows in a Kubernetes cluster:

```sh
curl -sSL https://ibm.biz/logs-router-setup | bash -s --   -v 1.1.1   -m IAMAPIKey    -k xxxx   -t Kubernetes   -r eu-es   -p 3443 -s '${POD_NAME}' -a 'mycluster-dallas:${POD_NAMESPACE}'
```
{: codeblock}

In this example, the name of the cluster is added as a string.

### Example: Configuring fixed values
{: #agent-set-appsubname-2}

To configure the {{site.data.keyword.agent}} with custom fixed values for the `applicationName` and `subsystemName` metadata fields, you can deploy the agent as follows in a Kubernetes cluster:

```sh
curl -sSL https://ibm.biz/logs-router-setup | bash -s --   -v 1.1.1   -m IAMAPIKey    -k xxxx   -t Kubernetes   -r eu-es   -p 3443 -s 'mysubsystem' -a 'myapp'
```
{: codeblock}


## Configuring the agent to set custom values based on the log line
{: #agent-set-appsubname-5}


You can dynamically add values for application and subsystem name depending on the log line.

The following example shows how to configure an agent for a Kubernetes cluster that adds a custom application name for a JSON formatted message:

1. Add the applicationName to the log line.

    For example, your log line looks as follows: `{"level":"info", "msg":"Test message", "applicationName":"my-application"}`

2. Add the JSON PARSER plugin to the `logger-agent-iks.yaml` file to convert a stingify JSON into a JSON object.  For more information, see [JSON](https://docs.fluentbit.io/manual/data-pipeline/parsers/json){: external}.

    ```yaml
    [PARSER]
        # Converts the original log source from a JSON map string to the internal binary representation.
        Name   json
        Format json
        # Time_Key: Set the time in your log entry to the log record time included with the log. If not set, Fluenti Bit uses its own time.
        Time_Key time
        Time_Format %d/%b/%Y:%H:%M:%S %z
        # Time_Keep: To keep all fields in the original log record
        Time_Keep On
    ```
    {: codeblock}

3. Add the PARSER plugin to the `logger-agent-iks.yaml` file to extract fields from logs. For more information, see [Parser](https://docs.fluentbit.io/manual/data-pipeline/filters/parser){: external}.

    By default, the parser plugin only keeps the parsed fields in its output.
    {: note}

    ```yaml
    [FILTER]
       # Name: Specify the name of the parser
       Name parser
       # Match: A pattern that is used to match against the tags that are defined on incoming records.
       Match *
       # Key_Name: Specify the field name in the log to be parsed.
       Key_Name message
       # Parser: Specify the parser name to interpret the field.
       Parser json
       # Reserve_Data: Set to keep all the fields
       Reserve_Data On
       # preserve_key: Set to keep the original key field.
       Preserve_Key On
    ```
    {: codeblock}

4. Extract the application name by using the Nest filter plugin

    The Nest Filter plugin allows you to operate on or with nested data. Its modes of operation are: `nest` where it takes a set of records and puts them in a map, and `lift` where it takes a map by key and lifts its records up. For more information, see [Nest](https://docs.fluentbit.io/manual/data-pipeline/filters/nest#configuration-file){: external}.

    applicationName must be at the top level, therefore, you must use the `lift` operation.

    [FILTER]
       Name nest
       Match *
       Operation lift
       Nested_under message
       Wildcard applicationName

With this in place, the "applicationName" for the log line example above would be "my-application" for that particular line.
