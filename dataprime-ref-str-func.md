---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-01"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}# DataPrime string functions
{: #dataprime-ref-str-func}

This guide provides a full glossary of all available DataPrime string functions.
{: shortdesc}

## `chr`
{: #chr}

Returns the Unicode code point number as a single character string.

```text
chr(number: number): string
```
{: codebock}



## `codepoint`
{: #codepoint}

Returns the Unicode code point of the only character of string.

```text
codepoint(string: string): number
```
{: codeblock}



## `concat`
{: #concat}


Concatenates multiple strings into one.


```text
concat(value: string, ...values: string): string
```
{: codeblock}


## `contains`
{: #contains}

Returns true if substring is contained in string

```text
contains(string: string, substring: string): bool
```
{: codeblock}



## `endsWith`
{: #endswith}

Returns true if string ends with suffix

```text
endsWith(string: string, suffix: string): bool
```
{: codeblock}



## `indexOf`
{: #indexof}

Returns the position of substring in string, or -1 if not found.

```text
indexOf(string: string, substring: string): number
```
{: codeblock}



### `length`
{: #length}

Returns the length of value

```text
length(value: string): number
```
{: codeblock}



### `ltrim`
{: #ltrim}

Removes whitespace to the left of the string value

```text
ltrim(value: string): string
```
{: codeblock}



## `matches`
{: #matches}

Evaluates the regular expression pattern and determines if it is contained within string.

```text
matches(string: string, regexp: regexp): bool
```
{: codeblock}



## `pad`
{: #pad}

Left pads string to `charCount`. If `size < fillWith.length()` of string, result is truncated. See [`padLeft`](#padleft) for more details. Alias for `padLeft`.

```text
pad(value: string, charCount: number, fillWith: string): string
```
{: codeblock}



## `padLeft`
{: #padleft}

```text
padLeft(value: string, charCount: number, fillWith: string): string
```
{: codeblock}

Left pads string to `charCount`. If `size < fillWith.length()` of string, result is truncated.

## `padRight`
{: #padright}

Right pads string to `charCount`. If `size < fillWith.length()` of string, result is truncated.

```text
padRight(value: string, charCount: number, fillWith: string): string
```
{: codeblock}



## `regexpSplitParts`
{: #regexpsplitparts}

Splits string on regexp-delimiter, returns the field at index. Indexes start with 1.

```text
regexpSplitParts(string: string, delimiter: regexp, index: number): string
```
{: codeblock}



## `rtrim`
{: #rtrim}


Removes whitespace to the right of the string value.

```text
rtrim(value: string): string
```
{: codeblock}


## `splitParts`
{: #splitparts}

Splits string on delimiter, returns the field at index. Indexes start with 1.

```text
splitParts(string: string, delimiter: string, index: number): string
```
{: codeblock}



## `startsWith`
{: #startswith}

Returns true if string starts with prefix.

```text
startsWith(string: string, prefix: string): bool
```
{: codeblock}



## `substr`
{: #substr}

Returns the substring in value, from position from and up to length `length`.

```text
substr(value: string, from: number, length: number?): string
```
{: codeblock}



## `toLowerCase`
{: #tolowercase}

Converts value to lowercase.

```text
toLowerCase(value: string): string
```
{: codeblock}



## `toUpperCase`
{: #touppercase}

Converts value to uppercase.

```text
toUpperCase(value: string): string
```
{: codeblock}



## `trim`
{: #trim}

Removes whitespace from the edges of a string value.

```text
trim(value: string): string
```
{: codeblock}



## String interpolation
{: #string-interpolation}

* `this is an interpolated {$d.some_keypath} string` – `{$d.some_keypath}` will be replaced with the evaluated expression that is enclosed by the brackets.

* ``this is how you escape \{ and \} and \` `` – The backward slash `\` is used to escape characters such as `{` and `}` that are used for keypaths.
