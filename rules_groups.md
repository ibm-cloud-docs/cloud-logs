---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-18"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Working with rule groups
{: #rules_groups}

In {{site.data.keyword.logs_full}}, parsing rules are organized inside *Rule Groups*. Each group has a name and a set of rules with a logical relationship between them. Logs are processed according to the order of rule group (from the beginning to the end). They are then processed by the order of rules within the rule group and according to the logical operators between them (`AND/OR`). Rules help you to process, parse, and restructure log data to prepare for monitoring and analysis.
{: shortdesc}


## Creating a rules group
{: #rules_groups_create}

To create a rule group in the {{site.data.keyword.logs_full}} UI, click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **Parsing rules** and click **New Rule Group** or choose one of the quick rule creation options.

A rule group definition has several sections. Complete the following steps to create a rule group:

1. In the **Details** section, enter the *Rule Group Name* and the *Rule Group Description*.

    Each group has a name and can have an optional description.

2. In the **Rule Matcher** section, configure the applications, subsystems, and severities that define the logs on which to apply the rules that are included in the rules group.

    The *Rule Matcher* section defines a query. Only logs that match the rule matcher query are processed by the group. This matching is important in making sure that only intended logs go through the group rules and for performance reasons. 

    The rule matcher query is defined by selecting a set of applications, subsystems, and severities. Only logs that match all components of the query are processed by the group. All entries in the section are optional. If you do not select a field, or define a RegEx, the Rule Group runs on all of your logs. 

3. In the **Rules** section, configure a sequence of rules to apply on the data.

    The ordering of rules is important, as it affects the final outcome.

    The options for rules include:

    - Parse rule: Rule to convert unstructured text into JSON.

    - Extract: Rule to extract specific values you need as JSON keys without having to parse the entire log.

    - Extract JSON: Rule to extract the value of a JSON key into a metadata field.

    - Replace: Rule to fix log structure, change the log severity, or obscure information.

    - Block: Rule to filter out incoming logs by using a RegEx expression.

    - Timestamp Extract: Rule to replace the log timestamp with a timestamp that is included in the log record.

    - Exclude Fields: Rule to remove JSON fields and reduce the number of indexed fields.

    - Stringify JSON Field: Rule to reduce the amount of indexed fields by transforming a JSON object into a stringify JSON field.

    - Parse JSON Field: Rule to transform escaped or stringified logs to JSON format.

    When you create a rule, you can use the sample log area to verify your rule. Create or paste a log in to this area and it shows you the results of the rule that processes the log.
    {: tip}

## Changing the order of execution of rules groups
{: #rules_groups_order_change}

You can change the order for rule groups. You can change their order by dragging them to reorder them in the list.


## Deleting a rules group
{: #rules_groups_delete}


To delete a rule group, click the group, and click **DELETE RULE GROUP**.


## Editing a rules group
{: #rules_groups_update}


To edit a rule group, click the group, make your changes, and click **SAVE CHANGES**.

### Adding more than 1 rule to a rules group
{: #rules_groups_add}

You can add more rules to a rules group after you create the rules group.

Complete the following steps to add more rules to a rules group:

1. Select the rule group. Then, select **ADD RULE**.

2. Select the logical relationship between an existing rule and a new one. You can use `AND/OR` logic.

   For example:

   `Rule-1 AND Rule-2` means that a log is always processed by both rules.

   `Rule-1 OR Rule-2` means that the log is processed by either Rule-1 or Rule-2, whichever matches first or neither if none match the log. In other words, if Rule-1 is a match to the log, then Rule-2 is not applied to it.

### Changing the order of execution of rules in a rules group
{: #rules_groups_rules_order_change}

You can change the order of execution of rules within a rules group by dragging the rule into a new position relative to other rules.




## Order of execution of rules
{: #rules_groups_execution_order}

As logs are ingested, rules groups are applied in order, starting from the top.

Within a rules group:
1. The rules group matcher query is applied first.

    Only logs that match the applications, subsystems and severities that are configured continue applying the parsing rules.

2. Parsing rules are then are applied top-down as defined in the parsing rules UI. You can drag and drop rules at different positions if you need to apply a rule before others.

   * The rules within a rule group are applied from the first rule in the list to the final listed rule.

   * You can combine rules within a rule group by selecting `AND` or `OR` conditions. When you select `AND`, all rules are tried and applied if the regex applies to that log line. When you select `OR`, as soon as a rule matches the log line, the rest of the rules are not applied.

   The `OR` and `AND` operators in the group do not follow the mathematical order of operations.

   Rules are applied immediately so that the output of one rule becomes the input of the next one.
   {: note}

The order of execution of rules groups and rules is important and define the final log’s structure.

Put block rules first and use the rule matcher when possible to prevent unnecessary processing of logs and speed-up your data processing.
{: important}

For example, consider these two rules that parse Heroku Postgres logs:

* [Postgres follower](https://regex101.com/r/IyjCIj/4){: external}

* [Postgres leader](https://regex101.com/r/aQJsp5/2){: external}

The follower log has this entry at the end: `follower_lag_commits`. This entry means that the leader rule captures both logs because it is less restrictive and all other fields match. Follower matches only the follower logs (the first test string is not captured in the follower example because it doesn’t have the additional entry). The follower rule would be run first. 



## Searching for a rules group
{: #rules_groups_search}

To quickly find a rule group, you can use the search function to search for rules. You can use rules or group names in the free text search field.

## Turning on or off a rules group
{: #rules_groups_toggle}

You can set to active or inactive a rule group by using the toggle associated with the rule group.
