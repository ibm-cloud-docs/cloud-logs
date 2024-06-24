---

copyright:
  years:  2024
lastupdated: "2024-06-17"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# What happens if a metrics bucket is not configured?
{: #ts-no-metrics-bucket}
{: troubleshoot}
{: support}

An error is issued when a metrics bucket is not defined.
{: shortdesc}

You get the following error message: 
{: tsSymptoms}

```text
WARNING - Metric Bucket is Missing
To extend the retention period of your metric data beyond a few hours, it is essential to
configure a metric bucket. Without this configuration, your data may be automatically purged
after a short time frame, resulting in potential data loss.
```
{: screen}


A metrics bucket is not configured.
{: tsCauses}


[Configure a metrics bucket and associate it with your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket)
{: tsResolve}
