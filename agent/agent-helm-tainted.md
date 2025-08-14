---

copyright:
  years:  2025, 2025
lastupdated: "2025-08-14"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Ensure tainted nodes are updated
{: #agent-helm-tainted}

When you deploy or upgrade the Logging agent, you can configure the `logs-values.yaml` file to include information on what to do when you have tainted nodes.

For example, if you have a taint on a node: `kubectl taint nodes 10.1.2.3 myNodeType=ingress:NoSchedule`, you can configure the agent to be scheduled on that node by adding the `tolerations` configuration to your `log-values.yaml` file:

```yaml
tolerations:
  - effect: NoSchedule
    key: myNodeType
    value: ingress
    operator: Equal
```
{: codeblock}

- These fields are directly added to the DaemonSet's tolerations section.
- This ensures the agent respects the taint rules and can be scheduled accordingly.
