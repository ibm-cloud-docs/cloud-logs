---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-01"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# DataPrime operators reference
{: #dataprime-ref-operators}

This guide provides a full glossary of all available DataPrime operators.
{: shortdesc}

## `block`
{: #block}

The negation of `filter`. Filters-out all events where the condition is true. The same effect can be achieved by using `filter` with `!(condition)`.

```bash
block $d.status_code >= 200 && $d.status_code <= 299         # Leave all events which don't have a status code of 2xx
```
{: codeblock}

The data is exposed using the following fields:

* $m - Event metadata

   * `timestamp`
   * `severity` – Possible values are `Verbose`, `Debug`, `Info`, `Warning`, `Error`, `Critical`
   * `priorityclass` – Possible values are `high`, `medium`, `low`
   * `logid`

* $l - Event labels

   * `applicationname`
   * `subsystemname`
   * `category`
   * `classname`
   * `computername`
   * `methodname`
   * `threadid`
   * `ipaddress`

* $d -The user’s data

## `bottom`
{: #bottom}

*No grouping variation*: Limits the rows returned to a specified number and order the result by a set of expressions.

```text
order_direction := "descending"/"ascending" according to top/bottom
bottom <limit> <result_expression1> [as <alias>] [, <result_expression2> [as <alias2>], ...] by <orderby_expression> [as alias>]
```
{: codeblock}

For example, the following query:

```text
bottom 5 $m.severity as $d.log_severity by $d.duration
```
{: codeblock}

Will result in logs of the following form:

```text
[
   { "log_severity": "Debug", "duration":  1000 }
   { "log_severity": "Warning", "duration": 2000 },
   ...
]
```
{: codeblock}

*Grouping variation*: Limits the rows returned to a specified number and groups them by a set of aggregation expressions and orders them by a set of expressions.

```text
order_direction := "descending"/"ascending" according to top/bottom

bottom <limit> <(groupby_expression1|aggregate_function1)> [as <alias>] [, <(groupby_expression2|aggregate_function2)> [as <alias2>], ...] by <(groupby_expression1|aggregate_function1)> [as <alias>]
```
{: codeblock}

For example, the following query:

```text
bottom 10 $m.severity, count() as $d.number_of_severities by avg($d.duration) as $d.avg_duration
```
{: codeblock}

Will result in logs of the following form:

```text
[
   { "severity": "Warning", "number_of_severities": 50, avg_duration: 1000 },
   { "severity": "Debug", "number_of_severities":  10, avg_duration: 2000 }
   ...
]
```
{: codeblock}

Supported aggregation functions are listed in “Aggregation Functions” section.

## `choose`
{: #choose}

Leave only the keypaths provided, discarding all other keys. Fully supports nested keypaths in the output.

```text
(choose|select) <keypath1> [as <new_keypath>],<keypath2> [as <new_keypath>],...
```
{: codeblock}

Examples:

```text
choose $d.mysuperkey.myfield
choose $d.my_superkey.mykey as $d.important_value, 10 as $d.the_value_ten
```
{: codeblock}

## `convert`
{: #convert}

Convert the data types of keys.

The `datatypes` keyword is optional and can be used for readability.

```text
(conv|convert) [datatypes] <keypath1>:<datatype1>,<keypath2>:<datatype2>,...
```
{: codeblock}

Examples:

```text
convert $d.level:number
conv datatypes $d.long:number,$d.lat:number
convert $d.data.color:number,$d.item:string
```
{: codeblock}

## `count`
{: #count}

Returns a single row containing the number of rows produced by the preceding operators.

```text
count [into <keypath>]
```
{: codeblock}

An alias can be provided to override the keypath where the result will be written.

For example, the following part of a query:

```text
count into $d.num_rows
```
{: codeblock}

Will result in a single row of the following form:

```text
{ "num_rows": 7532 }
```
{: codeblock}

## `countby`
{: #countby}

Returns a row counting all the rows grouped by the expression.

```text
countby <expression> [as <alias>] [into <keypath>]
```
{: codeblock}

An alias can be provided to override the keypath the result will be written into.

For example, the following part of a query

```text
countby $d.verb into $d.verb_count
```
{: codeblock}

Will result in a row for each group.

It is functionally identical to

```text
groupby $data.verb calculate count() as $d.verb_count
```
{: codeblock}

## `create`
{: #create}

Create a new key and set its value to the result of the expression. Key creation is granular, meaning that parent keys in the path are not overwritten.

```text
  (a|add|c|create) <keypath> from <expression> [on keypath exists (fail|skip|overwrite)] [on keypath missing (fail|create|skip)] [on datatype change (skip|fail|overwrite)
```
{: codeblock}

The creation can be controlled by adding the following clauses:

* Adding `keypath exists` allows to choose what to do when the keypath already exists.

   * `overwrite` – Overwrites the old value. This is the default value

   * `fail` – Fails the query

   * `skip` – Skips the creation of the key

* Adding `keypath missing` chooses what to do when the new keypath does not exist.

   * `create` – Creates the key. This is the default value

   * `fail` – Fails the query

   * `skip` – Skips the creation of the new key

* Adding on `datatype changed` chooses what to do if the key already exists and the new data changes the datatype of the value.

   * `overwrite` – Overwrites the value. This is the default value.

   * `fail` – Fails the query

   * `skip` – Leaves the key with the original value (and type)

Examples:

```text
create $d.radius from 100+23
c $d.log_data.truncated_message from $d.message.substring(1,50)
c $data.trimmed_name from $data.username.trim()

create $d.temperature from 100*23 on datatype changed skip
```
{: codeblock}

## `distinct`
{: #distinct}

Returns one row for each distinct combination of the provided expressions.

```text
distinct <expression> [as <alias>] [, <expression_2> [as <alias_2>], ...]
```
{: codeblock}

This operator is functionally identical to `groupby` without any aggregate functions.

## `enrich`
{: #enrich}

Enrich your logs using additional context from a lookup table.

Upload your lookup table using **Data flow** ![Data Flow icon](/images/flow--data.svg "Data Flow") > Data Enrichment > Custom Enrichment.



```text
enrich <value_to_lookup> into <enriched_key> using <lookup_table>
```
{: codeblock}

* `value_to_lookup` – A string expression that will be looked up in the lookup table.

* `enriched_key` – Destination key to store the enrichment result.

* `lookup_table` – The name of the Custom Enrichment table to be used.

The table’s columns will be added as sub-keys to the destination key. If `value_to_lookup` is not found, the destination key will be null.
You can then filter the results using the DataPrime capabilities, such as filtering logs by specific value in the enriched field.

Example:

The original log:

```json
{
    "userid": "111",
    ...
}
```
{: codeblock}

The Custom Enrichment lookup table called `my_users`:

| ID | Name | Department|
|----|----|----|
| 111 |	John | Finance |
| 222 |	Emily |	IT |
{: caption="Sample lookup table" caption-side="bottom"}


Running the following query:

```text
enrich $d.userid into $d.user_enriched using my_users
```
{: codeblock}

Will result in the following enriched log:

```json
{
    "userid": "111",
    "user_enriched": {
        "ID": "111",
        "Name": "John",
        "Department": "Finance"
    },
    ...
}
```
{: codeblock}

Consider the following when using `enrich`:

* Run the DataPrime query source `lookup_table` to view the enrichment table.

* If the original log already contains the enriched key:

   * If `value_to_lookup` exists in the `lookup_table`, the sub-keys will be updated with the new value. If the `value_to_lookup` does not exist, their current value will remain.

   * Any other sub-keys which are not columns in the `lookup_table` will remain with their existing values.

* All values in the `lookup_table` are considered to be strings. This means that:

   * The `value_to_lookup` must be in a string format.

   * All values are enriched in a string format. You can then convert them to your preferred format (for example, JSON, timestamp) using the appropriate functions.

## `extract`
{: #extract}

Extract data from some string value into a new object. Multiple extraction methods are supported.

```text
(e|extract) <expression> into <keypath> using <extraction-type>(<extraction-params>) [datatypes keypath:datatype,keypath:datatype,...]
```
{: codeblock}

The following are the supported extraction methods and their parameters:

* `regexp` – Create a new object based on regexp capture-groups

* `e` – A regular expression with names capture-groups.

Example:

```text
extract $d.my_text into $d.my_data using regexp(e=/user (?<user>.*) has logged in/)
```
{: codeblock}

* `kv` – Extract a new object from a string that contains key=value key=value... pairs

* `pair_delimiter` – The delimiter to expect between pairs. Default is (a space)

* `key_delimiter` – The delimiter to expect separating between a key and a value. Default is =.

Examples:

```text
extract $d.text into $d.my_kvs using kv()
e $d.text into $d.my_kvs using kv(pair_delimiter=' ',key_delimiter='=')
```
{: codeblock}


* `jsonobject` – Extract a new object from a string contains an encoded json object, potentially attempting to unescape the string before decoding it into a json

* `max_unescape_count` – Max number of escaping levels to unescape before parsing the json. Default is 1. When set to 1 or more, the engine will detect whether the value contains an escaped JSON string and unescape it until its parsable or max unescape count is exceeded.

Example:

```text
e $d.json_message_as_str into $d.json_message using jsonobject(max_unescape_count=1)
```
{: codeblock}

It is possible to provide datatype information as part of the extraction, by using the datatypes clause. For example, adding datatypes `my_field:number` to an extraction would cause the extract `my_field` keypath to be a number instead of a string. For example:

```text
extract $d.my_msg into $d.data using kv() datatypes my_field:number
```
{: codeblock}

Extracted data always goes into a new keypath as an object, allowing further processing of the new keys inside that new object. For example:

```text
# Assuming a dataset which look like that:
{ "msg": "query_type=fetch query_id=100 query_results_duration_ms=232" }
{ "msg": "query_type=fetch query_id=200 query_results_duration_ms=1001" }

# And the following DataPrime query:
source logs
  | extract $d.msg into $d.query_data using kv() datatypes
query_results_duration_ms:number
  | filter $d.query_data.query_results_duration_ms > 500

# The results will contain only the second message, in which the duration is greater than 500 ms
```
{: codeblock}

## `filter`
{: #filter}

Filter events, leaving only events for which the condition evaluates to true.

```text
(f|filter|where) <condition-expression>
```
{: codeblock}

Examples:

```text
f $d.radius > 10
filter $m.severity.toUpperCase() == 'INFO'
filter $l.applicationname == 'myapp'
filter $l.applicationname == 'myapp' && $d.msg.contains('failure')
```
{: codeblock}

Comparison with null works only for scalar values and will always return null on JSON subtrees.
{: note}


When using a condition to compare a keypath with null, this will only work on scalar values (string, number, timestamp and so on). For JSON objects within a given document, comparing with null will always return null.

Use filter with functions to perform complex searches.

Examples:

```text
filter in($l.applicationname, 'ibm-audit-event', 'ibm-platform-logs') #
filter ipInSubnet(ip_address, '155.64.5.20/24')
```
{: codeblock}

e - Filter for IP addresses in a given range.
filter can be coupled with functions to perform complex searches with very little syntax, for example using the ipInSubnet function:


filter ipInSubnet(ip_address, '154.67.8.20/24')


## `groupby`
{: #groupby}

Groups the results of the preceding operators by the specified grouping expressions and calculates aggregate functions for every group created.

```text
groupby <grouping_expression> [as <alias>] [, <grouping_expression_2> [as <alias_2>], ...] [calculate]
  <aggregate_function> [as <result_keypath>]
  [, <aggregate_function_2> [as <result_keypath_2], ...]
```
{: codeblock}

For example, the following query:

```text
groupby $m.severity calculate sum($d.duration)
```
{: codeblock}

Will result in logs of the following form:

```json
{ "severity": "Warning", "_sum": 17045 }
```
{: codeblock}

The keypaths for the grouping expressions will always be under `$d`. Using the `as` keyword, we can rename the keypath for the grouping expressions and aggregation functions. For example:

```text
groupby $l.applicationname as $d.app calculate sum($d.duration) as $d.sum_duration
```
{: codeblock}

Will result in logs of the following form:

```json
{ "app": "web-api", "sum_duration": 17045 }
```
{: codeblock}

When querying with the `groupby` operator, you can apply an [aggregation function](#aggregation_functions) (such `asavg`, `max`, `sum`) to the bucket of results. This feature gives you the power to manipulate an aggregation expression inside the expression itself, allowing you to calculate and manipulate your data simultaneously.



## `join`
{: #join}

`Join` merges the results of the current (left) query with a second (right) query based on a specified condition. It offers multiple forms to control how the data is combined and supports nesting, allowing the right query to include its own `join` command.

`Join` supports three variations:

`join left`|`join`
:   For each event in the left query, the command selects a matching event from the right query based on the specified condition. If no match is found, rows are included for all events in the left query. Unmatched rows from the right query are set to `null`.

`join full`
:   Returns a row for every event, including those that may not have a match in either query (left or right), filling missing values with `null`.


`join inner`
:   Only returns rows where there are non-null results from both queries.


`join cross`
:   Pairs each row from the left query with every row from the right query, generating the full Cartesian product. Unlike other `join` types, `join cross` does not support `on` or `using conditions`. It functions similarly to a `join inner` but without any filtering, returning all possible row combinations.

For `left` (default), `inner`, and `full`, you can specify either a `join` condition by using the `on` keyword or a keypath using the by using `keyword`. The Cartesian product is filtered to retain only rows where the condition holds true or where the keypath values match on both sides.

Since all joins, regardless of the modifier, are based on the Cartesian product, duplicate results can occur if the `join` condition matches multiple times. To prevent unintended duplication, consider preprocessing subqueries, such as by using distinct.



Syntax:

```text
<left_side_query> | join [left/inner/full] (<right_side_query>) on <condition> into <right_side_target>
<left_side_query> | join [left/inner/full] (<right_side_query>) using <join_keypath_1> [, <join_keypath_2>, ...] into <right_side_target>
<left_side_query> | join cross (<right_side_query>) into <right_side_target>
```
{: codeblock}

Where:

* `<right_side_query>` - The `<right_side_query>` denotes the new query to be joined to.

* `<left_side_query>` - The `<left_side_query>` denotes the initial query, for example, in the query `source logs | filter x != null | join ...`, the left hand side query is `source logs | filter x != null`.

* `<condition>` - The condition if results from both queries should be joined.


   In the condition, you can use the `left=>` and `right=>` prefixes to refer to the events of the left and right queries, respectively. However, it is not required if a keypath exists in only one of the queries.

   When using the `==` (equality) operator in your condition, it must compare a keypath from the left query with a keypath from the right query. However, given that the keypaths must be unique or prefixed with `left=>` or `right=>`, the ordering of the operands is not important.


* `<join_keypath_n>` - `<join_keypath_n>` as a join key means to join results where a given keypath is equal in the results of both the left side query and the right side query.

* `<right_side_target>` - The keypath where the joined data will be added to the current query.

### `join` example
{: #join_basic}

You have this [custom enrichment](/docs/cloud-logs?topic=cloud-logs-enriching-data) table named `users` providing information on IDs related to names:

```json
{ "id": "111", "name": "John" }
{ "id": "222", "name": "Emily" }
{ "id": "333", "name": "Alice" }
```
{: codeblock}

And this data providing login events and user IDs, but not the user name associated with the user IDs.

```json
{ "userid": "111", "timestamp": "2022-01-01T12:00:00Z" }
{ "userid": "111", "timestamp": "2022-01-01T12:30:00Z" }
{ "userid": "222", "timestamp": "2022-01-01T13:00:00Z" }
{ "userid": "222", "timestamp": "2022-01-01T13:00:00Z" }
{ "userid": "222", "timestamp": "2022-01-01T13:00:00Z" }
```
{: codeblock}

Using `join` you can use a query to return data including the desired data.

```text
source users | join (source logs | countby userid) on id == userid into logins
```
{: codeblock}

This query is processed as follows:

* The `source` is the custom enrichment table (`users`).

* In the `join`, a count by the `userid` field is generated. This gives us our `count` statistics.

* The `id` field in the custom enrichment table is compared with the `userid` field in the logs.

* The result is pushed into the `logins` key. If the `logins` key already exists on the left hand query, it will be overwritten.

For example:

```json
{ "id": "111", "name": "John", "logins": { "userid": "111", "_count": 2 } }
{ "id": "222", "name": "Emily", "logins": { "userid": "222", "_count": 3 } }
{ "id": "333", "name": "Alice", "logins": null }
```
{: codeblock}

The result of the right side query now is inside the `logins` field. Note that there were no logins for user ID `333` (Alice), so the logins field is `null` because there was no result matched by the `join` condition.

### `join` example with the `using` keyword
{: #join_using}

Consider if our login dataset is:

```json
{ "id": "111", "timestamp": "2022-01-01T12:00:00Z" }
{ "id": "111", "timestamp": "2022-01-01T12:30:00Z" }
{ "id": "222", "timestamp": "2022-01-01T13:00:00Z" }
{ "id": "222", "timestamp": "2022-01-01T13:00:00Z" }
{ "id": "222", "timestamp": "2022-01-01T13:00:00Z" }
```
{: codeblock}

In this case data on both sides of the join include the field `id`. In this case the `using` keyword can be used to take advantage of the common data:

```text
source users | join (source logins | countby id) using id into logins
```
{: codeblock}

The result will be similar, but instead of `userid`, the field `id` is returned.

```json
{ "id": "111", "name": "John", "logins": { "id": "111", "_count": 2 } }
{ "id": "222", "name": "Emily", "logins": { "id": "222", "_count": 3 } }
{ "id": "333", "name": "Alice", "logins": null }
```
{: codeblock}

If you have two fields that are named differently but would simplify your `join` query, you can use [`move`](/docs/cloud-logs?topic=cloud-logs-dataprime-ref#move) to move one of the fields so keypaths match on both sides.
{: tip}

### `join` example using `left=>` and `right=>` keywords
{: #join_left_right}

You can use the `left=>` and `right=>` prefixes to refer to the events of the left and right queries. However, it is not required if a keypath exists in only one of the queries.

Using the data from the previous example, consider the query:

```text
source users | join (source logins | countby id) on left=>id == right=>id into logins
```
{: codeblock}

This is required because both data sets contain a field with the same name (`id`). For DataPrime to uniquely identify a field, it must know which side of the query we are referring. This query will result in the same output as the previous that used the `using` keyword.

When using the `==` (equality) operator in your condition, it must compare a keypath from the left query with a keypath from the right query. However, given that the keypaths must be unique or prefixed with `left=>` or `right=>`, the ordering of the operands is not important.
{: tip}

### `join full` example
{: #join_full}

You have this [custom enrichment](/docs/cloud-logs?topic=cloud-logs-enriching-data) table named `users` providing information on IDs related to names:

```json
{ "id": "111", "name": "John" }
{ "id": "222", "name": "Emily" }
{ "id": "333", "name": "Alice" }
```
{: codeblock}

And consider this dataset:

```json
{ "id": "001", "timestamp": "2022-01-01T12:00:00Z" }
{ "id": "111", "timestamp": "2022-01-01T12:00:00Z" }
{ "id": "111", "timestamp": "2022-01-01T12:30:00Z" }
{ "id": "222", "timestamp": "2022-01-01T13:00:00Z" }
{ "id": "222", "timestamp": "2022-01-01T13:00:00Z" }
{ "id": "222", "timestamp": "2022-01-01T13:00:00Z" }
```
{: codeblock}

The second set of documents (right query) includes a log entry with `"id": "001"` that does not exist in the first set of documents (left query). If you use a standard join, this entry from the right query will be ignored and will not appear in the result. To ensure that every `id` field is included in the output, whether or not it appears in the left or right query, you can use `join full`:

```text
source users | join full (source logins | countby id) using id into logins
```
{: codeblock}

This query results in:

```json
{ "id": "001", "name": "null", "logins": { "id": "001", "_count": 1 } }
{ "id": "111", "name": "John", "logins": { "id": "111", "_count": 2 } }
{ "id": "222", "name": "Emily", "logins": { "id": "222", "_count": 3 } }
{ "id": "333", "name": "Alice", "logins": null }
```
{: codeblock}

By using `join full`, all `id` fields from both datasets are preserved, and any missing values are set to `null`.

`join full` is particularly useful when the results of both queries include time buckets. For example, if the left query's results are missing a time bucket for a specific hour (for example, `XX:XX:XX`), with `join full` this data point is included. This is especially useful for comparing two time series on a graph.
{: tip}

### `join inner` example
{: #join_inner}

If you want to remove any rows if column results for the left or right queries that produce a null value, use `join inner`.

Using the previous data, this query removes rows with unmatched data from either side:

```text
source users | join inner (source logins | countby id) using id into logins
```
{: codeblock}

* The left query `source users` retrieves the users dataset containing the fields `id` and `name`.

* The right query (`source logins | countby id`) retrieves the logins dataset, grouping by `id` and counting occurrences for each `id`.

* `join inner` matches rows where `id` exists in both datasets and merges the data into a single record.

* Rows with no match in either dataset are excluded from the final results.

In this case, for the two document sets above, results will be as follows:

```json
{ "id": "111", "name": "John", "logins": { "id": "111", "_count": 2 } }
{ "id": "222", "name": "Emily", "logins": { "id": "222", "_count": 3 } }
```
{: codeblock}



### `join cross` example
{: #join_cross}

`join cross` combines every row from the left query with every row from the right query, producing a Cartesian product of the two sets.

Assume that we have the following documents from a custom enrichment table named `users`.

```json
{ "id": "111", "name": "John" }
{ "id": "222", "name": "Emily" }
{ "id": "333", "name": "Alice" }
```
{: codeblock}

Now, consider this set of documents named `logs`.

```json
{ "id": "111", "timestamp": "2022-01-01T12:00:00Z" }
{ "id": "111", "timestamp": "2022-01-01T12:30:00Z" }
{ "id": "222", "timestamp": "2022-01-01T13:00:00Z" }
{ "id": "222", "timestamp": "2022-01-01T13:00:00Z" }
{ "id": "222", "timestamp": "2022-01-01T13:00:00Z" }
```
{: codeblock}

The following query will produce a Cartesian product of the `users` and `logs` datasets because `join cross` pairs every row from the left query with every row from the right query, regardless of any matching conditions.

```text
source users | join cross (source logs) into logins
```
{: codeblock}

```json
{ "id": "111", "name": "John", "logins": { "id": "111", "timestamp": "2022-01-01T12:00:00Z" } }
{ "id": "111", "name": "John", "logins": { "id": "111", "timestamp": "2022-01-01T12:30:00Z" } }
{ "id": "111", "name": "John", "logins": { "id": "222", "timestamp": "2022-01-01T13:00:00Z" } }
{ "id": "111", "name": "John", "logins": { "id": "222", "timestamp": "2022-01-01T13:00:00Z" } }
{ "id": "111", "name": "John", "logins": { "id": "222", "timestamp": "2022-01-01T13:00:00Z" } }
{ "id": "222", "name": "Emily", "logins": { "id": "111", "timestamp": "2022-01-01T12:00:00Z" } }
{ "id": "222", "name": "Emily", "logins": { "id": "111", "timestamp": "2022-01-01T12:30:00Z" } }
{ "id": "222", "name": "Emily", "logins": { "id": "222", "timestamp": "2022-01-01T13:00:00Z" } }
{ "id": "222", "name": "Emily", "logins": { "id": "222", "timestamp": "2022-01-01T13:00:00Z" } }
{ "id": "222", "name": "Emily", "logins": { "id": "222", "timestamp": "2022-01-01T13:00:00Z" } }
{ "id": "333", "name": "Alice", "logins": { "id": "111", "timestamp": "2022-01-01T12:00:00Z" } }
{ "id": "333", "name": "Alice", "logins": { "id": "111", "timestamp": "2022-01-01T12:30:00Z" } }
{ "id": "333", "name": "Alice", "logins": { "id": "222", "timestamp": "2022-01-01T13:00:00Z" } }
{ "id": "333", "name": "Alice", "logins": { "id": "222", "timestamp": "2022-01-01T13:00:00Z" } }
{ "id": "333", "name": "Alice", "logins": { "id": "222", "timestamp": "2022-01-01T13:00:00Z" } }
```
{: codeblock}

The query results in each user being paired with every log entry: 3 rows from `users` multiplied by 5 rows from `logs`, resulting in 15 rows. Each user (`John`, `Emily`, `Alice`) is paired with every log entry.

Using `join cross` is especially useful when you are interested in seeing a complete picture of your data, then adding a `left` or `right` `join` to these results.
{: tip}



### Limitations and considerations
{: #join_limitations}

There are limitations and considerations when including `join` in a query:

* The `join` condition only supports keypath equality (`==`). If multiple equality conditions are needed, they can be combined with `&&` (logical and).

* One side of the join (either current query or join query) must be small (< 200MB). You can use [`filter`](/docs/cloud-logs?topic=cloud-logs-dataprime-ref#filter) and [`remove`](/docs/cloud-logs?topic=cloud-logs-dataprime-ref#remove) to reduce the size of the query.

* Left outer joins require all columns in the condition to be non-null. **Any null columns will not be joined.** To include right hand query null columns, use `join full`. To exclude all null columns produced by the left and right joins, use `join inner`.




## `limit`
{: #limit}

Limits the output to the first `event-count` events.

```text
limit <event-count>
```
{: codeblock}

Example:

```text
limit 100
```
{: codeblock}

## `move`
{: #move}

Move a key (including its child keys, if any) to a new location.

```text
(m|move) <source-keypath> to <target-keypath>
```
{: codeblock}

Examples:

```text
move $d.my_data.hostname to $d.my_new_data.host
m $d.kubernetes.labels to $d.my_labels
```
{: codeblock}




## `multigroupby`
{: #multigroupby}


`multigroupby` concatenates the results from two or more queries incorporating `groupby` into a single dataset.

Use `multigroupby` for:

* Efficiency: Data is scanned only once for multiple queries.

* Synchronization: Results remain coherent, avoiding discrepancies that can arise when running separate queries.

```text
multigroupby  (<grouping_expression_1> as <alias> [, <grouping_expression_2> as <alias_2>, ...])  [, (<grouping_expression_1> as <alias> [, <grouping_expression_2> as <alias_2>, ...]), ...][calculate]  <aggregation_expression> [as <result_keypath>] [, <aggregation_expression_2> [as <result_keypath_2], ...]
```
{: codeblock}

By using the same alias `app` for both groupings, the same semantic meaning is presented as a unified field. In the next example, different aliases are used and the data is combined, but not merged.

### Example - `Multigroupby` with the same alias
{: #multigrouby-same-alias}

In this example we want to group our logs as follows:

* First by `applicationname` (`app`) and then further by `subsystemname` (`ss`), providing detailed counts for each combination.

* Then independently by `applicationname`, giving total counts of logs for each application regardless of `subsystems`.

```text
source logs
| multigroupby ($l.applicationname as app, $l.subsystemname as ss),($l.applicationname as app) calculate count() | orderby app,ss
```
{: codeblock}

The result will be similar to:

```json
[
    {
        "_count0": 241,
        "app": "monitoring24",
        "ss": "NO_SUBSYSTEM_NAME"
    },
    {
        "_count0": 231,
        "app": "monitoring24",
        "ss": "logs-opentelemetry-agent"
    },
    {
        "_count0": 15,
        "app": "monitoring24",
        "ss": "logs-opentelemetry-collector"
    },
    {
        "_count0": 487,
        "app": "monitoring24",
        "ss": null
    }
]
```
{: codeblock}

The first three rows represent counts for each unique combination of `app` and `ss`. For example, there are 241 logs where the application (`app`) is `monitoring24` and the subsystem (`ss`) is `NO_SUBSYSTEM_NAME`. Similarly, there are 231 logs for the same application but with the subsystem `logs-opentelemetry-agent`, and so on.

The final row provides a total count of logs for the application `monitoring24`, aggregating all subsystems. Here, `_count0` is 487, the sum of all the detailed counts above. The `ss` field is `null` to indicate this is the total for the application as a whole.

By using the same alias `app` for both groupings, the same semantic meaning is presented as a unified field. In the next example, different aliases are used and the data is combined, but not merged.
{: note}

### Example - `Multigroupby` with different aliases
{: #multigrouby-diff-alias}

Now, consider the effects of introducing 2 different aliases for the queries. In this case, the first grouping is labeled as `app1` for `applicationname` combined with `ss`, while the second grouping is labeled as `app2` for `applicationname` `alone`.

```text
source logs | multigroupby ($l.applicationname as app1, $l.subsystemname as ss),($l.applicationname as app2) calculate count()
```
{: codebock}

The result will be similar to:

```json
[
    {
        "_count0": 241,
        "app1": "monitoring24",
        "app2": null,
        "ss": "logs-opentelemetry-agent"
    },
    {
        "_count0": 231,
        "app1": "monitoring24",
        "app2": null,
        "ss": "logs-opentelemetry-collector"
    },
    {
        "_count0": 15,
        "app1": "monitoring24",
        "app2": null,
        "ss": "no_subsystem_name"
    },
    {
        "_count0": 487,
        "app1": null,
        "app2": "monitoring24",
        "ss": null
    }
]
```
{: codeblock}

By introducing separate aliases (`app1` and `app2`), the query maintains the distinction between the two groupings rather than merging the data. Rows where `app1` is populated and `app2` is `null` correspond to the detailed grouping by `applicationname` and `subsystemname`. For instance, 241 logs are associated with `app1 = "monitoring24"` and `ss = "logs-opentelemetry-agent"`. This follows the first grouping logic.

The row where `app2` is populated and `app1` is `null` reflects the total count for the second grouping, where logs are aggregated solely by `applicationname`. For `app2 = "monitoring24"`, the count is 487, and both `app1` and `ss` are `null` to indicate this higher-level aggregation.

By using separate aliases (`app1` and `app2`), the query does not merge the data, but rather makes it clear which group each result belongs to. The overall logic remains the same: detailed counts for specific combinations and aggregate counts for the total.

### `Multigroupby` limitations
{: #multigrouby-limitations}

`multigroupby` doesn’t return duplicate rows for duplicate group sets.

If you run `multigroupby` with app and ss, the expected result (if duplicates were allowed) might look like this:

```json
[
  {"app": "monitoring24", "ss": "logs-opentelemetry-agent", "_count0": 2},
  {"app": "monitoring24", "ss": "logs-opentelemetry-collector", "_count0": 2}
]
```
{: codeblock}

Due to the limitation, `multigroupby` will merge these duplicates and return only one row for each unique combination, even if that combination occurs multiple times in the data:

```json
[
  {"app": "monitoring24", "ss": "logs-opentelemetry-agent", "_count0": 2}
]
```
{: codeblock}



## `orderby` / `sortby` / `order by` / `sort by`
{: #order_sort}

Sort the data by ascending/descending order of the expression value. Ordering by multiple expressions is supported.

```text
(orderby|sortby|order by|sort by) <expression> [(asc|desc)] , ...
```
{: codeblock}

Examples:

```text
orderby $d.myfield.myfield
orderby $d.myfield.myfield:number desc
sortby $d.myfield desc
```
{: codeblock}

Sorting numeric values can be done by casting expression to the type:, for example, `<expression>: number`. In some cases, this will be inferred automatically by the engine.

## `redact`
{: #redact}

Replace all substrings matching a regexp pattern from some keypath value, effectively hiding the original content.

The matching keyword is optional and can be used to increase readability.

```text
redact <keypath> [matching] /<regular-expression>/ to '<redacted_str>'
redact <keypath> [matching] <string> to '<redacted_str>'
```
{: codeblock}

Examples:

```text
redact $d.mykey /[0-9]+/ to 'SOME_INTEGER'
redact $d.mysuperkey.user_id 'root' to 'UNKNOWN_USER'
redact $d.mysuperkey.user_id matchingn 'root' to 'UNKNOWN_USER'
```
{: codeblock}

## `remove`
{: #remove}

Remove a keypath from the object.

```text
r|remove <keypath1> [ "," <keypath2> ]...
```
{: codeblock}

Examples:

```text
r $d.mydata.unneeded_key
remove $d.mysuperkey.service_name, $d.mysuperkey.unneeded_key
```
{: codeblock}

## `replace`
{: #replace}

Replace the value of some key with a new value.

If the replacement value changes the datatype of the keypath, the following options are available:

* `skip` – The replacement will be ignored

* `fail` – The query will fail

* `overwrite` – The new value will overwrite the previous one, changing the datatype of the keypath

```text
replace <keypath> with <expression> [on datatype changed skip/fail/overwrite]
```
{: codeblock}

Examples:

```text
replace $d.message with null
replace $d.some_superkey.log_length_plus_10 with $d.original_log.length()+10 on datatype changed overwrite
```
{: codeblock}

## `roundtime`
{: #roundtime}

Rounds the time of the event into some time interval, possibly creating a new key for the result.

* If `source-timestamp` is not provided, then `$m.timestamp` is used as the source timestamp.

* If `source-timestamp` is provided, it should be of type (or cast to) `timestamp`.

By default, the rounded result is written back to the source keypath `source-timestamp`. If into `target-keypath` is provided, then `source-timestamp` is not modified, and the result is written to a new `target-keypath`.

Supported time intervals are:

* Xns – X nanoseconds (Be cautious of the source-timestamp‘s resolution)
* Xms – X milliseconds
* Xs – X seconds
* Xm – X minutes
* Xh – X hours
* Xd – X days

And any combination from greater to lesser time units, for example,  `1h30m15s`.

```text
roundtime [source-timestamp] to <time-interval> [into <target-keypath>]
```
{: codeblock}

Examples:

```text
roundtime to 1h into $d.tm
roundtime $d.timestamp to 1h
roundtime $d.my_timestamp: timestamp to 60m
roundtime to 60s into $d.rounded_ts_to_the_minute
```
{: codeblock}

## `source`
{: #source}

Set the data source that your DataPrime query is based on.

```text
(source|from) <data_store>
```
{: codeblock}

Where `data_store` can be either:

* `logs`


* The name of the custom enrichment. In this case, the command will display the custom enrichment table.

Examples:

```text
source logs
```
{: codeblock}



## `stitch`
{: #stitch}

The `stitch` command performs a horizontal union of two datasets, combining them side-by-side. It aligns rows from one dataset with rows from another and concatenates their columns, creating a single, unified dataset.

When using the `stitch` command:

* Datasets must be ordered, since rows are combined in sequence (that is, row 1 of dataset A is stitched with row 1 of dataset B).

* If one dataset has more rows than the other, unmatched rows will have null values in the stitched columns.

* The resulting dataset will contain all columns from both datasets.


`stitch` differs from `union`. `stitch` combines datasets horizontally by appending columns row-by-row. `union` appends rows vertically, stacking datasets on top of each other.


```text
... | stitch (<subquery>) into <target-keypath>
```
{: codeblock}

Example:

You have these [custom enrichment](/docs/cloud-logs?topic=cloud-logs-enriching-data) tables:

`sales` dataset:

```json
{ "product": "Widget", "sales": 100 }
{ "product": "Gadget", "sales": 200 }
{ "product": "Dashboard", "sales": 150 }
```
{: codeblock}

`revenue` dataset:

```json
{ "product": "Widget", "revenue": 5000 }
{ "product": "Gadget", "revenue": 8000 }
{ "product": "Dashboard", "revenue": 6000 }
```
{: codeblock}

In this query you will combine these datasets side-by-side, ensuring that each row from one dataset aligns with the corresponding row from the other:

```text
source sales | orderby product
| stitch (source revenue | orderby product) into combined_data
```
{: codeblock}

* `source sales` fetches all rows from the `sales` dataset, which contains products and their corresponding sales figures.

* `orderby product` sorts the `sales` dataset by the `product` field to creae a consistent order for row alignment.

* `stitch (source revenue | orderby product)` fetches rows from the `revenue` dataset and sorts them by the `product` field. The `sales` and `revenue` datasets are combined horizontally, aligning rows based on their order after sorting.

* `into combined_data` stores the combined dataset into a variable called `combined_data`.

The result from the query is:

```json
{ "product": "Widget", "sales": 100, "combined_data": { "product": "Widget", "revenue": 5000 } }
{ "product": "Gadget", "sales": 200, "combined_data": { "product": "Gadget", "revenue": 8000 } }
{ "product": "Dashboard", "sales": 150, "combined_data": { "product": "Dashboard", "revenue": 6000 } }
```
{: codeblock}

If the datasets have unequal rows, the `stitch` command fills the missing values with `null`.

For example, consider the following datasets:

`sales` dataset (3 rows):

```json
{ "product": "Widget", "sales": 100 }
{ "product": "Gadget", "sales": 200 }
{ "product": "Dashboard", "sales": 150 }
```
{: codeblock}

`revenue` dataset (2 rows):

```json
{ "product": "Widget", "revenue": 5000 }
{ "product": "Gadget", "revenue": 8000 }
```
{: codeblock}

Running this query:

```text
source sales | orderby product
| stitch (source revenue | orderby product) into combined_data
```
{: codeblock}

Results in:

```json
{ "product": "Widget", "sales": 100, "combined_data": { "product": "Widget", "revenue": 5000 } }
{ "product": "Gadget", "sales": 200, "combined_data": { "product": "Gadget", "revenue": 8000 } }
{ "product": "Dashboard", "sales": 150, "combined_data": { "product": "Dashboard", "revenue": null } }
```
{: codeblock}

### `stitch` usage notes
{: #stitch_notes}

* Rows must correlate logically for stitching to produce meaningful results. Make sure that rows from both datasets represent the same entities and are in the same order. For example, if the `product` field in the `sales` dataset does not match the `product` field in the `revenue` dataset for corresponding rows, stitching will not work as expected.

* If datasets differ in row count, the result will include `null` values for missing data in the shorter dataset.




## `top`
{: #top}

*No grouping variation*: Limits the rows returned to a specified number and order the result by a set of expressions.

```text
order_direction := "descending"/"ascending" according to top/bottom

top <limit> <result_expression1> [as <alias>] [, <result_expression2> [as <alias2>], ...] by <orderby_expression> [as alias>]
```
{: codeblock}

For example, the following query:

```text
top 5 $m.severity as $d.log_severity by $d.duration
```
{: codeblock}

Will result in logs of the following form:

```json
[
   { "log_severity": "Warning", "duration": 2000 },
   { "log_severity": "Debug", "duration":  1000 }
   ...
]
```
{: codeblock}

*Grouping variation*: Limits the rows returned to a specified number and groups them by a set of aggregation expressions and orders them by a set of expressions.

```text
order_direction := "descending"/"ascending" according to top/bottom

top <limit> <(groupby_expression1|aggregate_function1)> [as <alias>] [, <(groupby_expression2|aggregate_function2)> [as <alias2>], ...] by <(groupby_expression1|aggregate_function1)> [as <alias>]
```
{: codeblock}

For example, the following query:

```text
top 10 $m.severity, count() as $d.number_of_severities by avg($d.duration) as $d.avg_duration
```
{: codeblock}

Will result in logs of the following form:

```json
[
   { "severity": "Debug", "number_of_severities":  10, avg_duration: 2000 }
   { "severity": "Warning", "number_of_severities": 50, avg_duration: 1000 },
   ...
]
```
{: codeblock}

You can apply an [aggregation function.](#aggregation_functions)



## `union`
{: #union}

The `union` command concatenates the results from two or more datasets into one dataset. This allows users to combine results from multiple queries into one seamless dataset. One dataset can be a result set piped into the `union` command and then concatenated with another dataset.

Use union when you need to append rows from one dataset to another.

When processing large datasets, to optimize performance, consider using `filter` to limit rows from each dataset before using `union`.
{: tip}

Users are limited to a maximum of 10 `union` commands per query for {{site.data.keyword.frequent-search}} data. There is no limit on other data.
{: restriction}

### How `union` differs from `join`
{: #union-vs-join}

* `union` combines result sets by appending rows from one dataset to another. It does not merge or compare columns from multiple documents.

* `join` matches and combines columns from two tables based on a condition, creating rows that contain data from both tables.

```text
<query> | union <query>
```
{: codeblock}

### Example combining 2 datasets
{: #union-combine}

You have these 2 datasets:

Logs for `Team 58942`

```json
{ "id": "111", "name": "John" , "team.id": "58942" }
{ "id": "222", "name": "Emily", "team.id": "58942" }
{ "id": "333", "name": "Alice", "team.id": "58942" }
```
{: codeblock}

Logs for `Team 98361`

```json
{ "userid": "111", "timestamp": "2022-01-01T12:00:00Z", "team.id": "98361" }
{ "userid": "111", "timestamp": "2022-01-01T12:30:00Z", "team.id": "98361" }
{ "userid": "222", "timestamp": "2022-01-01T13:00:00Z", "team.id": "98361" }
{ "userid": "222", "timestamp": "2022-01-01T13:00:00Z", "team.id": "98361" }
{ "userid": "222", "timestamp": "2022-01-01T13:00:00Z", "team.id": "98361" }
```
{: codeblock}

And you want to combine them into 1 dataset. You can do this using `union`.

```text
source logs(teamId=58942) | union logs(teamId=98361)
```
{: codeblock}

The query processes the two datasets:

* `source logs(teamId=58942)`: Retrieves all documents for `Team 58942`
* `union logs (teamID=98361)`: Appends the `Team 98361` dataset to the `Team 58942` dataset


This will result in the following dataset:

```json
{ "id": "111", "name": "John" , "team.id": "58942" }
{ "id": "222", "name": "Emily", "team.id": "58942" }
{ "id": "333", "name": "Alice", "team.id": "58942" }
{ "userid": "111", "timestamp": "2022-01-01T12:00:00Z", "team.id": "98361" }
{ "userid": "111", "timestamp": "2022-01-01T12:30:00Z", "team.id": "98361" }
{ "userid": "222", "timestamp": "2022-01-01T13:00:00Z", "team.id": "98361" }
{ "userid": "222", "timestamp": "2022-01-01T13:00:00Z", "team.id": "98361" }
{ "userid": "222", "timestamp": "2022-01-01T13:00:00Z", "team.id": "98361" }
```
{: codeblock}


