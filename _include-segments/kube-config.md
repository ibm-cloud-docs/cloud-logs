If you have [configured kube auditing](/docs/containers?topic=containers-health-audit#audit-api-server-la), when you use {{site.data.keyword.logs_full_notm}} you need to install the [IBM Cloud Logs agent](/docs/cloud-logs?topic=cloud-logs-agent-about). You also need to change the `Path` in the `tail` `INPUT` section of the `input-kubernetes.conf` file to include:

```text
/var/log/kubelet/kubelet.log,/var/log/syslog
```
{: codeblock}


