---

copyright:
  years:  2024, 2025
lastupdated: "2025-03-31"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# DataPrime reference
{: #dataprime-ref}

This guide provides a full glossary of all available DataPrime operators and expressions.
{: shortdesc}

## Operators
{: #operators}

DataPrime provides the following operators.

### `block`
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

### `bottom`
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

### `choose`
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

### `convert`
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

### `count`
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

### `countby`
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

### `create`
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

### `distinct`
{: #distinct}

Returns one row for each distinct combination of the provided expressions.

```text
distinct <expression> [as <alias>] [, <expression_2> [as <alias_2>], ...]
```
{: codeblock}

This operator is functionally identical to `groupby` without any aggregate functions.

### `enrich`
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

### `extract`
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

### `filter`
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
filter $l.applicationname == 'recommender'
filter $l.applicationname == 'myapp' && $d.msg.contains('failure')
```
{: codeblock}

Comparison with null works only for scalar values and will always return null on JSON subtrees.
{: note}

### `groupby`
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



### `join`
{: #join}

`Join` merges the results of the current (left) query with a second (right) query based on a specified condition. It offers multiple forms to control how the data is combined and supports nesting, allowing the right query to include its own `join` command.

`Join` supports three variations:

`join left`|`join`
:   For each event in the left query, the command selects a matching event from the right query based on the specified condition. If no match is found, rows are included for all events in the left query. Unmatched rows from the right query are set to `null`.

`join full`
:   Returns a row for every event, including those that may not have a match in either query (left or right), filling missing values with `null`.

`join inner`
:   Only returns rows where there are non-null results from both queries.

Syntax:

```text
 <left_side_query> | join (<right_side_query>) on <condition> into <right_side_target>
 <left_side_query> | join (<right_side_query>) using <join_keypath_1> [, <join_keypath_2>, ...] into <right_side_target>
```
{: codeblock}

Where:

* `<right_side_query>` - The `<right_side_query>` denotes the new query to be joined to.

* `<left_side_query>` - The `<left_side_query>` denotes the initial query, for example, in the query `source logs | filter x != null | join ...`, the left hand side query is `source logs | filter x != null`.

* `<condition>` - The condition if results from both queries should be joined.

* `<join_keypath_n>` - `<join_keypath_n>` as a join key means to join results where a given keypath is equal in the results of both the left side query and the right side query.

* `<right_side_target>` - The keypath where the joined data will be added to the current query.

#### `join` example
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

#### `join` example with the `using` keyword
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

#### `join` example using `left=>` and `right=>` keywords
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

#### `join full` example
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

#### `join inner` example
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


#### Limitations and considerations
{: #join_limitations}

There are limitations and considerations when including `join` in a query:

* The `join` condition only supports keypath equality (`==`). If multiple equality conditions are needed, they can be combined with `&&` (logical and).

* One side of the join (either current query or join query) must be small (< 200MB). You can use [`filter`](/docs/cloud-logs?topic=cloud-logs-dataprime-ref#filter) and [`remove`](/docs/cloud-logs?topic=cloud-logs-dataprime-ref#remove) to reduce the size of the query.

* Left outer joins require all columns in the condition to be non-null. **Any null columns will not be joined.** To include right hand query null columns, use `join full`. To exclude all null columns produced by the left and right joins, use `join inner`.




### `limit`
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

### `move`
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




### `orderby` / `sortby` / `order by` / `sort by`
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

### `redact`
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

### `remove`
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

### `replace`
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

### `roundtime`
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

### `source`
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



### `stitch`
{: #stitch}

The `stitch` command performs a horizontal union of two datasets, combining them side-by-side. It aligns rows from one dataset with rows from another and concatenates their columns, creating a single, unified dataset.

When using the `stitch` command:

* Datasets must be ordered, since rows are combined in sequence (that is, row 1 of dataset A is stitched with row 1 of dataset B).

* If one dataset has more rows than the other, unmatched rows will have null values in the stitched columns.

* The resulting dataset will contain all columns from both datasets.



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

#### `stitch` usage notes
{: #stitch_notes}

* Rows must correlate logically for stitching to produce meaningful results. Make sure that rows from both datasets represent the same entities and are in the same order. For example, if the `product` field in the `sales` dataset does not match the `product` field in the `revenue` dataset for corresponding rows, stitching will not work as expected.

* If datasets differ in row count, the result will include `null` values for missing data in the shorter dataset.




### `top`
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



## Text Search Operators
{: #text_search}

### `find` / `text`
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

### `lucene`
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

### `wildfind` / `wildtext`
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

## String Functions
{: #string}

### `chr`
{: #chr}

Returns the Unicode code point number as a single character string.

```text
chr(number: number): string
```
{: codebock}



### `codepoint`
{: #codepoint}

Returns the Unicode code point of the only character of string.

```text
codepoint(string: string): number
```
{: codeblock}



### `concat`
{: #concat}


Concatenates multiple strings into one.


```text
concat(value: string, ...values: string): string
```
{: codeblock}


### `contains`
{: #contains}

Returns true if substring is contained in string

```text
contains(string: string, substring: string): bool
```
{: codeblock}



### `endsWith`
{: #endswith}

Returns true if string ends with suffix

```text
endsWith(string: string, suffix: string): bool
```
{: codeblock}



### `indexOf`
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



### `matches`
{: #matches}

Evaluates the regular expression pattern and determines if it is contained within string.

```text
matches(string: string, regexp: regexp): bool
```
{: codeblock}



### `pad`
{: #pad}

Left pads string to `charCount`. If `size < fillWith.length()` of string, result is truncated. See [`padLeft`](#padleft) for more details. Alias for `padLeft`.

```text
pad(value: string, charCount: number, fillWith: string): string
```
{: codeblock}



### `padLeft`
{: #padleft}

```text
padLeft(value: string, charCount: number, fillWith: string): string
```
{: codeblock}

Left pads string to `charCount`. If `size < fillWith.length()` of string, result is truncated.

### `padRight`
{: #padright}

Right pads string to `charCount`. If `size < fillWith.length()` of string, result is truncated.

```text
padRight(value: string, charCount: number, fillWith: string): string
```
{: codeblock}



### `regexpSplitParts`
{: #regexpsplitparts}

Splits string on regexp-delimiter, returns the field at index. Indexes start with 1.

```text
regexpSplitParts(string: string, delimiter: regexp, index: number): string
```
{: codeblock}



### `rtrim`
{: #rtrim}


Removes whitespace to the right of the string value.

```text
rtrim(value: string): string
```
{: codeblock}


### `splitParts`
{: #splitparts}

Splits string on delimiter, returns the field at index. Indexes start with 1.

```text
splitParts(string: string, delimiter: string, index: number): string
```
{: codeblock}



### `startsWith`
{: #startswith}

Returns true if string starts with prefix.

```text
startsWith(string: string, prefix: string): bool
```
{: codeblock}



### `substr`
{: #substr}

Returns the substring in value, from position from and up to length `length`.

```text
substr(value: string, from: number, length: number?): string
```
{: codeblock}



### `toLowerCase`
{: #tolowercase}

Converts value to lowercase.

```text
toLowerCase(value: string): string
```
{: codeblock}



### `toUpperCase`
{: #touppercase}

Converts value to uppercase.

```text
toUpperCase(value: string): string
```
{: codeblock}



### `trim`
{: #trim}

Removes whitespace from the edges of a string value.

```text
trim(value: string): string
```
{: codeblock}



## IP Functions
{: #ip-functions}

### `ipInSubnet`
{: #ipinsubnet}

Returns true if IP is in the subnet of `ipPrefix`.

```text
ipInSubnet(ip: string, ipPrefix: string): bool
```
{: codeblock}



### `ipPrefix`
{: #ipprefix}

Returns the IP prefix of a given IP address with `subnetSize` bits (for example, 192.128.0.0/9).

```text
ipPrefix(ip: string, subnetSize: number): string
```
{: codeblock}



### String interpolation
{: #string-interpolation}

* `this is an interpolated {$d.some_keypath} string` – `{$d.some_keypath}` will be replaced with the evaluated expression that is enclosed by the brackets.

* ``this is how you escape \{ and \} and \` `` – The backward slash `\` is used to escape characters such as `{` and `}` that are used for keypaths.


## UUID Functions
{: #uuid-functions}


### `isUuid`
{: #isuuid}

Returns true if UUID is valid.

```text
isUuid(uuid: string): bool
```
{: codeblock}



### `randomUuid`
{: #randomuuid}

Returns a random UUIDv4.

```text
randomUuid(): string
```
{: codeblock}


## General Functions
{: #general-functions}

### `firstNonNull`
{: #firstnonnull}

Returns the first non-null value from the parameters. Works only on scalars.

```text
firstNonNull(value: any, ...values: any): any
```
{: codeblock}


### `if`
{: #if}

Return either the `then` or `else` according to the result of `condition`.

```text
if(condition: bool, then: any, else: any?): any
```
{: codeblock}



### `in`
{: #in}

Tests if the comparand is equal to any of the values in a set v1 ... vN.

```text
in(comparand: any, value: any, ...values: any): bool
```
{: codeblock}



### `recordLocation`
{: #recordlocation}

Returns the location of the record (for example, s3 URL).

```text
recordLocation(): string
```
{: codeblock}



## Number Functions
{: #number-functions}

### `abs`
{: #abs}

Returns the absolute value of number.

```text
abs(number: number): number
```
{: codeblock}



### `ceil`
{: #ceil}

Rounds the value up to the nearest integer.

```text
ceil(number: number): number
```
{: codeblock}



### `e`
{: #euler}

Returns the constant Euler’s number.

```text
e(): number
```
{: codeblock}



### `floor`
{: #floor}

Rounds the value down to the nearest integer.

```text
floor(number: number): number
```
{: codeblock}



### `fromBase`
{: #frombase}

Returns the value of string interpreted as a base-radix number.

```text
fromBase(string: string, radix: number): number
```
{: codeblock}



### `ln`
{: #ln}

Returns the natural log of number.

```text
ln(number: number): number
```
{: codeblock}



### `log`
{: #log}

Returns the log of number in base `base`.

```text
log(base: number, number: number): number
```
{: codeblock}



### `log2`
{: #log2}

Returns the log of number in base 2. Equivalent to `log(2, number)`.

```text
log2(number: number): number
```
{: codeblock}



### `max`
{: #max-number}

Returns the maximum number of all the numbers passed to the function.

```text
max(value: number, ...values: number): number
```
{: codeblock}



### `min`
{: #min}

Returns the least number of all the numbers passed to the function.

```text
min(value: number, ...values: number): number
```
{: codeblock}



### `mod`
{: #mod}

Returns the modulus (remainder) of number divided by `divisor`.

```text
mod(number: number, divisor: number): number
```
{: codeblock}



### `pi`
{: #pi}

Returns the constant Pi.

```text
pi(): number
```
{: codeblock}



### `power`
{: #power}

Returns `number`^`exponent`.

```text
power(number: number, exponent: number): number
```
{: codeblock}



### `random`
{: #random}

Returns a pseudo-random value in the range 0.0 <= x < 1.0.

```text
random(): number
```
{: codeblock}



### `randomInt`
{: #randomint}

Returns a pseudo-random integer number between 0 and n (exclusive).

```text
randomInt(upperBound: number): number
```
{: codeblock}


### `round`
{: #round}

Round `number` to `digits` decimal places.

```text
round(number: number, digits: number?): number
```
{: codeblock}



### `sqrt`
{: #sqrt}

Returns square root of a number.

```text
sqrt(number: number): number
```
{: codeblock}



### `toBase`
{: #tobase}

Returns the base-radix representation of `number`.

```tex
toBase(number: number, radix: number): string
```
{: codeblock}



## URL Functions
{: #url-functions}

### `urlDecode`
{: #urldecode}

Unescapes the URL encoded in string. Contrast with [urlEncode](#urlencode).

```text
urlDecode(string: string): string
```
{: codeblock}



### `urlEncode`
{: #urlencode}

Escapes string by encoding it so that it can be safely included in URL. Contrast with [urlDecode](#urldecode).

```text
urlEncode(string: string): string
```
{: codeblock}


## Date / Time Functions
{: #date-time}

Functions for processing timestamps, intervals and other time-related constructs.

### Time Units
{: #time-units}

Many date/time functions accept a time unit argument to modify their behavior. DataPrime supports time units from nanoseconds to days. They are represented as literal strings of the time unit name in either long or short notation:

* long notation: `day`, `hour`, `minute`, `second`, `milli`, `micro`, `nano`

* short notation: `d`, `h`, `m`, `s`, `ms`, `us`, `ns`

### Time Zones
{: #time-zones}

DataPrime timestamps are always stored in the UTC time zone, but some date/time functions accept a time zone argument to modify their behavior. Time zone arguments are strings that specify a time zone offset, shorthand or identifier:

* time zone offset in hours (for example, '+01' or '-02')
* time zone offset in hours and minutes (for example, '+0130' or '-0230')
* time zone offset in hours and minutes with separator (for example '+01:30' or '-02:30')
* time zone shorthand (for example, 'UTC', 'GMT', 'EST', and so on)
* time zone identifier (for example, 'Asia/Yerevan', 'Europe/Zurich', 'America/Winnipeg', and so on)

### `addInterval`
{: #addinterval}

Adds two intervals together. Also works with negative intervals. Equivalent to `left + right`.

```text
addInterval(left: interval, right: interval): interval
```
{: codeblock}


### `addTime`
{: #addtime}

Adds an interval to a timestamp. Also works with negative intervals. Equivalent to `t + i`.

```text
addTime(t: timestamp, i: interval): timestamp
```
{: codeblock}



### `diffTime`
{: #difftime}

Calculates the duration between two timestamps. Positive if `to` > `from`, negative if `to` < `from`. Equivalent to `to - from`.

```text
diffTime(to: timestamp, from: timestamp): interval
```
{: codeblock}



### `extractTime`
{: #extracttime}

Extracts either a date or time unit from a timestamp. Returns a floating point number for time units less than a minute, otherwise an integer. Date units such as `month` or `week` start from 1 (not from 0).

```text
extractTime(timestamp: timestamp, unit: dateunit | timeunit, tz: string?): number
```
{: codeblock}

Function parameters:

* `timestamp` (required) – the timestamp to extract from.
* `unit` (required) – the date or time unit to extract. Must be a string literal and one of:
   * any time unit in either long or short notation
   * a date unit in long notation: `year`, `month`, `week`, `day_of_year`, `day_of_week`
   * a date unit in short notation: `Y`, `M`, `W`, `doy`, `dow`
* `tz` (optional) – a time zone to convert the timestamp before extracting.


Example 1: extract the hour in Tokyo

```text
limit 1 | choose $m.timestamp.extractTime('h', 'Asia/Tokyo') as h # Result 1: 11pm { "h": 23 }
```
{: codeblock}

Example 2: extract the number of seconds

```text
limit 1 | choose $m.timestamp.extractTime('second') as s # Result 2: 38.35 seconds { "s": 38.3510265 }
```
{: codeblock}

Example 3: extract the timestamp’s month

```text
limit 1 | choose $m.timestamp.extractTime('month') as m # Result 3: August { "m": 8 }
```
{: codeblock}

Example 4: extract the day of the week

```text
limit 1 | choose $m.timestamp.extractTime('dow') as d # Result 4: Tuesday { "d": 2 }
```
{: codeblock}



### `formatInterval`
{: #formatinterval}

Formats `interval` to a string with an optional time unit `scale`.

```text
formatInterval(interval: interval, scale: timeunit?): string
```
{: codeblock}

Function parameters:

* `interval` (required) – the interval to format.
* `scale` (optional) – the maximum time unit of the interval to show. Defaults to nano.


Example:

```text
limit 3 | choose formatInterval(now() - $m.timestamp, 's') as i # Results: { "i": "122s261ms466us27ns" } { "i": "122s359ms197us227ns" } { "i": "122s359ms197us227ns" }
```
{: codeblock}

### `formatTimestamp`
{: #formattimestamp}

Formats a timestamp to a string with an optional format specification and destination time zone.

```text
formatTimestamp(timestamp: timestamp, format: string?, tz: string?): string
```
{: codeblock}

Function parameters:

* `timestamp` (required) – the timestamp to format.
* `format` (optional) – a date/time format specification for parsing timestamps. Defaults to 'iso8601'. The format can be any string with embedded date/time formatters, or one of several shorthands. Here are a few samples:
   * '%Y-%m-%d' – print the date only, for example '2023-04-05'
   * '%H:%M:%S' – print the time only, for example '16:07:33'
   * '%F %H:%M:%S' – print both date and time, for example '2023-04-05 16:07:33'
   * 'iso8601' – print a timestamp in ISO 8601 format, for example '2023-04-05T16:07:33.123Z'
   * 'timestamp_milli' – print a timestamp in milliseconds (13 digits), for example '1680710853123'

`tz` (optional) – the destination time zone to convert the timestamp before formatting.

Example 1: print a timestamp with default format and +5h offset

```text
limit 1 | choose $m.timestamp.formatTimestamp(tz='+05') as ts # Result 1: { "ts": "2023-08-29T19:08:37.405937400+0500" }
```
{: codeblock}

Example 2: print only the year and month

```text
limit 1 | choose $m.timestamp.formatTimestamp('%Y-%m') as ym # Result 2: { "ym": "2023-08" }
```
{: codeblock}

Example 3: print only the hours and minutes

```text
limit 1 | choose $m.timestamp.formatTimestamp('%H:%M') as hm # Result 3: { "hm": "14:11" }
```
{: codeblock}

Example 4: print a timestamp in milliseconds (13 digits)

```text
limit 1 | choose $m.timestamp.formatTimestamp('timestamp_milli') as ms # Result 4: { "ms": "1693318678696" }
```
{: codeblock}

### `fromUnixTime`
{: #fromunixtime}

Converts a number of a specific time units since the UNIX epoch to a timestamp (in UTC). The UNIX epoch starts on January 1, 1970 – earlier timestamps are represented by negative numbers.

```text
fromUnixTime(unixTime: number, timeUnit: timeunit?): timestamp
```
{: codeblock}

Function parameters:

* `unixTime` (required) – the amount of time units to convert. Can be either positive or negative and will be rounded down to an integer.
* `timeUnit` (optional) – the time units to convert. Defaults to 'milli'.

Example:

```text
limit 1 | choose fromUnixTime(1658958157515, 'ms') as ts # Result: { "ts": 1658958157515000000 }
```
{: codeblock}

### `multiplyInterval`
{: #multiplyinterval}

Multiplies an interval by a numeric factor. Works both with integer and fractional numbers. Equivalent to `i * factor`.

```text
multiplyInterval(i: interval, factor: number): interval
```
{: codeblock}



### `now`
{: #now}

Returns the current time at query execution time. Stable across all rows and within the entire query, even when used multiple times. Nanosecond resolution if the runtime supports it, otherwise millisecond resolution.

```text
now(): timestamp
```
{: codeblock}



Example:

```text
limit 3 | choose now() as now, now() - $m.timestamp as since # Results: { "now": 1693312549105874700, "since": "14m954ms329us764ns" } { "now": 1693312549105874700, "since": "14m954ms329us764ns" } { "now": 1693312549105874700, "since": "14m960ms519us564ns" }
```
{: codeblock}

### `parseInterval`
{: #parseinterval}

Parses an interval from a string with format `NdNhNmNsNmsNusNns` where N is the amount of each time unit. Returns null when the input does not match the expected format:

* It consists of time unit components – a non-negative integer followed by the short time unit name. Supported time units are: 'd', 'h', 'm', 's', 'ms', 'us', 'ns'.
* There must be at least one time unit component.
* The same time unit cannot appear more than once.
* Components must be decreasing in time unit order – from days to nanoseconds.
* It can start with `-` to represent negative intervals.

```text
parseInterval(string: string): interval
```
{: codeblock}


Example 1: parse a zero interval

```text
limit 1 | choose '0s'.parseInterval() as i # Result 1: { "i": "0ns" }
```
{: codeblock}

Example 2: parse a positive interval

```text
limit 1 | choose '1d48h0m'.parseInterval() as i # Result 2: { "i": "3d" }
```
{: codeblock}

Example 3: parse a negative interval

```text
limit 1 | choose '-5m45s'.parseInterval() as i # Result 3: { "i": "-5m45s" }
```
{: codeblock}

### `parseTimestamp`
{: #parsetimestamp}

Parses a timestamp from string with an optional format specification and time zone override. Returns null when the input does not match the expected format.

```text
parseTimestamp(string: string, format: string?, tz: string?): timestamp
```
{: codeblock}

Function parameters:

* `string` (required) – the input from which the timestamp will be extracted.
* `format` (optional) – a date/time format specification for parsing timestamps. Defaults to 'auto'. The format can be any string with embedded date/time extractors, one of several shorthands, or a cascade of formats to be attempted in sequence. Here are a few samples:
   * '%Y-%m-%d' – parse date only, for example '2023-04-05'
   * '%F %H:%M:%S' – parse date and time, for example '2023-04-05 16:07:33'
   * 'iso8601' – parse a timestamp in ISO 8601 format, for example '2023-04-05T16:07:33.123Z'
   * 'timestamp_milli' – parse a timestamp in milliseconds (13 digits), for example '1680710853123'
   * '%m/%d/%Y|timestamp_second' – parse either a date or a timestamp in seconds, in that order
* `tz` (optional) – a time zone override to convert the timestamp while parsing. This parameter will override any time zone present in the input. A time zone can be extracted from the string by using an appropriate format and omitting this parameter.

Example 1: parse a date with the default format

```text
limit 1 | choose '2023-04-05'.parseTimestamp() as ts # Result 1: { "ts": 1680652800000000000 }
```
{: codeblock}

Example 2: parse a date in US format

```text
limit 1 | choose '04/05/23'.parseTimestamp('%D') as ts # Result 2: { "ts": 1680652800000000000 }
```
{: codeblock}

Example 3: parse date and time with units

```text
limit 1 | choose '2023-04-05 16h07m'.parseTimestamp('%F %Hh%Mm') as ts # Result 3: { "ts": 1680710820000000000 }
```
{: codeblock}

Example 4: parse a timestamp in seconds (10 digits)

```text
limit 1 | choose '1680710853'.parseTimestamp('timestamp_second') as ts # Result 4: { "ts": 1680710853000000000 }
```
{: codeblock}

### `roundInterval`
{: #roundinterval}

Rounds an interval to a time unit `scale`. Lesser time units will be zeroed out.

```text
roundInterval(interval: interval, scale: timeunit): interval
```
{: codeblock}

Function parameters:

* `interval` (required) – the interval to round.
* `scale` (required) – the maximium time unit of the interval to keep.

Example:

```text
limit 1 | choose 2h5m45s.roundInterval('m') as i # Result: { "i": "2h5m" }
```
{: codeblock}


### `roundTime`
{: #roundtime_interval}

Rounds a timestamp to the given interval. Useful for bucketing, for example, rounding to 1h for hourly buckets. Equivalent to `date / interval`.

```text
roundTime(date: timestamp, interval: interval): timestamp
```
{: codeblock}


Example:

```text
groupby $m.timestamp.roundTime(1h) as bucket count() as n # Results: { "bucket": "29/08/2023 15:00:00.000 pm", "n": 40653715 } { "bucket": "29/08/2023 14:00:00.000 pm", "n": 1779386 }
```
{: codeblock}

### `subtractInterval`
{: #subtractinterval}

Subtracts one interval from another. Equivalent to `addInterval(left, -right)` and `left - right`.

```text
subtractInterval(left: interval, right: interval): interval
```
{: codeblock}



### `subtractTime`
{: #subtracttime}

Subtracts an interval from a timestamp. Equivalent to `addTime(t, -i)` and `t - i`.

```text
subtractTime(t: timestamp, i: interval): timestamp
```
{: codeblock}



### `toInterval`
{: #tointerval}

Converts a number of specific time units to an interval. Works with both integer and floating point and positive and negative numbers.

```text
toInterval(number: number, timeUnit: timeunit?): interval
```
{: codeblock}

Function parameters:

* `number` (required) – the amount of time units to convert.
* `timeUnit` (optional) – Time units to convert. Defaults to nano.

Example 1: convert a floating point number

```text
limit 1 | choose 2.5.toInterval('h') as i # Result 1: { "i": "2h30m" } # Example 2: convert an integer number limit 1 | choose -9000.toInterval() as i # Result 2: { "i": "-9us" }
```
{: codeblock}

### `toUnixTime`
{: #tounixtime}

Converts timestamp to a number of specific time units since the UNIX epoch (in UTC). The UNIX epoch starts on January 1, 1970 – earlier timestamps are represented by negative numbers.

```text
toUnixTime(timestamp: timestamp, timeUnit: timeunit?): number
```
{: codeblock}


Function parameters:

* `timestamp` (required) – the timestamp to convert.
* `timeUnit` (optional) – the time units to convert to. Defaults to 'milli'.

Example:

```text
limit 1 | choose $m.timestamp.toUnixTime('hour') as hr # Result: { "hr": 470363 }
```
{: codeblock}

## Encoding / Decoding Functions
{: #encode-decode}


### `decodeBase64`
{: #decodebase64}

Decode a base-64 encoded string.

```text
decodeBase64(value: string): string
```
{: codeblock}



### `encodeBase64`
{: #encodebase64}

Encode a string into base-64.

```text
encodeBase64(value: string): string
```
{: codeblock}



## Case Expressions
{: #case-expressions}

Case expressions are special constructs in the language that allow choosing between multiple options in a readable way. They can be wherever an expression is expected.

### `case`
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

### `case_contains`
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

### `case_equals`
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

### `case_greaterthan`
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

### `case_lessthan`
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


## Aggregation Functions
{: #aggregation_functions}


### `any_value`
{: #anyvalue}

Returns any non-null expression value in the group. If expression is not defined, it defaults to the $data object.

```text
any_value(expression: any?)
```
{: codeblock}

Returns null if all expression values in the group are null.

Example:

```text
groupby $m.severity calculate any_value($d.url)
```
{: codeblock}

### `avg`
{: #avg}

Calculates the average value of a numerical expression in the group.

```text
avg(expression: number)
```
{: codeblock}

Example:

```text
groupby $m.severity calculate avg($d.duration) as average_duration
```
{: codeblock}

### `count`
{: #count-non-nnull}

Counts non-null expression values. If expression is not defined, all rows will be counted.

```text
count(expression: any?) [into <keypath>]
```
{: codeblock}

An alias can be provided to override the keypath the result will be written to.

For example, the following part of a query

```text
count() into $d.num_rows
```
{: codeblock}

will result in a single row of the following form:

```json
{ "num_rows": 7532 }
```
{: codeblock}

### `count_if`
{: #countif}

Counts non-null expression values on rows which satisfy the condition. If expression is not defined, all rows that satisfy condition will be counted.

```text
count_if(condition: bool, expression: any?)
```
{: codeblock}

Example:

```text
groupby $m.severity calculate count_if($d.duration > 500) as $d.high_duration_logs
groupby $m.severity calculate count_if($d.duration > 500, $d.company_id) as $d.high_duration_logs
```
{: codeblock}

### `distinct_count`
{: #distinctcount}

Counts non-null distinct expression values.

```text
distinct_count(expression: any)
```
{: codeblock}

Example:

```text
groupby $l.applicationname calculate distinct_count($d.username) as active_users
```
{: codeblock}

### `distinct_count_if`
{: #distinctcountif}

Counts non-null distinct expression values on rows which satisfy condition.

```text
distinct_count_if(condition: bool, expression: any)
```
{: codeblock}

Example:

```text
groupby $l.applicationname calculate distinct_count_if($m.severity == 'Error', $d.username) as users_with_errors
```
{: codeblock}

### `max`
{: #max-of-group}

Calculates the maximum value of a numerical expression in the group.

```text
max(expression: number | timestamp)
```
{: codeblock}

Example:

```text
groupby $m.severity calculate max($d.duration)
```
{: codeblock}

### `min`
{: #min-of-group}

Calculates the minimum value of a numerical expression in the group.

```text
min(expression: number | timestamp)
```
{: codeblock}

Example:

```text
groupby $m.severity calculate min($d.duration)
```
{: codeblock}

### `percentile`
{: #percentile}

Calculates the approximate n-th percentile value of a numerical expression in the group.

```text
percentile(percentile: number, expression: number, error_threshold: number?)
```
{: codeblock}

Since the percentile calculation is approximate, the accuracy may be controlled with the `error_threshold` parameter which ranges from 0 to 1 (defaults to 0.01). A lower value will result in better accuracy at the cost of longer query times.

Example:

```text
groupby $m.severity calculate percentile(0.99, $d.duration) as p99_latency
```
{: codeblock}

### `sample_stddev`
{: #samplestddev}

Computes the sample standard deviation of a numerical expression in the group.

```text
sample_stddev(expression: number)
```
{: codeblock}

Example:

```text
groupby $m.severity calculate sample_stddev($d.duration)
```
{: codeblock}

### `sample_variance`
{: #samplevariance}

Computes the variance of a numerical expression in the group.

```text
sample_variance(expression: number)
```
{: codeblock}

Example:

```text
groupby $m.severity calculate sample_variance($d.duration)
```
{: codeblock}

### `stddev`
{: #stddev}

Computes the standard deviation of a numerical expression in the group.

```text
stddev(expression: number)
```
{: codeblock}

Example:

```text
groupby $m.severity calculate stddev($d.duration)
```
{: codeblock}

### `sum`
{: #sum}

Calculates the sum of a numerical expression in the group.

```text
sum(expression: number)
```
{: codeblock}


Example:

```text
groupby $m.severity calculate sum($d.duration) as total_duration
```
{: codeblock}


### `variance`
{: #variance}

Computes the variance of a numerical expression in the group.

```text
variance(expression: number)
```
{: codeblock}

Example:

```text
groupby $m.severity calculate variance($d.duration)
```
{: codeblock}

### DataPrime Expressions in Aggregations
{: #dp-expressions}

When querying with the groupby operator, you can apply an aggregation function (such `asavg`, `max`, `sum`) to the bucket of results. This feature gives you the ability to manipulate an aggregation expression inside the expression itself, allowing you to calculate and manipulate your data simultaneously.

Example 1

This examples takes logs which have some `connect_duration` and `batch_duration` fields, and calculates the ratio between the averages of those durations, per region.

```text
# Query
source logs
  | groupby region aggregate avg(connect_duration) / avg(batch_duration)
```
{: codeblock}

Example 2

This query calculates the percentage of logs which don’t have a `kubernetes_pod_name` out of the total number of logs. The calculation is done per subsystem.

```text
# Query
source logs
| groupby $l.subsystemname aggregate
  sum(if(kubernetes.pod_name != null,1,0)) / count() as pct_without_pod_name
 ```
{: codeblock}

Example 3

This query calculates the ratio between the maximum and minimum salary per department, and provides a `Based on N Employees` string as an additional column per row.

```text
# Query
source logs
| groupby department_id aggregate
    max(salary) / min(salary) as salary_ratio
    `Based on {count()} Employees`
```
{: codeblock}

Example 4

This query calculates the ratio between error logs and info logs.

```text
source logs
| groupby $m.timestamp / 1h as hour aggregate
    count_if($m.severity == '5') / count_if($m.severity == '3') as error_to_info_ratio
```
{: codeblock}
