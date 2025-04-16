---

copyright:
  years:  2024, 2025
lastupdated: "2025-04-16"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Fluent Bit plug-ins
{: #agent-plugin-support}

The {{site.data.keyword.agent}} includes and supports selected Fluent Bit plug-ins. Some plug-ins are not supported.
{: shortdesc}

The {{site.data.keyword.agent}} is built using [Fluent Bit](https://fluentbit.io/){: external}, which is an open source log processor and forwarder.  Although Fluent Bit can be built and configured to use a number of different plug-ins, the {{site.data.keyword.agent}} does not include every plug-in available for Fluent Bit.  Each plug-in falls into one of three categories:

* [Supported by IBM](#plugins-supported)
* [Available but not directly supported](#plugins-available)
* [Unavailable](#plugins-unavailable)


See [About the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about) for further information about the agent.
{: tip}

## Supported plug-ins
{: #plugins-supported}

This section lists the Fluent Bit plug-ins which are fully supported by IBM in the {{site.data.keyword.agent}}. IBM owns and maintains these plugins.

### Supported output plug-ins
{: #output-plugins-supported}

| Plug-in | Type | Description | Documentation |
| ------ | ---- | ----------- | ------------- | 
| logs-router-icl-output-plugin | output | Send log events directly to {{site.data.keyword.logs_full_notm}} | [documentation](/docs/cloud-logs?topic=cloud-logs-agent-plugin-parameters) |


## Plug-ins available but not directly supported
{: #plugins-available}

This section lists the Fluent Bit plug-ins which can be used with the {{site.data.keyword.agent}}, but for which IBM does not provide direct support.  For questions regarding these plug-ins, clients will need to refer to the appropriate section in the [official Fluent Bit documentation](https://docs.fluentbit.io/manual){: external}.

### Available input plug-ins
{: #input-plugins-available}

The {{site.data.keyword.agent}} includes the following Fluent Bit [input plug-ins](https://docs.fluentbit.io/manual/pipeline/inputs){: external}.

| Plug-in | Type | Description | Documentation |
| ------- | ---- | ----------- | ------------- |
| `collectd` | input | Receive datagrams from collectd service | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/collectd){: external} |
| `docker-events` | input | Capture docker server events | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/docker-events){: external} |
| `dummy` | input | Generate dummy events for testing | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/dummy){: external} |
| `elasticsearch` | input | Handle Elasticsearch API requests | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/elasticsearch){: external} |
| `fluentbit_metrics` | input | Collect Fluent Bit metrics | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/fluentbit-metrics){: external} |
| `forward` | input | Listen for Forward messages from Fluentd/Fluent Bit | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/forward){: external} |
| `head` | input | Read events from the head of a file | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/head){: external} |
| `http` | input | Receive events via HTTP endpoint | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/http){: external} |
| `kafka` | input | Collect messages from Apache Kafka | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/kafka){: external} |
| `kmsg` | input | Read events from Linux kernel log buffer | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/kernel-logs){: external} |
| `kubernetes_events` | input | Retrieve Kubernetes API events | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/kubernetes-events){: external} |
| `mqtt` | input | Receive messages in MQTT control packets over TCP | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/mqtt){: external} |
| `splunk` | input | Receive Splunk HTTP HEC requests | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/splunk){: external} |
| `stdin` | input | Read messages from standard input | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/standard-input){: external} |
| `syslog` | input | Receive syslog messages | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/syslog){: external} |
| `systemd` | input | Collect log messages from journald on Linux | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/systemd){: external} |
| `tail` | input | Monitor and read events from text files | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/tail){: external} |
| `tcp` | input | Receive messages over TCP interface | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/tcp){: external} |
| `udp` | input | Receive messages over UDP interface | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/udp){: external} |
| `opentelemetry` | input | Receive data in OTLP | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/opentelemetry){: external} |
| `winlog` | input | Read Windows Event Log | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/windows-event-log){: external} |
| `winevtlog` | input | Read Windows Event Log using the `winevt` API | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/windows-event-log-winevtlog){: external} |
| `windows_exporter_metrics` | input | Collect system/host metrics on Windows systems | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/windows-exporter-metrics){: external} |

### Available filter plug-ins
{: #filter-plugins-available}

The {{site.data.keyword.agent}} includes the following Fluent Bit [filter plug-ins](https://docs.fluentbit.io/manual/pipeline/filters){: external}.

| Plug-in | Type | Description | Documentation |
| ------- | ---- | ----------- | ------------- |
| `aws` | filter | Enrich events with AWS metadata for EC2 workloads | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/aws-metadata){: external} |
| `checklist` | filter | Check if value from list exists in record | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/checklist){: external} |
| `ecs` | filter | Enrich events with AWS ECS metadata | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/ecs-metadata){: external} |
| `expect` | filter | Ensure that records contain expected keys and values | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/expect){: external} |
| `geoip2` | filter | Enrich events with GeoIP2 location data | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/geoip2-filter){: external} |
| `grep` | filter | Select/exclude records based on pattern-matching | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/grep){: external} |
| `kubernetes` | filter | Enrich events with Kubernetes metadata | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/kubernetes){: external} |
| `lua` | filter | Process records using Lua scripts | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/lua){: external} |
| `parser` | filter | Parse individual fields in event records | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/parser){: external} |
| `record_modifier` | filter | Add/remove specific fields | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/record-modifier){: external} |
| `modify` | filter | Modify records based on rules and conditions | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/modify){: external} |
| `multiline` | filter | Concatenate multiple lines into a single event | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/multiline){: external} |
| `nest` | filter | Nest/elevate fields within a record | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/nest){: external} |
| `nightfall` | filter | Redact sensitive data within records | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/nightfall){: external} |
| `rewrite_tag` | filter | Modify record tags for routing | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/rewrite-tag){: external} |
| `stdout` | filter | Print records to standard output in filter stage | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/standard-output){: external} |
| `sysinfo` | filter | Add system information to records | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/sysinfo){: external} |
| `throttle` | filter | Flow-control message rate | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/throttle){: external} |
| `type_converter` | filter | Convert field types | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/type-converter){: external} |

### Available output plug-ins
{: #output-plugins-available}

The {{site.data.keyword.agent}} includes the following Fluent Bit [output plug-ins](https://docs.fluentbit.io/manual/pipeline/outputs){: external}.

| Plug-in | Type | Description | Documentation |
| ------- | ---- | ----------- | ------------- |
| `counter` | output | Count records processed | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/counter){: external} |
| `file` | output | Write records to a file | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/file){: external} |
| `flowcounter` | output | Count records and sizes | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/flowcounter){: external} |
| `forward` | output | Forward records to another Fluent Bit (or Fluentd) instance | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/forward){: external} |
| `http` | output | Send logs to an HTTP endpoint | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/http){: external} |
| `null` | output | Discard events entirely | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/null){: external} |
| `slack` | output | Send messages to a Slack channel | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/slack){: external} |
| `prometheus_exporter` | output | Expose metrics for Prometheus | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/prometheus-exporter){: external} |
| `prometheus_remote_write` | output | Submit metrics using Prometheus remote write protocol| [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/prometheus-remote-write){: external} |

## Plug-ins unavailable in {{site.data.keyword.logs_routing_full_notm}}
{: #plugins-unavailable}

This section lists plug-ins which, while part of the open source Fluent Bit project, are not available for use with the {{site.data.keyword.agent}}.

### Input plug-ins
{: #input-plugins-unavailable}

The following input plugins are not included with the {{site.data.keyword.agent}} and therefore cannot be used with it.

| Plug-in | Type | Description | Documentation |
| ------- | ---- | ----------- | ------------- |
| `cpu` | input | Collect CPU usage metrics | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/cpu-metrics){: external} |
| `disk` | input | Collect disk I/O metrics | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/disk-io-metrics){: external} |
| `exec` | input | Execute an external program to generate logs | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/exec){: external} |
| `exec_wasi` | input | Execute external WASM program to generate logs | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/exec-wasi){: external} |
| `health` | input | Check health of a TCP server | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/health){: external} |
| `mem` | input | Collect memory and swap usage metrics | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/memory-metrics){: external} |
| `netif` | input | Collect network metrics as log events | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/network-io-metrics){: external} |
| `nginx_metrics` | input | Scrape NGINX metrics | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/nginx){: external} |
| `node_exporter_metrics` | input | Collect system-level metrics | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/node-exporter-metrics){: external} |
| `podman_metrics` | input | Collect metrics from podman containers | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/podman-metrics){: external} |
| `proc` | input | Collect log-based process metrics | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/process){: external} |
| `process_exporter_metrics` | input | Collect process metrics | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/process-exporter-metrics){: external} |
| `prometheus_scrape` | input | Scrape metrics from Prometheus endpoint | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/prometheus-scrape-metrics){: external} |
| `prometheus_remote_write` | input | Ingest Prometheus remote-write payloads | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/prometheus-remote-write){: external} |
| `random` | input | Generate random values | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/random){: external} |
| `serial` | input | Collect messages/data via serial interface | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/serial-interface){: external} |
| `statsd` | input | Receive metrics via StatsD protocol | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/statsd){: external} |
| `thermal` | input | Report system temperature | [documentation](https://docs.fluentbit.io/manual/pipeline/inputs/thermal){: external} |

### Filter plug-ins
{: #filter-plugins-unavailable}

The following filter plug-ins are not included in the {{site.data.keyword.agent}} and therefore cannot be used with it.

| Plug-in | Type | Description | Documentation |
| ------ | ---- | ----------- | ------------- |
| `log_to_metrics` | filter | Generate log-based metrics | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/log_to_metrics){: external} |
| `tensorflow` | filter | Run Tensorflow machine learning tasks on log records | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/tensorflow){: external} |
| `wasm` | filter | Use Wasm programs as filters | [documentation](https://docs.fluentbit.io/manual/pipeline/filters/wasm){: external} |

### Output plugins
{: #output-plugins-unavailable}

The followng output plug-ins are not included in the {{site.data.keyword.agent}} and therefore cannot be used with it.

| Plug-in | Type | Description | Documentation |
| ------- | ---- | ----------- | ------------- |
| `cloudwatch_logs` | output | Send logs and metrics to Amazon CloudWatch | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/cloudwatch){: external} |
| `kinesis_firehose` | output | Send logs to Amazon Kinesis Firehose | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/firehose){: external} |
| `kinesis_streams` | output | Send logs to Amazon Kinesis Streams | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/kinesis){: external} |
| `s3` | output | Send data to Amazon S3 | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/s3){: external} |
| `azure_blob` | output | Send records to Azure Blob Storage | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/azure_blob){: external} |
| `azure_kusto` | output | Send logs to Azure Data Explorer (Kusto) | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/azure_kusto){: external} |
| `azure` | output | Send logs to Azure Log Analytics | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/azure){: external} |
| `azure_logs_ingestion` | output | Send logs using Azure Logs Ingestion API | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/azure_logs_ingestion){: external} |
| `datadog` | output | Send logs to Datadog | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/datadog){: external} |
| `es` | output | Send logs to Elasticsearch | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/elasticsearch){: external} |
| `gelf` | output | Send logs in Graylog Extended Log Format | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/gelf){: external} |
| `chronicle` | output | Send logs to Google Chronicle | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/chronicle){: external} |
| `bigquery` | output | Send logs to Google Cloud BigQuery | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/bigquery){: external} |
| `influxdb` | output | Send logs to an InfluxDB database | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/influxdb){: external} |
| `kafka` | output | Send logs to Apache Kafka | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/kafka){: external} |
| `kafka-rest` | output | Send logs to an Apache Kafka REST Proxy server | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/kafka-rest-proxy){: external} |
| `loki` | output | Send logs to Grafana Loki | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/loki){: external} |
| `nats` | output | Send logs to a NATS server | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/nats){: external} |
| `nrlogs` | output | Send logs to New Relic | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/new-relic){: external} |
| `oracle_log_analytics` | output | Send logs to Oracle Cloud Infrastructure Logging Analytics | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/oci-logging-analytics){: external} |
| `opensearch` | output | Send logs to Amazon OpenSearch | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/opensearch){: external} |
| `opentelemetry` | output | Send logs and data to an OpenTelemetry endpoint | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/opentelemetry){: external} |
| `pgsql` | output | Send logs to a PostgreSQL database as JSONB | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/postgresql){: external} |
| `skywalking` | output | Send logs to Apache SkyWalking | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/skywalking){: external} |
| `splunk` | output | Send logs to a Splunk HTTP Event Collector | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/splunk){: external} |
| `stackdriver` | output | Send logs to Google Cloud Stackdriver Logging | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/stackdriver){: external} |
| `syslog` | output | Deliver messages to Syslog servers | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/syslog){: external} |
| `tcp` | output | Send logs to a TCP server | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/tcp-and-tls){: external} |
| `td` | output | Send logs to Treasure Data | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/treasure-data){: external} |
| `vivo_exporter` | output | Send logs and data to Calyptia Vivo | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/vivo-exporter){: external} |
| `websocket` | output | Send logs to a WebSocket endpoint | [documentation](https://docs.fluentbit.io/manual/pipeline/outputs/websocket){: external} |

Plugins not listed above are unsupported, and their functionality is not guaranteed.
{: note}
