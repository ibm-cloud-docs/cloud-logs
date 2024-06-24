---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}




# Blocking log data
{: #parse-block-rule}


In {{site.data.keyword.logs_full}}, you can use the *Block* rule to filter out incoming logs by using a RegEx expression.
{: shortdesc}


Block rules also have the following options:

- **Block all matching logs**: Blocks any log that matches the rule matcher and block rule.

- **Block all non-matching logs**: Blocks any log that does not match the rule matcher and block rule.

Selecting **View blocked logs in LiveTail and archive to IBM Cloud Object Storage** archives logs in the *{{site.data.keyword.compliance}}* policy plan. This is a more refined option to give logs a low priority. Only 15% of low priority logs volume is counted against the quota.
{: note}

## Before you begin
{: #parse-block-1}

Parsing rules are organized inside *Rule Groups*. Each group has a name and a set of rules with a logical relationship between them. Logs are processed according to the order of rule group (from the beginning to the end). They are then processed by the order of rules within the rule group and according to the logical operators between them (`AND/OR`). Rules help you to process, parse, and restructure log data to prepare for monitoring and analysis. For more information, see [Working with rule groups](/docs/cloud-logs?topic=cloud-logs-rules_groups).



## Configuring a Block rule
{: #parse-block-3-ui}
{: ui}

Complete the following steps:

1. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Parsing rules** and click **New Rule Group**.

2. In the **Details** section, enter the *Rule Group Name* and the *Rule Group Description*.

3. In the **Rule Matcher** section, configure the applications, subsystems, and severities that define the logs on which to apply the rules that are included in the rules group.

4. In the **Rules** section, select **Block** ![Block parsing rule icon](/icons/Block.svg "Block").

    1. Enter a name.

    2. Optionally, enter a description.

    3. Select a *Source Field*. This is the field on which the RegEx is applied.

    4. Enter the *Regular Expression* (RegEx) expression.

    5. Click **View blocked logs in LiveTail and archive to IBM Cloud Object Storage** to view and query these logs.

    6. Select the Block rule logic. You can choose to `Block all matching logs` or to `Block all non-matching logs`.

    7. Toggle the status to **ACTIVE** if you want the rule to be enabled.

5. Add additional rule groups by clicking **Add Rule** and selecting the desired rule type. Toggle **AND**/**OR** to select how you would like the additional rules processed.

6. Click **Create Rule Group**.


## Configuring a Block rule using the API
{: #parse-block-3-api}
{: api}

Complete the following steps:




## Example: Block logs with a specific error code
{: #parse-block-4}


Using a block, you can filter out your incoming logs. As with other rules, the main part of the rule is a RegEx identifying the logs to be allowed or blocked. In this example, all the logs that have the substring `sql_error_code 28000` are blocked.

The RegEx:

```text
sql_error_code=28000
```
{: codeblock}


The block logic indicates if the rule blocks all logs that match the RegEx or do not match the RegEx. In the previous example, checking **block all non-matching logs** would block all logs except logs that include the string `sql_error_code\s*=\s*28000` 
