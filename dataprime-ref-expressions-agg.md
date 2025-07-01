# DataPrime aggregate expressions
{: #dataprime-ref-expressions-agg}

This guide provides a full glossary of all available DataPrime expressions that you can use for aggregation.
{: shortdesc}

## `any_value`
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

## `avg`
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

## `count`
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

## `count_if`
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

## `distinct_count`
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

## `distinct_count_if`
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

## `max`
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

## `min`
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

## `percentile`
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

## `sample_stddev`
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

## `sample_variance`
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

## `stddev`
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

## `sum`
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


## `variance`
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

## DataPrime Expressions in Aggregations
{: #dp-expressions}

When querying with the groupby operator, you can apply an aggregation function (such `asavg`, `max`, `sum`) to the bucket of results. This feature gives you the ability to manipulate an aggregation expression inside the expression itself, allowing you to calculate and manipulate your data simultaneously.

Example 1

This examples takes logs which have some `connect_duration` and `batch_duration` fields, and calculates the ratio between the averages of those durations, per region.

```text
# Query
source logs
  | groupby region calculate avg(connect_duration) / avg(batch_duration)
```
{: codeblock}

Example 2

This query calculates the percentage of logs which don’t have a `kubernetes_pod_name` out of the total number of logs. The calculation is done per subsystem.

```text
# Query
source logs
| groupby $l.subsystemname calculate
  sum(if(kubernetes.pod_name != null,1,0)) / count() as pct_without_pod_name
 ```
{: codeblock}

Example 3

This query calculates the ratio between the maximum and minimum salary per department, and provides a `Based on N Employees` string as an additional column per row.

```text
# Query
source logs
| groupby department_id calculate
    max(salary) / min(salary) as salary_ratio
    `Based on {count()} Employees`
```
{: codeblock}

Example 4

This query calculates the ratio between error logs and info logs.

```text
source logs
| groupby $m.timestamp / 1h as hour calculate
    count_if($m.severity == '5') / count_if($m.severity == '3') as error_to_info_ratio
```
{: codeblock}
