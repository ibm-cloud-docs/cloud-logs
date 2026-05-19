---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-19"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# About the OTel collector
{: #otel-collector}

You can deploy the OTel collector in a Kubernetes or OpenShift cluster to ingest telemetry data from multiple sources, transform the data, and export it to an {{site.data.keyword.logs_full_notm}} instance for analysis.
{: shortdesc}


## Architecture for collecting metrics in orchestrated environments
{: #otel-collector-arch-orchestrated}

The OTel collector uses a three-tier architecture to balance node-level performance with cluster-wide scalability.

The following diagram shows the high level view of the three tier architecture that is used to collect and send metrics to an {{site.data.keyword.logs_full_notm}} instance:

![Metrics collection architecture for orchestrated environments](../images/metrics.png "Metrics collection architecture for orchestrated environments"){: caption="Metrics collection architecture for orchestrated environments" caption-side="bottom"}

The **daemonSet**, known as the agent, collects metrics at the worker (node) level. Deploys a pod on each node of the cluster to collect node-local telemetry only.

A **StatefulSet**, known as the collector, acts as a cluster-wide scraping and aggregation layer.Collects metrics from the various applications, including the openshift and kubernetes metrics through kube state metrics, and OpenShift state metrics.
- Minimum 2 replicas are required for high availability.
- Provides stable pod identities that are required by the *Target Allocator*.
- Uses persistent storage for metric queues to help prevent data loss during backend outages.
- Configured with a 60-second graceful shutdown period to flush queues during rollouts.

The **target allocator** dynamically discovers and scrapes targets via Prometheus Custom Resource Definitions (CRD) and distributes the workload across the collector replicas.
- The Target Allocator is deployed per OTel Collector StatefulSet.
- Uses consistent-hashing to ensure even distribution and minimize metric "churn" during scaling.
- Minimum 2 replicas are required for high availability.
- Automatically monitors the cluster for Prometheus Operator CRDs.



## Deployment options
{: #otel-collector-deployment-orchestrated}


You can choose any of the following options to deploy the OTel collector:

### Option 1: Agent component only
{: #otel-collector-deployment-orchestrated-1}

Use this option when you want to scrape the metrics at the node level.
{: tip}

With the agent-only option,
- The agent component exports directly metrics that are collected at the node level to an {{site.data.keyword.logs_full_notm}} instance.
- The collector component is not required.
- The target allocator component is not required.

This option is configured by setting `agent.targetAllocator.enabled = true`, `collector.enabled = false` and `targetAllocator = false` in the Helm chart `values.yaml` file.


### Option 2: Collector component only
{: #otel-collector-deployment-orchestrated-2}

Use this option when you want to scrape the metrics from the application level.
{: tip}

With the collector-only option,
- The collector component scrapes all Prometheus targets through static scrape configurations.
- The agent component is not required.
- The target allocator component is not required.

This option is configured by setting `agent.targetAllocator.enabled = false`, `collector.enabled = true` and `targetAllocator = false` in the Helm chart `values.yaml` file.


the collector scrapes the metrics from the applications ( either through static scrape config or dynamically discover which metrics to scrape through service and pod monitors )

### Option 3: Collector that uses the target allocator (Recommended)
{: #otel-collector-deployment-orchestrated-3}

Use this option for cluster-level and centralized collection patterns, where scrape targets need to be discovered and distributed across replicas, or where telemetry needs centralized processing before export. This is typically useful for cluster-wide metrics, application scraping at scale, aggregation, and gateway-style deployments.
{: tip}

Select this option when you want to scrape the metrics from the application level with dynamic discovery by using PodMonitor and ServiceMonitor objects to monitor targets for a sample application.

You can enable the collector if you need:
- Trace sampling. Uses a tail-based sampling strategy.
- Cross-node metric aggregation
- Single egress point (agents → collector → IBM Cloud)
- k8s_cluster receiver metrics from the API server.

This option is configured by setting `agent.targetAllocator.enabled=false`, `collector.enabled = true` and `targetAllocator = true` in the Helm chart `values.yaml` file.

With the collector that uses the target allocator option,
- The agent component is not required.
- Prometheus Operator CRDs must be installed in the cluster.
- The target allocator is stateless and recovers quickly from restarts. Discovers targets via Prometheus Custom Resource Definitions (CRD) and distributes the workload across the collector replicas. Uses Prometheus Operator CRDs (ServiceMonitor/PodMonitor) for target discovery of applications.
- The collector component scrapes all Prometheus targets via the target allocator.


How it works? Collects metrics from OpenShift's built-in Prometheus via federation endpoint that supports bearer token authentication.

1. Creates a ServiceMonitor that scrapes a Prometheus /federate endpoint

2. Target Allocator discovers the ServiceMonitor

3. Collector scrapes using bearer token authentication

4. Metrics are forwarded to an {{site.data.keyword.logs_full_notm}} instance.



## Metrics collected in orchestrated environments
{: #otel-collector-metrics-orchestrated}

The following metrics are collected:

1. Node-local telemetry collected through the Daemonset tier:

    - **Host metrics**: CPU, memory, disk, filesystem, network, load, paging, processes, and process metrics via hostmetrics receiver accessing `/hostfs`.

    - **Kubelet metrics**: Container and pod resource usage via kubeletstats receiver.

    - **cAdvisor metrics**: Detailed container resource usage metrics: CPU, memory, network, disk I/O. These metrics are scraped from the kubelet's `/metrics/cadvisor` endpoint via prometheus receiver.

2. Cluster and application telemetry collected through the StatefulSet tier:

    - **Cluster metrics**: Nodes, deployments, pods, namespaces via k8s_cluster receiver.

    - **Application metrics**: Scraped from ServiceMonitor/PodMonitor targets via prometheus/target-allocator receiver.

    - **Collector self-monitoring metrics**: Collector's own internal metrics.

## Metrics collection interval
{: #otel-collector-metrics-collection}

Metrics are collected every 30 seconds by default.
{: note}

You can change the collection interval.

When choosing a collection interval, consider the following information:
- Use `10s`: Recommended value for high-frequency monitoring.

    More data points are collected.

    The cost is higher.

    Better option for Service Level Objectives (SLO).

- Use `30s`: Recommended value for most workloads.

- Use `60s`: Recommended value for a cost-optimized configuration.

Lower intervals increase cardinality and backend costs.
{: important}

## Requirements for orchestrated environments
{: #otel-collector-requirements-orchestrated}

Review the requirements to deploy the collector in an orchestrated environment:

-Agent (DaemonSet):

    CPU: 200m request, 1000m limit

    Memory: 512Mi request, 1Gi limit

-Collector (StatefulSet):

    Minimum 2 replicas for high availability

    CPU: 500m request per replica

    Memory: 1Gi request per replica

-Persistent storage:

    10Gi per replica (for queue persistence)

-Target Allocator (Deployment):

    Minimum 2 replicas for high availability

    CPU: 100m request

    Memory: 256Mi request
