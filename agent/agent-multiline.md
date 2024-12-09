---

copyright:
  years:  2024
lastupdated: "2024-12-09"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Supporting multiline logs in the {{site.data.keyword.agent}} by converting them to single line logs
{: #agent-multiline}

To support the ingestion of multiline logs, you must make changes to the {{site.data.keyword.agent}} configuration. This change includes the parsing required to group log lines that are supposed to be together as a single log record.
{: shortdesc}

## Default configuration
{: #multiline-default-configuration}

The default {{site.data.keyword.agent}} configuration includes a multiline parser that is enabled by using the `enableMultiline` value in Helm.

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
{: #multiline-modify-configuration}

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
{: #multiline-fluentbit}

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
{: #multiline-new-parser}

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
