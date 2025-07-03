---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Querying data directly from the archive
{: #query-archive-data-bucket}

You can query your {{site.data.keyword.logs_full_notm}} archive by using a third-party framework with the standard Apache Parquet reader provided by the relevant framework and required schema.
{: shortdesc}

## Archive folder structure
{: #archive_folder_structure}

{{site.data.keyword.logs_full_notm}} archive data is stored in standard hive-like partitions with the following partition fields:

```text
team_id=<team-id>: IBM Cloud Logs Team ID
dt=YYYY-MM-DD: Date of the data in UTC
hr=HH: Hour of the data in UTC
```
{: codeblock}

These fields can be defined as virtual columns inside the framework and can be used as filters in a query.

Be aware of the following:

* Both `dt` and `hr` are based on the event timestamp.
* The `team_id=<team-id>` partition lets you reuse the same bucket and prefix to write data from multiple {{site.data.keyword.logs_full_notm}} teams and query them in one query.

## Fields
{: #parquet_fields}

Each Apache Parquet file has three fields with data as JSON-formatted strings:

* `src_obj__event_metadata`: A JSON object containing metadata related to the event.
* `src_obj__event_labels`: A JSON object containing the labels of the event (such as the {{site.data.keyword.logs_full_notm}} `applicationName` and `subsystemName`).
* `src_obj__user_data`: A JSON object containing actual event data.

The following is an example of `src_obj__event_metadata`:

```json
{
  "timestamp": "2022-03-28T08:50:57.946",
  "severity": "Debug",
  "priorityclass": "low",
  "logid": "some-uuid"
}
```
{: codeblock}

The following is an example of `src_obj__event_labels`:

```json
{
  "applicationname": "some-app",
  "subsystemname": "some-subsystem",
  "category": "some-category",
  "classname": "some-class",
  "methodname": "some-method",
  "computername": "some-computer",
  "threadid": "some-thread-id",
  "ipaddress": "some-ip-address"
}
```
{: codeblock}

The following is an example of `src_obj__user_data`:

```json
{
  "_container_id": "0f099482cf3b507462020e9052516554b65865fb761af8e076735312772352bf",
  "host": "ip-10-1-11-144",
  "short_message": "10.1.11.144 - - [28/Mar/2022:08:50:57 +0000] \\"GET /check HTTP/1.1\\" 200 16559 \\"-\\" \\"Consul Health Check\\" \\"-\\""
}
```
{: codeblock}





## Archive queries and parsing
{: #query_archive}


With the {{site.data.keyword.logs_full_notm}} Archive Query feature you can query logs directly from your archive using Lucene, DataPrime, and regex query syntax without counting against your daily quota, even if the data was never indexed. Yoou can store more of your data in the [{{site.data.keyword.monitoring}} and {{site.data.keyword.compliance}} pipelines](/docs/cloud-logs?topic=cloud-logs-tco-data-pipelines) and take advantage of {{site.data.keyword.logs_full_notm}} real-time analysis and remote storage search capabilities. This means you can use a shorter retention period and still be able to quickly query all your data.

Archive queries run on the archive that you set in {{site.data.keyword.logs_full_notm}} and are available for all TCO logging levels. For example, if you prioritize logs for the {{site.data.keyword.monitoring}} pipeline you can still query them without indexing the data. You can also view and query them in the LiveTail, receive real-time alerts and notification of anomalies, use parsing rules, log aggregation, and events to metrics at a lesser cost than data sent to the {{site.data.keyword.frequent-search}} pipeline.
