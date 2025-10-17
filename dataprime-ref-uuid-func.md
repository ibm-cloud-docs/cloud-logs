---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# DataPrime UUID functions
{: #dataprime-ref-uuid-func}

This guide provides a glossary of {{site.data.keyword.logs_full}} DataPrime UUID functions.
{: shortdesc}


## `isUuid`
{: #isuuid}

Returns true if UUID is valid.

```text
isUuid(uuid: string): bool
```
{: codeblock}



## `randomUuid`
{: #randomuuid}

Returns a random UUIDv4.

```text
randomUuid(): string
```
{: codeblock}
