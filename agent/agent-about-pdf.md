---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router


---

{{site.data.keyword.attribute-definition-list}}


# About the {{site.data.keyword.logs_routing_full_notm}} agent
{: #agent-about-pdf}

The {{site.data.keyword.logs_routing_full_notm}} agent is based on the Fluent Bit open-source agent which is used to collect and process log data. You can deploy the IBM Cloud Logs Routing agent in supported environments and manage data from various sources and formats.
{: shortdesc}

The agent collects and sends infrastructure and application logs to the {{site.data.keyword.logs_routing_full_notm}} service.



## {{site.data.keyword.logs_routing_full_notm}} agent for orchestrated environments
{: #agent-about-orchestrated-pdf}

You can deploy the {{site.data.keyword.logs_routing_full_notm}} agent on a {{site.data.keyword.openshiftlong_notm}} or {{site.data.keyword.containerlong_notm}} cluster.

You can deploy the agent on clusters that you run on-prem, in {{site.data.keyword.cloud_notm}}, or in a different cloud.

The {{site.data.keyword.logs_routing_full_notm}} agent is a daemon set that is designed to have one pod running on each node of a cluster. Each pod will collect relevant logs for the node its running on. The {{site.data.keyword.logs_routing_full_notm}} agent will then forward those logs to the {{site.data.keyword.logs_routing_full_notm}} service.

By default, the {{site.data.keyword.logs_routing_full_notm}} agent monitors and collects log data from files matching the specified path pattern in `/var/log/containers/`, excluding logs from files matching the exclusion pattern. The refresh interval is set to 10 seconds. You can change these values and more in the config map `logger-agent-config`.

You can deploy the agent in the following platforms:
- Kubernetes clusters
- OpenShift clusters

## {{site.data.keyword.logs_routing_full_notm}} agent for non-orchestarted environments
{: #agent-about-std-pdf}

You can deploy the {{site.data.keyword.logs_routing_full_notm}} agent in Linux environments.

The following platforms are supported:

- RHEL 8
- RHEL 9
- Ubuntu 20
- Ubuntu 22
- Debian 11
- Debian 12

## Supported formats
{: #agent-about-formats-pdf}


The agent supports the following input formats:

* JSON
* apache
* apache2
* apache_error
* nginx
* docker (JSON with the docker-specific timestamp format)
* cri
* syslog
