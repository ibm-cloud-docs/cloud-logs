---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Modifying a metadata field by using a JSON Extract rule
{: #parse-extract-value-to-metadata-field}

In {{site.data.keyword.logs_full}}, you can use the *JSON Extract* rule to extract the value of a JSON field into a metadata field.
{: shortdesc}


## Before you begin
{: #parse-extract-value-to-metadata-field-1}

Parsing rules are organized inside *Rule Groups*. Each group has a name and a set of rules with a logical relationship between them. Logs are processed according to the order of rule group (from the beginning to the end). They are then processed by the order of rules within the rule group and according to the logical operators between them (`AND/OR`). Rules help you to process, parse, and restructure log data to prepare for monitoring and analysis. For more information, see [Working with rule groups](/docs/cloud-logs?topic=cloud-logs-rules_groups).


## Configuring a JSON Extract rule
{: #parse-extract-value-to-metadata-field-3-ui}
{: ui}

Complete the following steps:

1. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Parsing rules** and click **New Rule Group**.

2. In the **Details** section, enter the *Rule Group Name* and the *Rule Group Description*.

3. In the **Rule Matcher** section, configure the applications, subsystems, and severities that define the logs on which to apply the rules that are included in the rules group.

4. In the **Rules** section, select **JSON Extract** ![JSON Extract parsing rule icon](/icons/Json_Extract.svg "JSON Extract").

    1. Enter a name.

    2. Optionally, enter a description.

    3. Select a *JSON key*.

    4. Select a *Destination Field*, that is, select the field that will be populated with the JSON key value. Valid metadata fields are: `Category`, `Class`, `Method`, `Severity`, and `Thread ID`.

    5. Toggle the status to **ACTIVE** if you want the rule to be enabled.

5. Add additional rule groups by clicking **Add Rule** and selecting the desired rule type. Toggle **AND**/**OR** to select how you would like the additional rules processed.

6. Click **Create Rule Group**.


## Configuring a JSON Extract rule using the API
{: #parse-extract-value-to-metadata-field-3-api}
{: api}

Complete the following steps:



## Example: Extracting a key value and populating a metadata field
{: #parse-extract-value-to-metadata-field-4}

JSON Extract rules take the value of a key and use it to overwrite one of the metadata fields. This example extracts the value from a field that is called `worker` and use it to populate the metadata field that is named `Category`.

In the {{site.data.keyword.logs_full}} UI, specify `worker` for the **JSON Key** and `Category` for the **Destination Field**.

The source field is always text. The JSON key field should contain the field name from where you want to extract the value.

The destination field is the metadata field that is overwritten with this value. This rule is frequently used to extract and set severity and to set metadata fields such as `Category` that influence the classification algorithms. 

The original log is:

```json
{
    "transaction_ID": 12543,
    "worker": "A23",
    "Message": "success"
}
```
{: codeblock}

The log is not changed in the **Explore** > **Logs** interface but the metadata field `Category` is populated with “A23”.
