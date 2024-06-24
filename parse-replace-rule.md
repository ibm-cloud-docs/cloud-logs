---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Fixing log data by using a Replace rule
{: #parse-replace-rule}

In {{site.data.keyword.logs_full}}, you can use the *Replace* rule to change the log structure, repair incorrectly formatted logs, change the log severity, or mask information.
{: shortdesc}



## Before you begin
{: #parse-replace-1}

Parsing rules are organized inside *Rule Groups*. Each group has a name and a set of rules with a logical relationship between them. Logs are processed according to the order of rule group (from the beginning to the end). They are then processed by the order of rules within the rule group and according to the logical operators between them (`AND/OR`). Rules help you to process, parse, and restructure log data to prepare for monitoring and analysis. For more information, see [Working with rule groups](/docs/cloud-logs?topic=cloud-logs-rules_groups).



## Configuring a Replace rule
{: #parse-replace-3-ui}
{: ui}

Complete the following steps:

1. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Parsing rules** and click **New Rule Group**.

2. In the **Details** section, enter the *Rule Group Name* and the *Rule Group Description*.

3. In the **Rule Matcher** section, configure the applications, subsystems, and severities that define the logs on which to apply the rules that are included in the rules group.

4. In the **Rules** section, select **Replace** ![Replace parsing rule icon](/icons/Replace.svg "Replace").

    1. Enter a name.

    2. Optionally, enter a description.

    3. Select a *Source Field*. This is the field on which the RegEx is applied.

    4. Select a *Destination Field*. This is the field that will be populated with the results of applying the RegEx expression.

    5. Enter the *Regular Expression* (RegEx).

    6. Enter a replacement string that will replaced the matched RegEx.

    7. Toggle the status to **ACTIVE** if you want the rule to be enabled.

5. Add additional rule groups by clicking **Add Rule** and selecting the desired rule type. Toggle **AND**/**OR** to select how you would like the additional rules processed.

6. Click **Create Rule Group**.


## Configuring a Replace rule using the API
{: #parse-replace-3-api}
{: api}

Complete the following steps:




## Example: Repairing an incorrectly formatted JSON log
{: #parse-replace-4}

A common use case for a replace rule is to repair incorrectly formatted JSON logs.

In the following example, the JSON logs are sent with a date prefix that breaks the JSON format and turns them into unstructured logs.

The RegEx identifies the substring and removes the incorrect string in the log.

The original log is:

```text
2020-08-07 {“status”:”OK”, “user”:John Smith”, “ops”:”J1”}
```
{: codeblock}

The RegEx:

```text
.*{
```
{: codeblock}

The string to replace the result of evaluating the RegEx expression is:

```text
{
```
{: codeblock}


The resulting log:

```json
{"status":"OK", "user":"John Smith", "ops":"J1"}
```
{: codeblock}


## Example: Rebuilding a log with nested fields
{: #parse-replace-5}


The following example shows how to use a replace rule to rebuild a log with nested fields. Nested fields are a constraint in the extract and parse rules. 

The original log:

```json
{"ops":"G1","user":"John Smith-2125 Sierra Ventura Dr.-Sunnyvale-CA-94054","status":"305"}
```
{: codeblock}

The RegEx:

```text
(.*user"):"([^-]*)-([^-]*)-([^-]*)-([^-]*)-([^-]*)",([^$]*)
```
{: codeblock}

Each of the parentheses represents a capture group that can be addressed by `$n n=1..7`.

The replacement string:

```text
$1:{"name":"$2","address":"$3","city":"$4","state":"$5","zip":"$6"},$7
```
{: codeblock}

The resulting log;

```json
{
   "ops":"G1",
   "User":{
      "name":"John Smith",
      "address":"2125 Sierra Ventura Dr.",
      "city":"Sunnyvale",
      "state":"CA",
      "Zip":"94054"
   },
   "status":"305"
}
```
{: codeblock}


## Example: Transforming stringified (escaped) JSON field into an object
{: #parse-replace-6}

The inner_json rule is a special replace rule that takes a field value in a JSON log that includes stringified (escaped) JSON, and transform it into an object.

In the following example, the original log is:

```json
{
 "server":"opa",
 "IBC":"45ML",
 "thread":"1201",
 "message":"{\"first_name\":\"John\", \"last_name\":\"Smith\", \"userID\":\"AB12345\", \"duration\":45}"
}
```
{: codeblock}

The field message has a string value that is an escaped legal JSON.

Our special replace rule changes the name of the field from the original name "message" to "inner_json":

The RegEx:

```text
“message”\s*:\s*”{\s*\\”
```
{: codeblock}

This RegEx identifies a field name message with the beginning of the escaped JSON.

The replacement string is:

```text
“inner_json”:”{\”
```
{: codeblock}

This example replaces only the field name and nothing else.

The resulting log:

```json
{
   "server":"opa",
   "inner_json":{
     "first_name":"John" ,
     "last_name":"Smith" ,
     "userID":"AB12345" ,
     "duration":45
  }
}
```
{: codeblock}
