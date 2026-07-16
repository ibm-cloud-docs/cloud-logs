---

copyright:
  years:  2024, 2026
lastupdated: "2026-07-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Supported agent versions
{: #agent-supported-versions}

You can configure the {{site.data.keyword.agent}} to collect and send infrastructure and application logs to an {{site.data.keyword.logs_full_notm}} instance directly.
{: shortdesc}

The following table lists the agent versions that are supported and the version of Fluent Bit the agent is based on:

| {{site.data.keyword.agent}}                         | Based on Fluent Bit Version | Helm chart version |
|-----------------------------------------------------|-----------------------------|--------------------|
| v1.9.0                                              | [v5.0.6](https://fluentbit.io/announcements/v5.0.6/){: external} | v1.9.0   |
| v1.8.1                                              | [v4.2.2](https://fluentbit.io/announcements/v4.2.2/){: external} | v1.8.1   |
| v1.8.0                                              | [v4.2.2](https://fluentbit.io/announcements/v4.2.2/){: external} | v1.8.0   |
| v1.7.1                                              | [v4.0.8](https://fluentbit.io/announcements/v4.0.8/){: external} | v1.7.1   |
| v1.7.0                                              | [v4.0.8](https://fluentbit.io/announcements/v4.0.8/){: external} | v1.7.0   |
{: caption="Supported agent versions" caption-side="bottom"}

For information on recommended and supported Fluent Bit plug-ins see [Fluent Bit support](/docs/cloud-logs?topic=cloud-logs-agent-plugin-support)
{: tip}
