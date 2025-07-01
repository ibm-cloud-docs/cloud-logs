---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-01"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# DataPrime general functions
{: #dataprime-ref-expressions-gral-func}

This guide provides a full glossary of all available DataPrime general functions.
{: shortdesc}


## `firstNonNull`
{: #firstnonnull}

Returns the first non-null value from the parameters. Works only on scalars.

```text
firstNonNull(value: any, ...values: any): any
```
{: codeblock}


## `if`
{: #if}

Return either the `then` or `else` according to the result of `condition`.

```text
if(condition: bool, then: any, else: any?): any
```
{: codeblock}



## `in`
{: #in}

Tests if the comparand is equal to any of the values in a set v1 ... vN.

```text
in(comparand: any, value: any, ...values: any): bool
```
{: codeblock}



## `recordLocation`
{: #recordlocation}

Returns the location of the record (for example, s3 URL).

```text
recordLocation(): string
```
{: codeblock}
