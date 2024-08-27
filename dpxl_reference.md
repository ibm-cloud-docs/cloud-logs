---

copyright:
  years:  2024
lastupdated: "2024-08-26"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# DataPrime Expression Language (DPXL) reference
{: #dpxl_ref}

The DataPrime Expression Language, or DPXL, is an expression language based on DataPrime expression syntax.You can use it to define rich expression-based filters, such as when setting up streaming.
{: shortdesc}

DPXL expressions are a subset of DataPrime expressions, such as those used in the filter operator.

DPXL expressions are versioned to maintain predictability and stability. With versioning DPXL can be enhanced over time without changing the semantics of existing expressions.

Each DPXL expression starts with a version identifier `<vX>`, currently `<v1>`. This is followed by the actual boolean expression, including literals, logical and comparison constructs, keypath access, and functions.

```text
<v1> <boolean-expression>
```
{: codeblock}

The `<v>` prefix is automatically included when using the UI and does not need to be specified. However, a DPXL expression used in an API must start with the `<v1>` prefix.
{: tip}

```text
# A filter that returns true if my_text field has the value 'example'
<v1> $d.my_text == 'example'

# A filter that returns true if the event's timestamp is before the beginning of the year 2024
<v1> $m.timestamp < @'2024-01-01T00:00:00'

# A filter that returns true if the application name starts with 'dev-'
<v1> $l.applicationName.startsWith('dev-')

# A filter that returns true if the field region_id is us-east-1 or us-east-2
<v1> region_id:string.in('us-east-1', 'us-west-2')
```
{: codeblock}

## Data types
{: #dpxl_data_types}

DPXL supports different data types.

| Data type | Example |
|-----------|---------| 
| string | `'us-east-1’`  \n `’dev-’` |
| number | `23`  \n `-12.32` |
| bool | `true`  \n `false` |
| timestamp | `@(’2023-01-01T00:00Z’)`  \n `@’now’` |
| regular expression | `/H.*o$/`  \n `/^prod-.*/` |
| severity | `VERBOSE`  \n `DEBUG`  \n `INFO`  \n `WARNING`  \n `ERROR`  \n `CRITICAL` |
{: caption="Data types" caption-side="bottom"}

In addition, there’s a `null` literal, which can be used with all other types.

## Operators
{: #dpxl_operators}

DPXL supports multiple operators.

| Operator | Meaning | Example | Example description |
|----------|---------|---------|---------------------|
| `&&` | Logical AND | `country == ‘us’ && region == ‘us-south’` | Will return true if both the `country` is `us` and the `region` is `us-south`.
| `\|\|` | Logical OR |	`age > 40 \|\| country == ‘us’` | Will return true if either the `age` is above 40, or the `country` is `us`. |
| `!` | Logical NOT | `!region.contains(’us-’)` | Will return true if the `region` does not contain `us-` | 
{: caption="Operators" caption-side="bottom"}

### Ordering
{: #dpxl_ordering}

You can control the evaluation order inside an expression using parenthesis. For example:

```text
region.startsWith('us-') && 
(country == 'us' && (age > 40 || age < 10)) || (country == 'il' && age > 25)
```
{: codeblock}

## Comparison operators
{: #cpxl_compare}

DPXL supports multiple comparison operators.

| Operator | Meaning | Examples |
|----------|---------|----------|
| `>` |	Greater than | `duration > 40.5`  \n `$m.timestamp > @(’2023-01-01T00:00:00’)` |
| `>=` | Greater than or equals | `duration >= 40.5` |
| `<` | Less than | `age < 20` |
| `<=` | Less than or equals | `age <= 20`  \n `lastName <= ‘Smith’` |
| `==` | Equals | `region == 'us-south'` |
| `!=` | Not equal to | `first_name != 'joe'` |
{: caption="Comparison operators" caption-side="bottom"}


## Keypath
{: #dpxl_keypath}

Keypaths are divided into three different parts, each with a separate prefix:

`$m`
:   Metadata

`$l`
:   Labels, such as `applicationName` or `subsystemName`

`$d`
:   User data (default prefix)

### `$m` – Metadata keypaths
{: #dpxl_metadata}

| Keypath | Data type |	Description |
|---------|-----------|-------------|
| `$m.timestamp` | timestamp | Contains the timestamp of the event |
| `$m.severity` | severity | Contains the severity of the event |
{: caption="Metadata keypaths" caption-side="bottom"}


### `$l` – Label keypaths
{: #dpxl_label}

| Keypath | Data type |
|---------|-----------|
| `$l.applicationname` | string |
| `$l.subsystemname` | string |
{: caption="Label keypaths for logs" caption-side="bottom"}



### `$d` – User data keypaths
{: #dpxl_userdata}

Any user keypath can be accessed using `$d.<keypath>` including nested keypaths.

`$d` is the default prefix. Any keypath that does not contain a prefix will be considered a user data field.

## Functions
{: #dpxl_functions}

Functions provide additional capabilities within DPXL expressions.

| Function | Description | Example |
|----------|-------------|---------|
| `<s>.startsWith(<substr>):bool` |	Checks if a string `<s>` starts with the specified substring `<substr>` | `region.startsWith('us-')` |
| `<s>.endsWith(<substr>):bool` | Checks if a string `<s>` ends with the specified substring `<substr>` | `firstName.endsWith(’Jo’)` |
| `<s>.contains(<substr>):bool` | Checks if a string `<s>` contains the specified substring `<substr>` | `stream.contains(’err’)` |
| `<s>.matches(<regex>):bool` | Checks if a string `<s>` matches the specified pattern provided by the `<regex>` | `hostname.matches(/prod-.*/)` |
| `<value>.in(<value1>,<value2>,...)` | Checks if value is one of the provided values | `value1-valueN	region.in(’us-east’,’us-south’)` |
{: caption="Functions" caption-side="bottom"}


## Inferring data types
{: #dpxl_data_types_infer}

DPXL attempts to infer the expected datatype of keypaths. For example, when processing `age > 50`, it will infer that `age` is expected to be a number. In cases where DPXL cannot infer the data type for a keypath, it will require the necessary information about the type. For example:

```text 
'123':number

region1:string == region2

my_key:number > my_other_key
```
{: codeblock}

## Examples
{: #dpxl_examples}

The following are DPXL examples that you can use as a basis for your own DPXL expressions.

```text
# Allow access only to logs where the application name is "production"
<v1> $l.applicationname == 'production'
```
{: codeblock}

```text
# Allow access only to logs in which app name starts with dev, or the field "region_id" in the data is us-east
<v1> $l.applicationname.startsWith('dev-') && region_id == 'us-east'
```
{: codeblock}

```text
# Allow access only to logs in which the field "country" is not one of the listed below. 
<v1> !$d.country:string.in('us','il','gr')
```
{: codeblock}


```text
# Allow access only to logs where the pod name matches the regex provided
<v1> kubernetes.pod_name.matches(/^kafka-[0-9]+/)
```
{: codeblock}

 ```text
# Allow access only to logs that don't have a DEBUG severity
<v1> $m.severity != DEBUG
```
{: codeblock}

```text
# Allow access only to logs in which some query duration is very large
<v1> query_duration_seconds > 100
```
{: codeblock} 

```text
# Allow access only to logs up to the beginning of the year 2024
<v1> $m.timestamp < @'2024-01-01T00:00:00'
```
{: codeblock}

```text
# Disallow access to all logs entirely
<v1> false
```
{: codeblock}



### Inference limitations
{: #dpxl_inf_limit}

The `in` function cannot automatically infer the expected type of a keypath. To use the `in` function you need to indicate the type. For example:

```text
<v1> !$d.country:string.in('us','il','gr')
```
{: codepath}
