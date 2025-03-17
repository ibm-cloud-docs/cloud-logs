---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_full_notm}} log parsing rules
{: #log_parsing_rules}

You can use parsing rules to process, parse, and restructure log data to prepare for monitoring and analysis. For example, you can extract selected information, structure unstructured logs, or discard unnecessary parts of the logs. You can mask fields for compliance reasons and fix misformatted logs. You can block log data from being ingested based on log content and much more.   
{: shortdesc}

In {{site.data.keyword.logs_full}}, you can use parsing rules to control the structure of your data before the data is indexed in OpenSearch.
{: note}



## Rules groups
{: #log_parsing_rules-1}

Parsing rules are organized inside *Rule Groups*. Each group has a name and a set of rules with a logical relationship between them. Logs are processed according to the order of rule group (from the beginning to the end). They are then processed by the order of rules within the rule group and according to the logical operators between them (`AND/OR`). Rules help you to process, parse, and restructure log data to prepare for monitoring and analysis. For more information, see [Working with rule groups](/docs/cloud-logs?topic=cloud-logs-rules_groups).

## Types of rules
{: #log_parsing_rules-2}

You can configure the following parsing rules:

- Parse ![Parse parsing rule icon](/icons/PARSE.svg "Parse"): Convert unstructured text into JSON format.

- Extract ![Extract parsing rule icon](/icons/Extract.svg "Extract"): Extract values as JSON keys without parsing the entire log.

- Extract JSON ![JSON Extract parsing rule icon](/icons/Json_Extract.svg "JSON Extract"): Extract the value of a JSON key into a metadata field.

- Replace ![Replace parsing rule icon](/icons/Replace.svg "Replace"): Replace the value of a field with a fixed string value to fix the log structure, change the log severity, or obfuscate information.

- Block ![Block parsing rule icon](/icons/Block.svg "Block"): Drop incoming logs by using a regex expression.

- Timestamp Extract ![Timestamp parsing rule icon](/icons/Timestamp.svg "Timestamp"): Replace the log timestamp with a timestamp that is included in the log.

- Remove Fields ![Remove parsing rule icon](/icons/Remove.svg "Remove"): Remove JSON fields in a log to reduce the number of indexed fields.

- Stringify JSON Field ![JSON Stringify parsing rule icon](/icons/STRINGIFY.svg "JSON Stringify"): Transform a JSON field into a stringify JSON field to reduce the number of indexed fields.

- Parse JSON Field ![Parse parsing rule icon](/icons/PARSE.svg "Parse"): Transform escaped or stringified fields into JSON format.



## Rules that change the original log
{: #log_parsing_rules-3}

These rules modify the original log lines.

- Parse
- Timestamp Extract
- Replace
- Parse JSON field


## Rules that add more fields to the original log
{: #log_parsing_rules-4}

These rules add fields to the log line while the original log data is maintained.

- Extract JSON
- Extract

## Rules that drop data
{: #log_parsing_rules-5}

These rules remove data from a log line.

- Block
- Remove
- Stringify JSON field (can keep original log or not)


## Order of execution of rules
{: #log_parsing_rules-6}

As logs are ingested, rules groups are applied in order, starting from the first configured rule.

Specify block rules first and use the rule matcher when possible to prevent unnecessary processing of logs and speed-up your data processing.
{: tip}

Within a rules group:
1. The rules group matcher query is applied first.

    Only logs that match the applications, subsystems, and severities that are configured continue applying the parsing rules.

2. Rules are applied in order from the first rule until a rule is followed by an `OR` logical operator.

    Rules are applied immediately so that the output of one rule becomes the input of the next one.
    {: note}

    The `OR` and `AND` operators in the group do not follow the mathematical order of operations.


The order of execution of rules groups and rules is important, and define the final log’s structure.
