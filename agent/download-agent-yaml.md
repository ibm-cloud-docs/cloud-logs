---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}

# Downloading the {{site.data.keyword.logs_routing_full_notm}} agent YAML configuration file
{: #download-iclr-agent-configuration-file}

Customizing the agent configuration requires that you download the configuration file based on your cluster type and make changes to it. You then deploy the modified configuration.
{: shortdesc}

For a {{site.data.keyword.openshiftlong_notm}} cluster:

```sh
curl -sSL https://ibm.biz/iclr-agent-yaml -o logger-agent.yaml
```
{: pre}

For an {{site.data.keyword.containerlong_notm}} cluster:

```sh
curl -sSL https://ibm.biz/iclr-agent-iks-yaml -o logger-agent-iks.yaml
```
{: pre}
