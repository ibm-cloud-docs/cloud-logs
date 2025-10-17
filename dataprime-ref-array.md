---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# DataPrime array functions
{: #dataprime-ref-array}

This guide provides a glossary of all available {{site.data.keyword.logs_full}} DataPrime functions for processing arrays.
{: shortdesc}

## `arrayContains`
{: #arrayContains}

Returns `true` if an array includes the specified element, or `false` if the array does not include the element. Supported element types include `string`, `bool`, `number`, `interval`, `timestamp`, `regex`, and `enum`.

This function is the inverse of [`inArray`](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-array#inArray).

```text
arrayContains(array: array<T>, element: T): bool
```
{: codeblock}

`arrayContains` can also be specified in method notation:

```text
(array: array<T>).arrayContains(element: T): bool
```
{: codeblock}

Where:

`element`
:   Is the element to check for in the array.

`array`
:   Is the array to search. The array must contain elements of the same type as `element`.

### Example
{: #arraycontains-example}

In this example you have a firewall log that records blocked IDs. 

```json
{
    "action": "BLOCK",
    "client_ip": "134.56.32.98",
    "blocked_ips": [
        "134.56.32.91",
        "134.56.32.93",
        "134.56.32.90",
        "134.56.32.105"
    ]
}
```
{: codeblock}

By checking if `client_ip` is contained in `blocked_ips` you can determine if the request was from a blocked address. Either of these notations can be used.

```text
create is_blocked_ip from arrayContains(blocked_ips, client_ip)
```
{: codeblock}

```text
create is_blocked_ip from blocked_ips.arrayContains(client_ip)
```
{: codeblock}

The result will will include a new vield (`is_blocked_ip`) with a boolean value.

```json
{
    "action": "BLOCK",
    "client_ip": "134.56.32.98",
    "blocked_ips": [
        "134.56.32.91",
        "134.56.32.93",
        "134.56.32.90",
        "134.56.32.105"
    ],
    "is_blocked_ip": false
}
```
{: codeblock}


## `inArray`
{: #inArray}

Returns `true` if the specified element exists in the array, or `false` if the element does not exist in the array. Supported element types include `string`, `bool`, `number`, `interval`, `timestamp`, `regex`, and `enum`.

This function is the inverse of [`arrayContains`](/docs/cloud-logs?topic=cloud-logs-dataprime-ref-array#arrayContains).

```text
inArray(element: T, array: array<T>): bool
```
{: codeblock}

`inArray` can also be specified in method notation:

```text
(element: T).inArray(array: array<T>): bool
```
{: codeblock}

Where:

`element`
:   Is the element to check for in the array.

`array`
:   Is the array to search. The array must contain elements of the same type as `element`.

### Example
{: #inarray-example}

In this example you have a log entry with a client IP address.

```json
{
    "client_ip": "192.168.1.105"
}
```
{: codeblock}

You want to check if the `client_ip` value exists in an array of blocked IP addresses so you can identify if a request should be blocked. Either of these notations can be used.

```text
filter inArray(client_ip, ['192.168.1.105', '192.168.1.112', '192.168.1.32'])
```
{: codeblock}

```text
filter client_ip.inArray(['192.168.1.105', '192.168.1.112', '192.168.1.32'])
```
{: codeblock}

The result will be `true` since `192.168.1.105` is included in the array.

```json
{
    "client_ip": "192.168.1.105",
    "is_blocked": true
}
```
{: codeblock}
