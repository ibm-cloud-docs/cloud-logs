---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Convert unstructured text into JSON
{: #parse-rule}

In {{site.data.keyword.logs_full}}, you can use the *Parse* rule to convert unstructured text into 1 or more JSON fields.
{: shortdesc}


## Before you begin
{: #parse-rule-1}

Parsing rules are organized inside *Rule Groups*. Each group has a name and a set of rules with a logical relationship between them. Logs are processed according to the order of rule group (from the beginning to the end). They are then processed by the order of rules within the rule group and according to the logical operators between them (`AND/OR`). Rules help you to process, parse, and restructure log data to prepare for monitoring and analysis. For more information, see [Working with rule groups](/docs/cloud-logs?topic=cloud-logs-rules_groups).


## Using named captured groups to define new fields
{: #parse-rule-2}

The parse rule uses RegEx named capture groups to define new fields.

- Captured groups become the parsed log fields.
- The value that is associated with each group becomes the field’s value.
- The RegEx doesn’t have to match the entire log.
- Only the RegEx named capture groups (the values within the `< >`) and the value they capture are part of the reconstructed log.


## Configuring a Parse rule
{: #parse-rule-3-ui}
{: ui}

Complete the following steps to create a rules group with 1 Parse rule:

1. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Parsing rules** and click **New Rule Group**.

2. In the **Details** section, enter the *Rule Group Name* and the *Rule Group Description*.

3. In the **Rule Matcher** section, configure the applications, subsystems, and severities that define the logs on which to apply the rules that are included in the rules group.

4. In the **Rules** section, select **Parse** ![Parse parsing rule icon](/icons/PARSE.svg "Parse").

    1. Enter a name.

    2. Optionally, enter a description.

    3. Select a *Source Field*. This is the field on which the RegEx is applied.

    4. Select a *Destination Field*. This is the field that will be populated with the results of applying the RegEx expression.

    5. Enter the *Regular Expression* (RegEx).

    6. Toggle the status to **ACTIVE** if you want the rule to be enabled.

5. Add additional rule groups by clicking **Add Rule** and selecting the desired rule type. Toggle **AND**/**OR** to select how you would like the additional rules processed.

6. Click **Create Rule Group**.


## Configuring a Parse rule using the API
{: #parse-rule-3-api}
{: api}

Complete the following steps to create a rules group with 1 Parse rule:



## Example log conversions
{: #parse-rule-4}

The following example takes a Heroku L/H type error log that is sent from Heroku as an unstructured log and converts it to JSON log.

The original log is:

```text
sock=client at=warning code=H27 desc="Client Request Interrupted" method=POST path="/submit/" host=myapp.herokuapp.com fwd=17.17.17.17 dyno=web.1 connect=1ms service=0ms status=499 bytes=0
```
{: codeblock}

The RegEx is:

```text
^(sock=)?(?P<sock>(\S*))\s*at=(?P<severity>\S*)\s*code=(?P<error_code>\S*)\s*desc="(?P<desc>[^"]*)"\s*method=(?P<method>\S*)\s*path="(?P<path>[^"]*)" host=(?P<host>\S*)\s* (request_id=)?(?P<request_id>\S*)\s*fwd="?(?P<fwd>[^"\s]*)"?\s*dyno=(?P<dyno>\S*)\s*connect=(?P<connect>\d*)(ms)?\s*service=(?P<service>\d*)(ms)?\s*status=(?P<status>\d*)\s* bytes=(?P<bytes>\S*)\s*(protocol=)?(?P<protocol>[^"\s]*)$
```
{: codeblock}

The formatted log is:

```json
{
    "sock": "client",
    "severity": "warning",
    "error_code": "H27",
    "desc": "Client Request Interrupted",
    "method": "POST",
    "path": "/submit/",
    "host": "myapp.herokuapp.com",
    "request_id": "",
    "fwd": "17.17.17.17",
    "dyno": "web.1",
    "connect": "1",
    "service": "0",
    "status": "499",
    "bytes": "0",
    "protocol": ""
}
```
{: codeblock}
