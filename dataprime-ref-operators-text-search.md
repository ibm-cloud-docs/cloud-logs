# DataPrime text search operators reference
{: #dataprime-ref-operators-text-search}

This guide provides a full glossary of all available DataPrime operators.
{: shortdesc}

## `find` / `text`
{: #find_text}

Search for the string in a certain keypath.

```text
(find|text) <free-text-string> in <keypath>
```
{: codeblock}

Examples:

```text
find 'host1000' in $d.kubernetes.hostname
text 'us-east-1' in $d.msg
```
{: codeblock}

## `lucene`
{: #dp_lucene}

A generic Lucene-compatible operator, allowing both free and wild text searches, and more complex search queries.

Field names inside the lucene query are relative to `$d` (the root level of user-data).

```text
lucene <lucene-query-as-a-string>
```
{: codeblock}

Examples:

```text
lucene 'pod:recommender AND (is_error:true or status_code:404)'
```
{: codeblock}

## `wildfind` / `wildtext`
{: #wildfind_tex}

Search for the string in the entire user data. This can be used when the keypath in which the text resides is unknown.

The performance of this operator is slower than when using the `find/text` operator. Prefer using those operators when you know the keypath to search.
{: note}

```text
(wildfind/wildtext) <string>
```
{: codeblock}

Examples:

```text
wildfind 'my-region'
wildfind ':9092'
```
{: codeblock}
