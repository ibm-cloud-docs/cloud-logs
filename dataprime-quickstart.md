---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-28"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# DataPrime examples
{: #dataprime-qs}

DataPrime can be used to query and transform log data in {{site.data.keyword.logs_full_notm}}. This topic is intended to let you get started quickly with DataPrime by providing examples of various types of queries and data transformation.
{: shortdesc}

DataPrime supports data and helper types, expressions, and operators.

## Data and helper types
{: #dp_qs_data_helper}

DataPrime supports the following data types:

* boolean: >, <, =, true or false
* number/num: 42
* string: “foo”
* timestamp: 10-10-2021:11:11

DataPrime also supports several helper types, used as arguments for functions or operators, including:

* Interval: duration of time
* Regexp: standard regular expressions


## Expressions
{: #dp-qs-expressions}

Expressions consist of literals, functions, methods, operators, cast, and groupings that return data.

* literals: 42
* functions: length($.foo)
* methods: $d.foo.length()
   This is an alternative syntax for functions
* operator expressions: 1 + $d.foo
* cast: $d.foo:string
* groupings: (…)


## Operators
{: #dp-qs-operators}

Use operators as commands that transform unstructured streams of JSON data and creates a new stream for a specified time period. Examples include: `filter`, `extract`, `sortby`, `groupby`, `orderby`, `find`, and `choose`.

For more information about DataPrime operators, see the [DataPrime operators](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-operators).

## Formatting queries
{: #dp-qs-format}

Queries are formatted as follows:

```text
source logs | operator1 ... | operator2 ... | operator3 | ...
```
{: codeblock}

Any whitespace between operators is ignored. Queries can be written on multiple lines:

```text
source logs
  | operator1 ....
  | operator2 ....
  | operator3 ....
```
{: codeblock}

## Examples of frequently used operators
{: #dp-qs-examples}

The examples in this section use the following log records as input.

```text
{ region: "us-east-1", az: "us-east-1a", duration_ms: 231, result: 'success' }
{ region: "us-east-1", az: "us-east-1b", duration_ms: 2222, result: 'failure' }
{ region: "eu-west-1", az: "eu-west-1a", duration_ms: 501, result: 'success' }
{ region: "eu-west-2", az: "eu-west-2a", duration_ms: 23, result: 'success' }
```
{: codeblock}

### Filter examples
{: #dp-qs-filter}

Get only the logs which have a result of `success`:

```text
source logs
| filter result == 'success'

# Result - Full raw logs
```
{: codeblock}

Get only the logs which have a result of `failure` in the `eu-west-1` region:

```text
# Option 1

source logs
| filter result == 'failure' && region == 'eu-west-1'

# Option 2
source logs
| filter result == 'failure'
| filter region == 'eu-west-1'

# Result - Full raw logs
```
{: codeblock}

Get only the logs which have a region that starts with `eu-` :

```text
source logs
| filter region.startsWith('eu-')

# Result - Full raw logs
```
{: codeblock}

Get only the logs which have a duration greater than 2 seconds:

```text
source logs
| filter duration_ms / 1000 > 2

# Result - Full raw logs
```
{: codeblock}

Get all the logs, except the ones which are in the `ap-southeast-1` region:

```text
# Option 1
source logs
| filter region != 'ap-southeast-1'

# Option 2
source logs
| filter !(region == 'ap-southeast-1')

# Option 3
source logs
| block region == 'ap-southeast-1'

# Result - Full raw logs
```
{: codeblock}

Get 10 success logs which have a duration larggreaterer than 2 seconds:

```text
source logs
| filter result == 'success' && duration_ms / 1000 > 2
| limit 10

# Result - Full raw logs
```
{: codeblock}

Order the success logs by descending duration returning the highest duration 10 logs:

```text
source logs
| filter result == 'success'
| orderby duration_ms desc
| limit 10

# Result - Full raw logs
```
{: codeblock}

Do a free-text search on the `msg` field, returning only the logs which have the word `started` in them. Combine the free-text search with the filter to stream to stdout:

```text
# Query 1 -  Using the find operator for finding the text in msg, and then filtering using the filter operator

source logs
| find 'started' in msg
| filter stream == 'stdout'

# Results 1 - Full raw logs

# Query 2 - Using the ~ predicate and combining the free-text search and the filter into one expression that is passed to filter
source logs
| msg ~ 'started' && filter stream == 'stdout'

# Result - Full raw logs
```
{: codeblock}

Do a wild-search of text inside the entire log:

```text
# Option 1 - Using wildfind operator

source logs
| wildfind 'mycompany'

# Option 2 - Inside an expression

source logs
| filter $d ~~ 'mycompany'

# Result - Full raw logs
```
{: codeblock}

Use a full Lucene query to filter results:

```text
source logs
| lucene 'region:"us-east-1" AND "mycompany"'
```
{: codeblock}

Convert the data type of a key. Then get the logs whose version field contains a value greater than 32.

Consider this input data:

```text
{ "version" : "12", ... }
{ "version": "17", ... }
{ "version": "65", ... }
```
{: codeblock}

```text
# Option 1 - By casting

source logs
| filter version:number > 32

# Option 2 - Using convert operator

source logs
| convert version:number
| filter version > 32
```
{: codeblock}

Get the logs with a result of `success`, but select only result and duration fields for the output:

```text
# Option 1 - Using the choose operator

source logs
| filter result == 'success'
| choose result, duration_ms

# Option 2 - Using the select operator, which is just an alias for choose

source logs
| filter result == 'success'
| select result, duration_ms

# Result - Only result and duration keys will remain in each event
```
{: codeblock}

### Choose examples
{: #dp-qs-choose}

Get success logs, but choose only result and duration fields for the output.

```text
# Option 1 - Using the choose operator

source logs
| filter result == 'success'
| choose result, duration_ms

# Result - Only result and duration keys will remain in each event
```
{: codeblock}

Construct a new object using `choose`. The output fields are:

* `Outcome` contains the value of the result field from the original log.
* `Duration_seconds` contains the original `duration_ms` divided by 1000 to convert it to seconds.
* A new field called `meaning_of_life` which contains the value 42.

```text
source logs
| choose result as outcome, duration_ms / 1000 as duration_seconds, 42 as meaning_of_life

# Result - Notice the key names have been changed according to the "as X" parts
{ "outcome": "success", "duration_seconds": 2.54, "meaning_of_life": 42 }
{ "outcome": "failure", "duration_seconds": 0.233, "meaning_of_life": 42 }
```
{: codeblock}

### Count/Countby examples
{: #dp-qs-count}

Count all the success logs:

```text
source logs
| filter result == 'success'
| count

# Result - Total number of logs after filtering
```
{: codeblock}

Count logs, grouped by success/failure:

```text
source logs
| countby result

# Result - Number of logs per result value
{ "result": "success", "_count": 847 }
{ "result": "failure", "_count": 22 }
```
{: codeblock}

Count logs, grouped by success or failure in a region region, with the results in a new field named request_count:

```text
source logs
| countby region,result into request_count

# Result - Notice that the count keyname is set to request_count because of "into request_count"
{ "region": "eu-west-1", "result": "success", "request_count": 287 }
{ "region": "eu-west-1", "result": "failure", "request_count": 2 }
{ "region": "eu-west-2", "result": "success", "request_count": 2000 }
{ "region": "eu-west-3", "result": "success", "request_count": 54 }
{ "region": "eu-west-3", "result": "failure", "request_count": 2 }
```
{: codeblock}

Count events in each region, and return the 3 regions with the greatest results:

```text
source logs
| top 3 region by count()

# Result - 3 rows, each containing a region and a count of logs
```
{: codeblock}

Average the duration in seconds for each region, and return the lowest 3 regions:

```text
source logs
| bottom 3 regions by avg(duration_ms)

# Result - 3 rows, each containing a region and an average duration
```
{: codeblock}

### Groupby examples
{: #dp-gs-groupby}

Get the average and maximum durations for successes or failures:

```text
# Option 1 - Output keypaths are named automatically

source logs
| groupby result calc avg(duration_ms),max(duration_ms)

# Result 1
{ "result": "success", "_avg": 23.4, "_max": 287 }
{ "result": "failure", "_avg": 980.1, "_max": 1000.2 }

# Option 2 - Using "as X" to name the output keypaths

source logs
| groupby result calc avg(duration_ms) as avg_duration,max(duration_ms) as max_duration

# Result 2
{ "result": "success", "average_duration": 23.4, "max_duration": 287 }
{ "result": "failure", "average_duration": 980.1, "max_duration": 1000.2 }
```
{: codeblock}

When querying with the groupby operator, you can apply an aggregation function (such as `avg`, `max`, `sum`) to the bucket of results. This feature gives you the ability to manipulate an aggregation expression inside the expression itself, letting you to calculate and manipulate your data simultaneously. DataPrime aggregation functions can be found in the [DataPrime aggregation expressions](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-expressions-agg).

### Distinct examples
{: #dp-qs-distinct}

Get distinct regions from the data, grouping the logs by region name without aggregations.

Consider the following input:

```text
# Input Examples:
{ "region": "us-east-1", ... }
{ "region": "us-east-1", ... }
{ "region": "eu-west-1", ... }
```
{: codeblock}

```text
# Query 1 - Get distinct regions from the data

source logs
| distinct region

# Results 1 - distinct region names
{ "region": "us-east-1" }
{ "region": "eu-west-1" }
```
{: codeblock}

### Enrich examples
{: #dp-qs-enrich}

Enrich and filter your logs using additional context from a lookup table. For example, enrich user activity logs with the user’s department and then retrieve logs of all users in the Finance department.

First you need to upload the lookup table. In the {{site.data.keyword.logs_full_notm}} UI, click the **Data flow** icon ![Data Flow icon](/images/flow--data.svg "Data Flow") > **Data Enrichmrent**. Add a custom enrichment.

There are two possible ways to enrich your logs:

* Select log key to look up for a key value and enrich the logs automatically during ingestion. The logs are saved with the enriched fields. The advantages of this mode are:

   * Logs are automatically enriched.

   * The logs include the enrichment data, which makes it easier to consume everywhere. Consumption can include by any query and also by third-party products that read the logs from the bucket.

* Use the DataPrime enrich query to look up a value in the his table and enrich the log dynamically for the purpose of the query. The advantages of this mode are:

   * You can enrich old log data already ingested into {{site.data.keyword.logs_full_notm}}.
   * The enrichment does not increase the size of the stored logs, since the enrichment is done dynamically, and used only for the query results.

```text
enrich <value_to_lookup> into <enriched_key> using <lookup_table>
```
{: coeblock}

The `<value_to_lookup>` is the name of a log key or the actual value that will be looked up in the custom enrichment `<lookup_table>` and a key called `<enriched_key>` will be added to the log with all table columns as sub-keys. If the `<value_to_lookup>` is not found in the `<lookup_table>`, the `<enriched_key>` will still be added but with “null” values to maintain the same structure for all result logs. You can then filter the results using the DataPrime capabilities, such as filtering logs by specific value in the enriched field.

For example, using the following original log:

```text
{
  "userid": "111",
  ...
}
```
{: codeblock}

And, using the Custom Enrichment lookup table called “my_users”:

```text
ID	Name	Department
111	John	Finance
222	Emily	IT
```
{: codeblock}

Running the following query:

```text
enrich $d.userid into $d.user_enriched using my_users
```
{: codeblock}

Returns the following enriched log:

```text
{
  "userid": "111",
  "user_enriched": {
    "ID: "111",
    "Name": "John",
    "Department": "Finance"
  },
  ...
}
```
{: codeblock}

Consider the following when using `enrich`:

* Run the DataPrime query source `<lookup_table>` to view the enrichment table.

* If the original log already contains the enriched key:

   * If `<value_to_lookup>` exists in the `<lookup_table>`, the sub-keys will be updated with the new value.

   * If the `<value_to_lookup>` does not exist, the current value will be retained.

   * Any other sub-keys which are not columns in the <lookup_table> will retain their existing values.

* All values in the <lookup_table> are considered to be strings. This means that:

   * The `<value_to_lookup>` must be in a string format.

   * All values are enriched in a string format. You can then convert the values to your preferred format (for example, JSON, timestamp) using the appropriate functions.


### Extract example
{: #dp-qs-extract}

`Extract` lets you take semi-structured text and extract meaningful data out of it. There are multiple methods to extract this data:

* regexp – Extract using regular expression capture-groups
* jsonobject – Take a stringified JSON and extract it to a real object
* kv – Extract key=value pairs from a string

The extracted values can also be converted to their real data type as part of the extraction. This is done by adding the datatypes clause that contains the required conversions. This is the same syntax as the convert operator.

Extract information from a text field using a regular expression:

This example uses this input data:

```text
{ "msg": "... Query_time: 2.32 Lock_time: 0.05487 ..." }
{ "msg": "... Query_time: 0.1222 Lock_time: 0.0002 ..." }
...
```
{: codeblock}

```text
# Query 1

source logs
// Filter the relevant logs using lucene
| lucene '"Query_time:"'
// Extract duration and lock_time strings from the msg field
| extract msg into stats using regexp(
  /# Query_time: (?<duration>.*?) Lock_time: (?<lock_time>.*?) /)
// Choose to leave only the stats object that the extraction has created
| choose stats

# Results 1 - Output contains strings
{ "stats": { "duration": "0.08273" , "lock_time": "0.00121" } }
{ "stats": { "duration": "0.12" , "lock_time": "0.001" } }
{ "stats": { "duration": "3.121" , "lock_time": "0.83322" } }
...

# Query 2 - Added datatypes clause, so the extracted values will be numbers instead of strings

source logs
| lucene '"Query_time:"'
| extract msg into stats using regexp(
  /# Query_time: (?<duration>.*?) Lock_time: (?<lock_time>.*?) /)
  datatypes duration:number,lock_time:number
| choose stats

# Results 1 - Output contains real numbers and not strings (see previous example)
{ "stats": { "duration": 0.08273 , "lock_time": 0.00121 } }
{ "stats": { "duration": 0.12 , "lock_time": 0.001 } }
{ "stats": { "duration": 3.121 , "lock_time": 0.83322 } }
...

# Query 3 - Use the extracted values in a later operator, in this case a filter

source logs
| lucene '"Query_time:"'
| extract msg into stats using regexp(
  /# Query_time: (?<duration>.*?) Lock_time: (?<lock_time>.*?) /)
  datatypes duration:number,lock_time:number
| choose stats
// Filter for only the logs which contain a lock_time which is greater than 0.5
| filter stats.lock_time > 0.5

# Results 1 - Output contains real numbers
{ "stats": { "duration": 3.121 , "lock_time": 0.83322 } }
...
```
{: codeblock}

Extract a JSON object stored in a string:

This example uses this input data:

```text
{"my_json": "{\\"x\\": 100, \\"y\\": 200, \\"z\\": {\\"a\\": 300}}" , "some_value": 1}
{"my_json": "{\\"x\\": 400, \\"y\\": 500, \\"z\\": {\\"a\\": 600}}" , "some_value": 2}
...
```
{: codeblock}

```text
# Query 1

source logs
| **extract my_json into my_data using jsonobject()**

# Results 1
{
  "my_json": "..."
  "my_data": {
    "x": 100,
    "y": 200,
    "z": 300
  }
  "some_value": 1
}
{
  "my_json": "..."
  "my_data": {
    "x": 400,
    "y": 500,
    "z": 600
  }
  "some_value": 2
}

# Query 2 - Additional filtering on the resulting object

source logs
| extract my_json into my_data using jsonobject()
| **filter my_data.x = 100**

# Results 2 - Only the object containing x=100 is returned
Extract key=value data from a string. Notice that the kv extraction honors quoted values.
```
{: codeblock}

This example uses this input data:

```text
{ "log": "country=Japan city=\\"Tokyo\\"" , ... }
{ "log": "country=Israel city=\\"Tel Aviv\\"" , ... }
...
```
{: codeblock}

```text
# Query 1

source logs
| extract log into my_data using kv()

# Results 1
{
  "log": "..."
  "my_data": {
    "country": "Japan"
    "city": "tokyo"
  }
  ...
}
{
  "log": "..."
  "my_data": {
    "country": "Israel"
    "city": "Tel Aviv"
  }
  ...
}
```
{: codeblock}

This example uses this input data:

```text
# Example Data for Query 2 - Key/Value delimiter is ":" and not "="
{ "log": "country:Japan city:\\"Tokyo\\"" , ... }
{ "log": "country:Israel city:\\"Tel Aviv\\"" , ... }
...
```
{: codeblock}

```text
# Query 2

source logs
| extract log into my_data using kv(':')

# Results 2 - Same results as query 1
```
{: codeblock}

### Orderby/Sortby examples
{: #dp-qs-orderby}

Order the success logs by descending duration returning the highest-duration 10 logs:

```text
source logs
| filter result == 'success'
| orderby duration_ms desc
| limit 10

# Result - Full raw logs
```
{: codeblock}

Numerically order a string field which contains numbers:

This example uses this input data:

```text
{ "error_code": "23" }
{ "error_code": "12" }
{ "error_code": "4" }
{ "error_code": "1" }
```
{: codeblock}

```text
# Query 1

source logs
| orderby error_code:number

# Results 1 - Ordered by numeric value
{ "error_code": "1" }
{ "error_code": "4" }
{ "error_code": "12" }
{ "error_code": "23" }

# Query 2 - By using the convert operator

source logs
| convert error_code:number
| orderby error_code

# Results 2 - Same results
```
{: codeblock}

Order multiple fields by alphabetical order.

Ordering is case-sensitive; A-Z will be ordered before a-z.
{: note}

This example uses this input data:

```text
{ "last_name": "smith" , "first_name": "jane" }
{ "last_name": "doe", "first_name": "john" }
...

```
{: codeblock}

```text
# Query
source logs
| orderby last_name,first_name
```
{: codeblock}

The following is the same example but with case-insensitive ordering:

```text
source logs
| orderby toLowerCase(last_name),toLowerCase(first_name)
```
{: codeblock}

### Create example
{: #dp-qs-orderby-keypath}

Create a new keypath value.

This example uses this input data:

```text
{ "country": "Japan", "city": "Tokyo" }
{ "country": "Israel", "city": "Jerusalem" }
...
```
{: codeblock}

```text
# Query 1

source logs
| create default_temperature from 32.5

# Results 1 - Each log contains the new field, with the same value
{ "country": "Japan", "city": "Tokyo", "default_temperature": 32.5 }
{ "country": "Israel", "city": "Jerusalem", "default_temperature": 32.5 }
...

# Query 2 - Create a new field which contains the first three letters of the country, converted to uppercase

source logs
| create country_initials from toUpperCase(substr(country,1,3))

# Results 2
{ "country": "Japan", "city": "Tokyo", "country_initials": "JAP" }
{ "country": "Israel", "city": "Jerusalem", "country_initials": "ISR" }
```
{: codeblock}

This example uses this input data:

```text
{ ... , "temp_in_fahrenheit": 87.2 }
{ ... , "temp_in_fahrenheit": 32 }
...
```
{: codeblock}

```text
source logs
| create temp_in_celcius from (temp_in_fahrenheit - 32) * 5 / 9

# Results 3
{ ... , "temp_in_fahrenheit": 87.2, "temp_in_celcius": 30.66666 }
{ ... , "temp_in_fahrenheit": 32, "temp_in_celcius": 0.0 }
...
```
{: codeblock}

Create a new field containing `<country>`/`<city>` as a string. Uses string-interpolation syntax

```text
source logs
| create country_and_city from `{country}/{city}`

# Results 3
{ "country": "Japan", "city": "Tokyo", "country_and_city": "Japan/Tokyo" }
{ "country": "Israel", "city": "Jerusalem", "country_and_city": "Israel/Jerusalem" }
```
{: codeblock}

### Move example
{: #dp-qs-move}

This operator can be used to move a source keypath to a target keypath, including entire subtrees. It can also be used to rename a keypath.

For nested source keypaths, only the actual key is move, The target keypath is merged with any other objects or keys which already exist in the data.
{: note}

When moving an entire subtree, the target keypath will serve as the root of the new subtree.

Move a key to a target location.

This example uses this input data:

```text
{ "query_id": "AAAA", "stats": { "total_duration": 23.3 , "total_rows": 500 }}
...
```
{: codeblock}

```text
# Query 1 - Rename a keypath

source logs
| move query_id to query_identifier

# Results 1 - Keypath renamed
{ "query_identifier": "AAAA", "stats": { "total_duration": 23.3 , "total_rows": 500 } }
...

# Query 2 - Move a key to an existing subtree

source logs
| move query_id to stats.query_id

# Results 2 - query_id moved into "stats"
{ "stats": { "total_duration": 23.3 , "total_rows": 500, "query_id": "AAAA" } }
...
```
{: codeblock}

Move a subtree to another location.

```text
# Query 1 - Rename subtree

source logs
| move stats to execution_data

# Results 1 - Rename subtree
{ "query_identifier": "AAAA", "execution_data": { "total_duration": 23.3 , "total_rows": 500 } }
...

# Query 2 - Move subtree to root

source logs
| move stats to $d

# Results 2
{ "query_id": "AAAA", "total_duration": 23.3 , "total_rows": 500 }
...
```
{: codeblock}

This example uses this input data:

```text
{ "request": { "id": "1000" } , "user": { "name": "james", "id": 50 } }
...
```
{: codeblock}

```text
# Move subtree to another subtree

source logs
| move user to request.user_info

# Results - Entire user subtree moved into request.user_info
{ "request": { "id": "1000", "user_info": { "name": "james", "id": 50 } } }
...
```
{: codeblock}

### Replace examples
{: #dp-qs-replace}

Replace the value in an existing keypath:

This example uses this input data:

```text
{ "user": { "id": "1000" , "name": "James", "email": "james@mycompany.com" } }
{ "user": { "id": "2000" , "name": "John", "email": "john@mycompany.com" } }
...
```
{: codeblock}

```text
# Example 1

source logs
| replace user.name with 'anyone'

# Results 1
{ "user": { "id": "1000" , "name": "anyone", "email": "james@mycompany.com" } }
{ "user": { "id": "2000" , "name": "anyone", "email": "john@mycompany.com" } }
...

# Example 2

source logs
| replace user.name with user.email

# Results 2
{ "user": { "id": "1000" , "name": "james@mycompany.com", "email": "james@mycompany.com" } }
{ "user": { "id": "2000" , "name": "john@mycompany.com", "email": "john@mycompany.com" } }

# Example 3

source logs
| replace user.name with `UserName={user.id}`

# Results 3
{ "user": { "id": "1000" , "name": "UserName=1000", "email": "james@mycompany.com" } }
{ "user": { "id": "2000" , "name": "UserName=2000", "email": "john@mycompany.com" } }
...
```
{: codeblock}

### Remove examples
{: #dp-qs-remove}

This example uses this input data:

```text
{
  "stats": {
    "duration_ms": 2.34,
    "rows_scanned": 501,
    "message": "Operation has taken 2.34 seconds"
  },
  "some_value": 1000
}
...
```
{: codeblock}

```text
# Query 1 - Remove the message keypath

source logs
| remove stats.message
# Results 1
{
  "stats": {
    "duration_ms": 2.34,
    "rows_scanned": 501
  },
  "some_value": 1000
}
...

# Query 2 - Remove the entire stats subtree

source logs
| remove stats

# Results 2
{
  "some_value": 1000
}
...
```
{: codeblock}

### Redact examples
{: #dp-qs-redact}


This example uses this input data:

```text
{ "serverIp": "ip-172-30-20-12.eu-west-1.compute.internal", ... }
{ "serverIp": "ip-172-82-121-1.eu-west-2.compute.internal", ... }
{ "serverIp": "ip-172-99-72-187.us-east-1.compute.internal", ... }
...
```
{: codeblock}

```text
# Query 1 - Redact all parts containing the string '.computer.internal'

source logs
| redact serverIp matching 'compute.internal' to ''

# Results 1
{ "serverIp": "ip-172-30-20-12.eu-west-1", ... }
{ "serverIp": "ip-172-82-121-1.eu-west-2", ... }
{ "serverIp": "ip-172-99-72-187.us-east-1", ... }

# Query 2 - Redact all digits before aggregation using regexp

source logs
| redact serverIp matching /[0-9]+/ to 'X'
| countby serverIp

# Results 2
{ "serverIp": "ip-X-X-X-X.eu-west-X.compute.internal", "_count": 2323 }
{ "serverIp": "ip-X-X-X-X.us-east-X.compute.internal", "_count": 827 }
...
```
{: codeblock}

### Source examples
{: #dp-qs-source}

Set the data source that your DataPrime query is based on.

The syntax is:

```text
source <data_store>
```
{: codeblock}

Where `<data_store>` can be:

* `logs`
* `spans`
* The name of a custom enrichment. In this case, the command will display the custom enrichment table.

```text
source logs
```
{: codeblock}
