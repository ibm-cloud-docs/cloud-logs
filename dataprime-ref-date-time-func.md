---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# DataPrime date / time functions
{: #dataprime-ref-date-time-func}

This guide provides a glossary of available {{site.data.keyword.logs_full}} DataPrime functions for processing timestamps, intervals and other time-related constructs.
{: shortdesc}



## Time Units
{: #time-units}

Many date/time functions accept a time unit argument to modify their behavior. DataPrime supports time units from nanoseconds to days. They are represented as literal strings of the time unit name in either long or short notation:

* long notation: `day`, `hour`, `minute`, `second`, `milli`, `micro`, `nano`

* short notation: `d`, `h`, `m`, `s`, `ms`, `us`, `ns`

## Time Zones
{: #time-zones}

DataPrime timestamps are always stored in the UTC time zone, but some date/time functions accept a time zone argument to modify their behavior. Time zone arguments are strings that specify a time zone offset, shorthand or identifier:

* time zone offset in hours (for example, '+01' or '-02')
* time zone offset in hours and minutes (for example, '+0130' or '-0230')
* time zone offset in hours and minutes with separator (for example '+01:30' or '-02:30')
* time zone shorthand (for example, 'UTC', 'GMT', 'EST', and so on)
* time zone identifier (for example, 'Asia/Yerevan', 'Europe/Zurich', 'America/Winnipeg', and so on)

## `addInterval`
{: #addinterval}

Adds two intervals together. Also works with negative intervals. Equivalent to `left + right`.

```text
addInterval(left: interval, right: interval): interval
```
{: codeblock}


## `addTime`
{: #addtime}

Adds an interval to a timestamp. Also works with negative intervals. Equivalent to `t + i`.

```text
addTime(t: timestamp, i: interval): timestamp
```
{: codeblock}



## `diffTime`
{: #difftime}

Calculates the duration between two timestamps. Positive if `to` > `from`, negative if `to` < `from`. Equivalent to `to - from`.

```text
diffTime(to: timestamp, from: timestamp): interval
```
{: codeblock}



## `extractTime`
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



## `formatInterval`
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

## `formatTimestamp`
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

## `fromUnixTime`
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

## `multiplyInterval`
{: #multiplyinterval}

Multiplies an interval by a numeric factor. Works both with integer and fractional numbers. Equivalent to `i * factor`.

```text
multiplyInterval(i: interval, factor: number): interval
```
{: codeblock}



## `now`
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

## `parseInterval`
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

## `parseTimestamp`
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

## `roundInterval`
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


## `roundTime`
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

## `subtractInterval`
{: #subtractinterval}

Subtracts one interval from another. Equivalent to `addInterval(left, -right)` and `left - right`.

```text
subtractInterval(left: interval, right: interval): interval
```
{: codeblock}



## `subtractTime`
{: #subtracttime}

Subtracts an interval from a timestamp. Equivalent to `addTime(t, -i)` and `t - i`.

```text
subtractTime(t: timestamp, i: interval): timestamp
```
{: codeblock}



## `toInterval`
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

## `toUnixTime`
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
