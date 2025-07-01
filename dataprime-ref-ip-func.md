# DataPrime IP functions
{: #dataprime-ref-ip-func}

This guide provides a full glossary of all available DataPrime IP functions.
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
