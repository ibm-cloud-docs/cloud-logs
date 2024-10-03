---

copyright:
  years:  2024
lastupdated: "2024-10-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Event types for alerts
{: #cl-events-for-en}


The following tables lists the event types and subtypes that {{site.data.keyword.logs_full_notm}} sends to {{site.data.keyword.en_short}}:

## Event types
{: #cl-events-for-en-types}

The following table lists the event types that {{site.data.keyword.logs_full_notm}} send to {{site.data.keyword.en_short}}:

| Event type                                  | Description |
|------------------------------------------|---------|
| `com.ibm.cloud.logs.test_event`  | Test event. |
| `com.ibm.cloud.logs.StandardImmediateAlertEvent` | Standard Immediate Alert |
| `com.ibm.cloud.logs.StandardLessThanAlertEvent` | Standard Less Than Alert |
| `com.ibm.cloud.logs.StandardMoreThanAlertEvent` | Standard More Than Alert |
| `com.ibm.cloud.logs.StandardMoreThanUsualAlertEvent` | Standard More Than Usual Alert |
| `com.ibm.cloud.logs.RatioLessThanAlertEvent` | Ratio Less Than Alert |
| `com.ibm.cloud.logs.RatioMoreThanAlertEvent` | Ratio More Than Alert |
| `com.ibm.cloud.logs.NewValueAlertEvent` | New Value Alert |
| `com.ibm.cloud.logs.UniqueCountAlertEvent` | Unique Count Alert |
| `com.ibm.cloud.logs.TimeRelativeLessThanAlertEvent` | Time Relative Less Than Alert |
| `com.ibm.cloud.logs.TimeRelativeMoreThanAlertEvent` | Time Relative More Than Alert |
| `com.ibm.cloud.logs.MetricLessThanAlertEvent` | Metric Less Than Alert |
| `com.ibm.cloud.logs.MetricMoreThanAlertEvent` | Metric More Than Alert |
| `com.ibm.cloud.logs.MetricMoreThanUsualAlertEvent` | Metric More Than Usual Alert |
| `com.ibm.cloud.logs.TracingImmediateAlertEvent` | Tracing Immediate Alert |
| `com.ibm.cloud.logs.TracingMoreThanAlertEvent` | Tracing More Than Alert |
| `com.ibm.cloud.logs.FlowAlertEvent` | Flow Alert Alert |
| `com.ibm.cloud.logs.FlowAnomaly` | Flow Anomaly event|
| `com.ibm.cloud.logs.SpikeAnomaly` | Spike Anomaly event |
| `com.ibm.cloud.logs.DailyReport` | Daily Report event|
| `com.ibm.cloud.logs.DataUsage` | Data Usage event |
{: caption="Table 1. Actions that generate event notifications" caption-side="bottom"}

## Event subtypes
{: #cl-events-for-en-subtypes}

The following table lists the {{site.data.keyword.logs_full_notm}} subtypes per event type related to alerts:

|Subtype                      | Description |
|-----------------------------|---------|
| `AlertTriggered`  | The alert is triggered. |
| `AlertResolved` | The alert is resolved. |
{: caption="Table 2. Subtypes for actions that generate event notifications" caption-side="bottom"}
