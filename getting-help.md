---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Getting help and support
{: #getting-help}

If you have problems or questions when using {{site.data.keyword.logs_full_notm}}, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.
{: shortdesc}

* You can check whether the {{site.data.keyword.cloud_notm}} is available by going to the [{{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.

* You can review the forums to see whether other users ran into the same problem. When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.

* If you still can't resolve the problem, you can open an IBM support ticket. For information about opening an IBM support ticket, or about support levels and ticket severities, see [Creating support cases](/docs/cloud-logs?topic=cloud-logs-data-usage-enable-metrics).


  
## Information to include in a support case for the {{site.data.keyword.powerSysShort}} agent
{: #getting-help-agent-support-case}

When you open a support case about a problem with the {{site.data.keyword.powerSysShort}} {{site.data.keyword.agent}}, include the following information:

* The output of the `systemctl status otelcol-ibm` command.
* The last 100 lines of the service output. To display them, run the `journalctl -u otelcol-ibm -n 100` command. Remove any sensitive data from the output before you share it.
* The agent version. To display it, run the `rpm -q otelcol-ibm` command.
* The region of your {{site.data.keyword.logs_full_notm}} instance and the time when the problem occurred.

Do not include your API key in the support case.
{: important}


