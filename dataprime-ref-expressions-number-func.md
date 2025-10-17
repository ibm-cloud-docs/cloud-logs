---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# DataPrime number functions
{: #dataprime-ref-number-func}

This guide provides a glossary of {{site.data.keyword.logs_full}} DataPrime number functions.
{: shortdesc}


## `abs`
{: #abs}

Returns the absolute value of number.

```text
abs(number: number): number
```
{: codeblock}



## `ceil`
{: #ceil}

Rounds the value up to the nearest integer.

```text
ceil(number: number): number
```
{: codeblock}



## `e`
{: #euler}

Returns the constant Euler’s number.

```text
e(): number
```
{: codeblock}



## `floor`
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



## `ln`
{: #ln}

Returns the natural log of number.

```text
ln(number: number): number
```
{: codeblock}



## `log`
{: #log}

Returns the log of number in base `base`.

```text
log(base: number, number: number): number
```
{: codeblock}



## `log2`
{: #log2}

Returns the log of number in base 2. Equivalent to `log(2, number)`.

```text
log2(number: number): number
```
{: codeblock}



## `max`
{: #max-number}

Returns the maximum number of all the numbers passed to the function.

```text
max(value: number, ...values: number): number
```
{: codeblock}



## `min`
{: #min}

Returns the least number of all the numbers passed to the function.

```text
min(value: number, ...values: number): number
```
{: codeblock}



## `mod`
{: #mod}

Returns the modulus (remainder) of number divided by `divisor`.

```text
mod(number: number, divisor: number): number
```
{: codeblock}



## `pi`
{: #pi}

Returns the constant Pi.

```text
pi(): number
```
{: codeblock}



## `power`
{: #power}

Returns `number`^`exponent`.

```text
power(number: number, exponent: number): number
```
{: codeblock}



## `random`
{: #random}

Returns a pseudo-random value in the range 0.0 <= x < 1.0.

```text
random(): number
```
{: codeblock}



## `randomInt`
{: #randomint}

Returns a pseudo-random integer number between 0 and n (exclusive).

```text
randomInt(upperBound: number): number
```
{: codeblock}


## `round`
{: #round}

Round `number` to `digits` decimal places.

```text
round(number: number, digits: number?): number
```
{: codeblock}



## `sqrt`
{: #sqrt}

Returns square root of a number.

```text
sqrt(number: number): number
```
{: codeblock}



## `toBase`
{: #tobase}

Returns the base-radix representation of `number`.

```tex
toBase(number: number, radix: number): string
```
{: codeblock}
