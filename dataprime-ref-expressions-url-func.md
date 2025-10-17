---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# DataPrime: URL decoding / encoding
{: #dataprime-ref-url-func}

This guide provides a glossary of {{site.data.keyword.logs_full}} DataPrime URL functions for encoding and decoding URLs.
{: shortdesc}

`urlDecode` and `urlEncode` support the function and the method notation.

## `urlEncode`
{: #urlencode}

Use `urlEncode` to convert characters into a format that can be transmitted over the Internet.

To send a URL over the Internet, the URL must be set using the ASCII character-set. For example, you might need to encode a set of characters and replace an empty space with `%20`.

### Function
{: #urlencode-func}

```text
urlEncode(string: string): string
```
{: codeblock}

For example, you could use the following sample to encode the value of `query_string_parameters.name` by using a function:

```text
replace query_string_parameters.name with urlEncode(query_string_parameters.name)
```
{: codeblock}



### Method
{: #urlencode-method}

```text
string: string.urlEncode(): string
```
{: codeblock}

For example, you could use the following sample to encode the value of `query_string_parameters.name` by using a method:

```text
replace query_string_parameters.name with query_string_parameters.name.urlEncode()
```
{: codeblock}



## `urlDecode`
{: #urldecode}

Use `urlDecode` to convert a URL into a format that is user friendly.


### Function
{: #urldecode-func}

```text
urlDecode(string: string): string
```
{: codeblock}

For example, you could use the following sample to decode the value of `query_string_parameters.name` by using a function:

```text
replace query_string_parameters.name with urlDecode(query_string_parameters.name)
```
{: codeblock}



### Method
{: #urldecode-method}

```text
string: string.urlDecode(): string
```
{: codeblock}

For example, you could use the following sample to decode the value of `query_string_parameters.name` by using a method:

```text
replace query_string_parameters.name with query_string_parameters.name.urlDecode()
```
{: codeblock}


## Example: Converting the URL header parameters into a JSON Object and URL decoding
{: #dataprime-ref-url-func-sample}

Consider the following log line:

```json
{
  "domain": "https://www.ibm.com",
  "path": "/home",
  "query_string": "name=My%20Name&b=c%20d&c=d"
}
```
{: codeblock}

First, extract each query string parameter into its own object field.

```text
extract query_string into query_string_parameters using kv(pair_delimiter='&',key_delimiter='=')
```
{: codeblock}

The resulting document looks like this:

```json
{
  "domain":"https://www.ibm.com",
  "query_string":"name=My%20Name&b=c%20d&c=d",
  "path": "/home",
  "query_string_parameters":{
    "name":"My%20Name",
    "b":"c%20d",
    "c":"d"
  }
}
```
{: codeblock}

Then, decode the `query_string_parameters.name` and replace `%20` with an empty space. Use `replace` to overwrite the old field with a new one and overwrite the value of an existing keypath with a new one.

```text
replace query_string_parameters.name with urlDecode(query_string_parameters.name)
replace query_string_parameters.b with urlDecode(query_string_parameters.b)
```
{: codeblock}

This results in the following document:

```json
{
  "domain":"https://www.ibm.com",
  "query_string":"name=My%20Name&b=c%20d&c=d",
  "path": "/home",
  "query_string_parameters":{
    "name":"My name",
    "b":"c d",
    "c":"d"
  }
}
```
{: codeblock}
