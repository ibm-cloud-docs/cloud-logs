---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Extracting specific values as JSON keys
{: #parse-extract-rule}


In {{site.data.keyword.logs_full}}, you can use the *Extract* rule to extract specific values you need as JSON keys without having to parse the entire log.
{: shortdesc}

Unlike a parse rule, an extract rule leaves the original log intact and adds fields to it at the root.
{: note}

## Before you begin
{: #parse-extract-1}

Parsing rules are organized inside *Rule Groups*. Each group has a name and a set of rules with a logical relationship between them. Logs are processed according to the order of rule group (from the beginning to the end). They are then processed by the order of rules within the rule group and according to the logical operators between them (`AND/OR`). Rules help you to process, parse, and restructure log data to prepare for monitoring and analysis. For more information, see [Working with rule groups](/docs/cloud-logs?topic=cloud-logs-rules_groups).


## Using named captured groups to define new fields
{: #parse-extract-2}

The extract rule uses RegEx-named capture groups to define new fields.

- Captured groups become the parsed log fields.
- The value that is associated with each group becomes the field’s value.
- The RegEx doesn’t have to match the entire log.
- Only the RegEx named capture groups (the values within the `< >`) and the value they capture are part of the reconstructed log.



## Configuring an Extract rule
{: #parse-extract-3-ui}
{: ui}

Complete the following steps:

1. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Parsing rules** and click **New Rule Group**.

2. In the **Details** section, enter the *Rule Group Name* and the *Rule Group Description*.

3. In the **Rule Matcher** section, configure the applications, subsystems, and severities that define the logs on which to apply the rules that are included in the rules group.

4. In the **Rules** section, select **Extract** ![Extract parsing rule icon](/icons/Extract.svg "Extract").

    1. Enter a name.

    2. Optionally, enter a description.

    3. Select a *Source Field*. This is the field on which the RegEx is applied.

    4. Enter the *Regular Expression* (RegEx).

    5. Toggle the status to **ACTIVE** if you want the rule to be enabled.

5. Add additional rule groups by clicking **Add Rule** and selecting the desired rule type. Toggle **AND**/**OR** to select how you would like the additional rules processed.

6. Click **Create Rule Group**.


## Example: Creating two new fields
{: #parse-extract-rule-4}

The following example extracts information from the field message and creates two new fields, ‘bytes’, and ‘status’ that can be queried and visualized.

The original log is :

```text
{"level":"INFO", "message": "200 bytes sent status is OK"}
```
{: codeblock}

The RegEx is:

```text
message"\s*:\s*"(?P<bytes>\d+)\s*.*?status\sis\s(?P<status>[^"]+)
```
{: codeblock}

The formatted log is:

```json
{
    "level": "INFO",
    "message": "200 bytes sent status is OK",
    "Bytes": "200",
    "status": "OK"
}
```
{: codeblock}

If the original log is unstructured, fields are added based on the named capture groups and the original log is stored inside a field called `text`. Using the previous example, it changes the original log to be unstructured.

The original log:

```text
"level":"INFO", "message": "200 bytes sent status is OK",
```
{: codeblock}

The resulting log:

```json
{
    "bytes": "200",
    "text": "\"level\":\"INFO\", \"message\": \"200 bytes sent status is OK\"",
    "status": "OK"
}
```
{: codeblock}
