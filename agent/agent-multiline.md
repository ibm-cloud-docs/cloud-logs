---

copyright:
  years:  2024
lastupdated: "2024-12-10"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Supporting multiline logs in the {{site.data.keyword.agent}} by converting them to single line logs
{: #agent-multiline}

To support the ingestion of multiline logs, you must make changes to the {{site.data.keyword.agent}} configuration. This change includes the parsing required to group log lines that are supposed to be together as a single log record.
{: shortdesc}

## About
{: #agent-multiline-about}

- You can configure the {{site.data.keyword.agent}} beginning with 1.4.1 to support multiline logs.
- You can configure the {{site.data.keyword.agent}} with the default multiline configuration and the `cri` parser for OpenShift and Kubernetes clusters.
- Alternatively, you can configure the {{site.data.keyword.agent}} with a supported multiline fluent bit parser, or with your own custom multiline parser.

To enable the {{site.data.keyword.agent}} to handle multiline, you can choose one of the following options:
- Deploy the {{site.data.keyword.agent}} by adding a new value `enableMultiline` in the `logs-values.yaml` file that you use to deploy the agent by using a Helm chart. For more information, see [Configuring the Helm chart values file for the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy#agent-helm-os-deploy-step2) or [Configuring the Helm chart values file for the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy#agent-helm-kube-deploy-step2).
- Update the {{site.data.keyword.agent}} to version 1.4.1. You must update the Helm chart `logs-values.yaml` file with the agent version and add the value `enableMultiline` to enable multiline support. For more information, see [Update the Helm chart values file for the Logging agent](/docs/cloud-logs?topic=cloud-logs-agent-helm-update#agent-helm-update-step1).
- Modify the configmap by adding the multiline stanzas.


## Multiline default configuration
{: #agent-multiline-default-configuration}

The default {{site.data.keyword.agent}} configuration includes a multiline parser.

The following is the provided multiline parser:

```text
    [MULTILINE_PARSER]
        Name            multiline_pattern
        Type            regex
        Flush_timeout   1000
        Rule            "start_state"     "/^.*:[\s]*$/"               "colon_cont"
        Rule            "start_state"     "/^.*$/"                     "cont"
        Rule            "cont"            "/^[\s]+.*:[\s]*$/"          "colon_cont"
        Rule            "cont"            "/^[\s]+.*$/"                "cont"
        Rule            "cont"            "/^}$/"                      "cont"
        Rule            "cont"            "/^\s*$/"                    "cont"
        Rule            "colon_cont"      "/^.*:[\s]*$/"               "colon_cont"
        Rule            "colon_cont"      "/^.*$/"                     "cont"
```
{: codeblock}

The default multiline {{site.data.keyword.agent}} configuration will also include a `FILTER` after the `INPUT` plug-in. The filter will apply the pattern of the configured `MULTILINE_PARSER`.

```text
filter-multiline.conf: |
    [FILTER]
        Name              multiline
        Match             *
        Multiline.parser  multiline_pattern
        Multiline.key_content log
```
{: codeblock}
`
For {{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.containerlong_notm}} environments a `cri` parser will be part of the tail input plug-in and included as a Multiline.parser.
{: note}

## Changing the configuration to handle a colon at the end of a line
{: #agent-multiline-modify-configuration}

The default configuration assumes that any line ending with a colon (`:`) is a multiline. If this is not the case in your environment, you will need to change the parser to ignore the final `:` by removing `colon_cont` in the parser. With this change the multiline parser should look like the following:

```text
    [MULTILINE_PARSER]
        Name            multiline_pattern
        Type            regex
        Flush_timeout   1000
        Rule            "start_state"     "/^.*$/"                     "cont"
        Rule            "cont"            "/^[\s]+.*$/"                "cont"
        Rule            "cont"            "/^}$/"                      "cont"
        Rule            "cont"            "/^\s*$/"                    "cont"
```
{: codeblock}

The {{site.data.keyword.agent}} configuration must also include a `FILTER` after the `INPUT` plug-in. The filter will apply the pattern of the configured `MULTILINE_PARSER`. The `Name` value of the `MULTILINE_PARSER` must match the `Multiline.parser` value in the `FILTER`.

## Fluent Bit supported multiline parsers
{: #agent-multiline-fluentbit}

There are supported multiline fluent bit parsers that can be used in place of the {{site.data.keyword.agent}} default parser. Fluent bit supports multiline parsers for `docker`, `cri` `java`, `go`, and `python`.

For more information about the fluent bit parsers, see [Built-in Multiline Parsers](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/multiline-parsing#built-in-multiline-parsers){: external}.

To use one of the built-in fluent bit parsers, change the multiline filter provided with the default configuration to include the desired parser.

```text
filter-multiline.conf: |
    [FILTER]
        Name              multiline
        Match             *
        Multiline.parser  INSERT_PARSER_NAME
        Multiline.key_content log
```
{: codeblock}

The {{site.data.keyword.agent}} configuration must also `@INCLUDE` the filter right after the input plug-in.

## Adding a custom multiline parser
{: #agent-multiline-new-parser}

To create a custom multiline parser for use with the {{site.data.keyword.agent}}, follow the instructions in [Configurable Multiline Parsers](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/multiline-parsing#configurable-multiline-parsers).{: external} You will define a custom regex to determine the multiline pattern.

The {{site.data.keyword.agent}} configuration must also include a `FILTER` after the `INPUT` plug-in. The filter will apply the pattern of the configured `MULTILINE_PARSER`. The `Name` value of the `MULTILINE_PARSER` must match the `Multiline.parser` value in the `FILTER`.

```text
filter-multiline.conf: |
    [FILTER]
        Name              multiline
        Match             *
        Multiline.parser  INSERT_CUSTOM_PARSER_NAME
        Multiline.key_content log
```
{: codeblock}
