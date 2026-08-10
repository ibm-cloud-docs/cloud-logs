---

copyright:
  years:  2024, 2026
lastupdated: "2026-08-10"

keywords:

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Quering alerts in {{site.data.keyword.logs_full_notm}}
{: #alerts-queries}

In {{site.data.keyword.logs_full}}, you can use Lucene query syntax to define the triggering condition for an alert.
{: shortdesc}

You must validate the query in the **Log Explorer** to check the logs that are filtered are the expected ones.
{: important}


## Lucene queries
{: #alerts-queries-lucene-query}

A Lucene query is composed of *Terms* and *Operators*. Terms are extracted from the log data.

There are two types of terms:

Single terms
:   This is a word in a text field that is not enclosed in double quotation marks (").

Phrase
:   This is a group of words enclosed in double quotation marks (").


**Recommendation**: Whether you use 1 word or a group of words, always enclose them in double quotation marks (").
{: tip}


## Core concepts
{: #alerts-queries-core-concepts}

You must understand the following ideas before writing reliable alert queries.

1. `.Keyword` subfield

Most text fields have a companion `.Keyword` sub-field that holds the raw, un-tokenized value. The `.Keyword` bypasses the analyzer, which gives predictable results. This is the only field type on which regex matching is reliable in an alert.

2. Regex: delimiters and anchoring

A regular expression must be wrapped in forward slash delimiters: for example, `/pattern/`.
A `.Keyword` regex is anchored to the entire field value, so it matches only when the whole field equals the pattern. To match a field value that contains your text within it, add the pattern with `.*` on both the sides. Regex characters that are placed inside plain double quotation marks for example, `field:"a.*b"` are considered as literal text, not as a pattern. This is a common source of unexpected results.


## Writing alert queries
{: #alerts-queries-writing}

The **Logs Explorer** and the alerting engine are independent query engines with different Lucene implementations. The **Logs Explorer** runs queries through the DataPrime implementation, which normalizes quoting and returns results. The alerting engine uses a separate real-time matcher service that evaluates each incoming log against the alert query as it arrives. The matcher applies stricter parsing and analysis rules.

The most reliable approach is to match against a field's `.keyword` sub-field by using a regex pattern padded with `.*` at both ends, so that it matches any value that contains your text:

```text
field.keyword:/.*value.*/
```
{: codeblock}

Follow the below methods:

1. Use .keyword with regex for exact and pattern matches

Query a field's .keyword sub-field inside forward-slash regex delimiters. As .keyword stores the raw, un-tokenised value, it bypasses the Lucene analyzer and produces consistent, predictable results in the alert engine.

| Instead of                   | Write                     |
| message:"payment failed"     | message.keyword:/.*payment.*failed.*/ |

2. Anchor patterns for a "contains" match

A .keyword regex matches the entire field value from start to end. If you query status.keyword:/error/, it only matches logs where the field value is exactly error — nothing more. To match any value that merely contains your text, pad the pattern with .* at both ends.

| Instead of                   | Write                     |
| status.keyword:/error/     | status.keyword:/.*error.*/  |

3. Quote plain string values

When you are not using a regex pattern, enclose text values in double quotes so they are treated as a phrase and matched exactly as written, rather than being passed through the Lucene analyzer.

| Instead of         | Write                      |
| http_status:200    | http_status.numeric:200     |

4. Escape special characters in regex patterns

Several characters have special meaning inside a Lucene regex pattern and must be escaped with a backslash so that the alert engine treats them as literal characters rather than operators. If these characters are not escaped, the pattern does not match as expected.

The characters that must be escaped are: `+`, `-`, `&&`, `|`, `!`, `(`, `)`, `{`, `}`, `[`, `]`, `^`, `"`, `~`, `*`, `?`, `:`, `\` and `/`.

Hyphens (`-`) are the most common cause of a query that appears correct but matches nothing. A hyphen that is not escaped is treated as a range operator, which splits the value into separate tokens that do not match the intended string. For absence and "less than" alert types, a query that matches nothing causes the alert engine to treat the absence condition as met and fire a false trigger.

Escape each special character in your value with a backslash inside the regex pattern. For example:

| Instead of                 | Write                                          |
| service_name:"auth-gateway-prod" | service_name.keyword:/.*auth\-gateway\-prod.*/ |

5.  Use values of atleast three characters

The Lucene analyzer drops tokens that are shorter than three characters during indexing. This means that short values such as `v2,` `01,` or `5` are silently removed from standard text fields and cannot be matched by a direct field query. If you must match a short value, use the .keyword sub-field with a regex pattern to bypass the analyzer.

| Instead of         | Write                          |
| log_level:"to"     | log_level.keyword:/.*to.*/     |

6. Extract values from arrays or nested fields first

The alert engine do not support querying any values that are nested inside arrays or structures. If the value you want to match is stored in an array or nested fields, use a parsing rule to extract it into a top-level field first. Then, write your alery query against that field.

| Instead of                   | Write                          |
| users.email.keyword:/.*@example\.com/    | _exists_:user_email    |

7. Use a metric for numeric thresholds

The alert engine does not support numeric comparison operators sych as greater than or less than directly in a log query. If you need to alert when a numeric value crosses a threshold, use *Events2Metrics* to convert the log field into a metric. Then, configure a metric alert with the threshold condition.

| Instead of         | Write                          |
| duration:>1000    | Events2Metrics metric for duration, then alert when the metric > 1000   |

8. Maintain matched values concise

Match a distinctive part of a long value rather than the entire string. When you write an alert query, you can also configure:

    * Group-by fields : Indicates grouping by short fields, for example *service-name*, *subsystem* etc than by lengthy unique identifiers.

    * Included fields: Maximum value length of 256 characters. If an included field contains a value that exceeds this limit, the notification payload truncates. If you need information from a long field in a notification, use a short distinctive portion of the value into a dedicated top-level field.

9. Use well-informed field names

Alert queries do not support field names that contain spaces. If the fiels you want to query has a space in its name, create a *parsing rule* that extracts the value into a new field with a space free name, and query that field in your alert.

10. Scope the alert to the correct data

Every log in {{site.data.keyword.logs_full_notm}} is assigned to one of three TCO tiers: Low ("Store & Search"), Medium ("Analyze & Alert"), or High ("Priority Insights"). The alert engine evaluates only logs in the Medium and High tiers. The logs in the Low tier are excluded from alert evaluation entirely.

A query that returns results in the **Logs Explorer** will never trigger an alert if those logs are in the Low tier. Before you configure an alert, confirm that the logs you want to alert on are assigned to the Medium or High tier.

11. Add delay for abscence alerts

For less than or abscence type alerts, you must configure an evaluation delay to prevent normal ingestion latency from causing a false or premature or false alarm. Without a delay, the alert engine may evaluate a time window before all logs for that period have arrived. This can cause an absence alert to fire prematurely.


### Exceptional cases
{: #alerts-queries-exceptional-cases}

1. Avoid bare wildcards

A bare wildcard such as `field:val*` is not a reliable way to match values in the alert engine. Wildcard queries on standard text fields are subject to Lucene analyzer tokenization, which can produce inconsistent or unexpected results. The alert engine may not evaluate wildcard patterns the same way that the **Logs Explorer** does.

Use a `.keyword` regex with `.*` anchors instead, which bypasses the analyzer and produces consistent results:

| Instead of  | Write                   |
| field:val*  | field.keyword:/.*val.*/ |


2. A field that does not display as expected

If a field returns results in a wider search but the alert does not fire, the field may not be present or correctly mapped. The alert engine evaluates only logs in the Medium and High TCO tiers. A field that exists in the low tier is not available to the alert engine.

To confirm whether the field is available in the alert engine, search for the field in **Priorty Insights**. If the field does not appear, check the TCO policy for the logs and reconfigure it so that the logs flow to medium or high tier.

If the field is present in **Priorty Insights**, but the alert does not fire yet, then query the field `.keyword`.
