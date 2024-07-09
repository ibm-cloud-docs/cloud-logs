---

copyright:
  years:  2024
lastupdated: "2024-07-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Limiting parsing to logs based on application, subsystem, or severity
{: #parse-severity}

In {{site.data.keyword.logs_full}}, you can use the *Severity Rules* to limit the logs that will be affected by other parsing rules based on the on the application, subsystem, or severity of the log.
{: shortdesc}


## Before you begin
{: #parse-severity-1}

Parsing rules are organized inside *Rule Groups*. Each group has a name and a set of rules with a logical relationship between them. Logs are processed according to the order of rule group (from the beginning to the end). They are then processed by the order of rules within the rule group and according to the logical operators between them (`AND/OR`). Rules help you to process, parse, and restructure log data to prepare for monitoring and analysis. For more information, see [Working with rule groups](/docs/cloud-logs?topic=cloud-logs-rules_groups).


## Using Severity Rules
{: #parse-severity-2}

By default, parsing rules includes a *Severity Rule* that matches logs of all severities, applications, and subsystems.

You can change the rule to limit the logs processed by the other rules you define in the group to only specific severity values, applications, or subsystems.


## Configuring a Severity Rule
{: #parse-severity-3-ui}
{: ui}

Complete the following steps to create a Severity Rule:

1. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Parsing rules** and click **Severity Rules**.

2. In the **Details** section, enter the *Rule Group Name* and the *Rule Group Description*. By default, the *Rule Group Name* is `Severity Rules`.

3. In the **Rule Matcher** section, configure the applications, subsystems, and severities that define the logs on which to apply the rules that are included in the rules group.

4. Open the **Rules** section. By default an [`Extract` rule](/docs/cloud-logs?topic=cloud-logs-parse-extract-rule&interface=ui) is provided to extract default severity values. Review this rule and modify for your environment if required.

5. Add additional rule groups by clicking **Add Rule** and selecting the desired rule type. Toggle **AND**/**OR** to select how you would like the additional rules processed. 

6. Click **Create Rule Group**.

Rules can be made active or inactive using a switcher. Active rules will be evaluated against log data.
{: tip}



