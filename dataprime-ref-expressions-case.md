---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# DataPrime case expressions
{: #dataprime-ref-expressions-case}

This guide provides a glossary of {{site.data.keyword.logs_full}} DataPrime case expressions.
{: shortdesc}


Case expressions are special constructs in the language that allow choosing between multiple options in a readable way. They can be wherever an expression is expected.
{: note}

## `case`
{: #case}

Choose between multiple values based on several generic conditions. Uses a default-value if no condition is met.

```text
case {
  condition1 -> value1,
  condition2 -> value2,
  ...
  conditionN -> valueN,
  _          -> <default-value>
}
```
{: codeblock}

Example:

```text
case {
  $d.status_code == 200 -> 'success',
  $d.status_code == 201 -> 'created',
  $d.status_code == 404 -> 'not-found',
  _ -> 'other'
}

# Here's the same example inside the context of a query. A new field is created with the `case` result,
# and then a filter will be applied, leaving only non-successful responses.

source logs | ... | create $d.http_response_outcome from case {
  $d.status_code == 200 -> 'success',
  $d.status_code == 201 -> 'created',
  $d.status_code == 404 -> 'not-found',
  _                     -> 'other'
} | filter $d.http_response_outcome != 'success'
```
{: codeblock}

## `case_contains`
{: #case-contains}

Shorthand for `case` which allows checking if a string `s` contains one of several substrings without repeating the expression leading to `s`. The chosen value is the first which matches `s.contains(substring)`.

```text
case_contains {
  s: string,
  substring1 -> result1,
  substring2 -> result2,
  ...
  substring3 -> resultN
}
```
{: codeblock}

Example:

```text
case_contains {
  $l.subsystemname,
  '-prod-' -> 'production',
  '-dev-'  -> 'development',
  '-stg-'  -> 'staging',
  _        -> 'test'
}
```
{: codeblock}

## `case_equals`
{: #caseequals}

Shorthand for case which allows comparing some expression `e` to several results without repeating the expression. The chosen value is the first which matches `s == value`.

```text
case_equals {
  e: any,
  value1 -> result1,
  value2 -> result2,
  ...
  valueN -> resultN
}
```
{: codeblock}

Example:

```text
case_equals {
  $m.severity,
  'info'   -> true,
  'warning -> true,
  _        -> false
}
```
{: codeblock}

## `case_greaterthan`
{: #casegreaterthan}

Shorthand for case which allows comparing `n` to multiple values without repeating the expression leading to `n`. The chosen value is the first which matches `expression > value`.

```text
case_greaterthan {
  n: number,
  value1: number -> result1,
  value2: number -> result2,
  ...
  valueN: number -> resultN,
  _              -> <default-value>
}
```
{: codeblock}

Example:

```text
case_greaterthan {
  $d.status_code,
  500 -> 'server-error',
  400 -> 'client-error',
  300 -> 'redirection',
  200 -> 'success',
  100 -> 'information',
  _   -> 'other'
}
```
{: codeblock}

## `case_lessthan`
{: #caselessthan}

Shorthand for case which allows comparing a number `n` to multiple values without repeating the expression leading to `n`. The chosen value is the first which matches `expression < value`.

```text
case_lessthan {
  n: number,
  value1: number -> result1,
  value2: number -> result2,
  ...
  valueN: number -> resultN,
  _              -> <default-value>
}
```
{: codeblock}

Example:

```text
case_lessthan {
  $d.temperature_celsius,
  10 -> 'freezing',
  20 -> 'cold',
  30 -> 'fun',
  45 -> 'hot',
  _  -> 'burning'
}
```
{: codeblock}
