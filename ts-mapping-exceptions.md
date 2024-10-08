---

copyright:
  years:  2024
lastupdated: "2024-09-23"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why am I not seeing results from my searches?
{: #ts-mapping-exceptions}
{: troubleshoot}
{: support}

When searching in {{site.data.keyword.logs_full}} I am not seeing the expected results returned. I know the fields I am searching for in my logs exist, but {{site.data.keyword.logs_full_notm}} doesn't seem to find them with my searches.
{: shortdesc}

Searching for field values does not return expected results.
{: tsSymptoms}

The problem is often related to a mapping exception.
{: tsCauses}


{{_include-segments/mapping-exception-whatis.md}}

You can determine if there are mapping exceptions using the {{site.data.keyword.logs_full_notm}} UI.
{: tsResolve}


{{_include-segments/mapping-exception-fix.md}}
