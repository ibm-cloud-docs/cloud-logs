---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# DataPrime expressions and constructs
{: #dataprime-ref-expressions}

This guide providesan overview of {{site.data.keyword.logs_full}} DataPrime expressions and constructs.
{: shortdesc}

## Expressions
{: #expressions}

DataPrime supports a limited set of JavaScript constructs that can be used in expressions.

The data is exposed using the following fields:

* $m – Event metadata

   * `timestamp`

   * `severity` – Possible values are `Verbose`, `Debug`, `Info`, `Warning`, `Error`, and `Critical`.

   * `priorityclass` – Possible values are high, medium, low.

   * `logid`

* $l – Event labels

   * `applicationname`

   * `subsystemname`

   * `category`

   * `classname`

   * `computername`

   * `methodname`

   * `threadid`

   * `ipaddress`

* $d – The user’s data

## Field Access
{: #field-access}

Accessing nested data is done by using a keypath, similar to any programming language or JSON tool. Keys with special characters can be accessed using a map-like syntax, with the key string as the map index, for example, `$d.my_superkey['my_field_with_a_special/character']`.

Examples:

```text
$m.timestamp
$d.my_superkey.myfield
$d.my_superkey['my_field_with_a_special/character']
$l.applicationname
```
{: codeblock}

## Language Constructs
{: #language-constructs}

All standard language constructs are supported:

* Constants

* Nested field access

* Basic math operations between numbers, including modulo (%)

* Boolean operations &&, ||, !

* Comparisons

* String concatenations through `concat`.

* casting – A simple notation for casting data types: for example,  `$d.temperature:number`. Type inference is automatically applied when possible.

## Text Search
{: #text-search}

Boolean expressions are available for text search:

* `$d.field ~ 'text phrase'` – case-insensitive search for a text phrase in a specific field.

* `$d ~~ 'text phrase'` – case-insensitive search for a text phrase in `$d`.


## Scalar Functions
{: #scalar}

Various functions can be used to transform values. All functions can be called as methods as well, for example, `$d.msg.contains('x')` is equivalent to `contains($d.msg,'x')`.


