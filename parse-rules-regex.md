---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-21"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Building RegEx expressions
{: #parse-rules-regex}

In {{site.data.keyword.logs_full}}, you can use parsing rules to control the structure of your data by applying RegEx expressions before the data is indexed for search.
{: shortdesc}

{{site.data.keyword.logs_full_notm}} uses the RegEx Golang flavor.

A RegEx pattern is case-sensitive.
{: important}

## Quantifiers
{: #parse-rules-regex-1}

| Quantifier | Matches |
|------------|---------|
| `*`        | 0 or more matches of the previous character or sequence.|
| `?`        | 0 or 1 matches of the previous character or sequence.|
| `+`        | 1 or more matches of the previous character or sequence.|
| `{N}`      | Matches exactly N times the previous character. |
| `{N,}`     | Matches N or more times the previous character. |
| `{N,Z}`    | Matches between N and Z times the previous character. |
{: caption="Quantifiers" caption-side="bottom"}



## Characters
{: #parse-rules-regex-2}

| Characters | Matches |
|------------|---------|
| `.`        | Matches any single character. |
| `.*`       | Matches anything. |
| `\d`       | Matches 1 single digit. |
| `\d*`      | Matches N digits. |
| `\D`       | Matches any symbol except digits. |
| `\w`       | Matches any letter, digit, or underscore. |
| `\W`       | Matches any character that is not a letter, digit, or underscore. |
| `\s`       | Matches a whitespace character.  |
| `\S`       | Matches any character except space, tab, newline or carriage return. |
| `\s*`      | Matches N whitespace characters. |
| `\S`       | Matches any character that is not whitespace. |
| `\S*`      | Matches N characters that are not whitespace. |
{: caption="Characters" caption-side="bottom"}



## Anchors
{: #parse-rules-regex-3}


| Anchors | Matches |
|------------|---------|
| `\b` | Defines a word boundary. |
| `^` | Matches the start of a string or line. |
| `$` | Matches the end of a string or line. |
{: caption="Anchors" caption-side="bottom"}



## Groupings
{: #parse-rules-regex-4}

| Grouping            | Matches |
|---------------------|---------|
| `[ ]`               | Represents a group of characters. |
| `( )`               | Used to group patterns. |
| `[abcd...]`         | Matches 1 character of the ones included within the square brackets. |
| `[a-z]`             | Matches 1 character in the range of a to z. |
| `[^a-z]`            | Matches 1 character that is not in the range of a to z. |
| `[....]+`           | Matches 1 or more characters of the ones listed within the square brackets. |
| `[....]?`           | Matches 1 or 0 characters of the ones listed within the square brackets. |
| `[^"]*`             | Matches N characters except double quotes. |
| `[^"\s]*`           | Matches N characters except double quotes and white space. |
| `[^.]*`             | Matches 0 or more non-dots. |
{: caption="Groupings" caption-side="bottom"}



## Named capture groups
{: #parse-rules-regex-capture-groups}

You can use named captured groups in a RegEx expression to define new fields from existing data in the log record.
{: note}

The format of a capture group is the following:

```text
(?P<fieldName>RegularExpression)
```
{: codeblock}

Where

- `?P` represents the beginning of a capture group.
- `fieldName` must be set to the name of the field being added.
- `RegularExpression` represents the RegEx that defines the value of the new field.

    The RegEx doesn’t have to match the entire log.
