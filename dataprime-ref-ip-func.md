---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}} 

# DataPrime IP functions
{: #dataprime-ref-ip-func}

This guide provides a glossary of {{site.data.keyword.logs_full}} DataPrime IP functions.
{: shortdesc}


## `ipInSubnet`
{: #ipinsubnet}

Returns true if IP is in the subnet of `ipPrefix`.

```text
ipInSubnet(ip: string, ipPrefix: string): bool
```
{: codeblock}



## `ipPrefix`
{: #ipprefix}

Returns the IP prefix of a given IP address with `subnetSize` bits (for example, 192.128.0.0/9).

```text
ipPrefix(ip: string, subnetSize: number): string
```
{: codeblock}
