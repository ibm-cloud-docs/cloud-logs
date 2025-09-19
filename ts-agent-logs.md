---

copyright:
  years:  2024, 2025
lastupdated: "2025-09-19"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# How can I find the {{site.data.keyword.logs_full_notm}} {{site.data.keyword.agent}} logs?
{: #ts-agent-logs}
{: troubleshoot}
{: support}

You might need to know where to find the {{site.data.keyword.agent}} logs when debugging an issue where {{site.data.keyword.logs_full}} is not receiving logs sent by the {{site.data.keyword.agent}}.
{: shortdesc}

You believe you have configured the {{site.data.keyword.agent}} from your Kubernetes clusters or Linux environments correctly, but you are seeing one or more of the following:
{: tsSymptoms}

* Logs not appearing in {{site.data.keyword.logs_full_notm}}.

* Logs in the {{site.data.keyword.logs_full_notm}} UI starting with the string `ICL dropped logs`.

There can be an issue with the {{site.data.keyword.agent}} where [logs are not being ingested](/docs/cloud-logs?topic=cloud-logs-ts-ingestion-failures) and you want to review the {{site.data.keyword.agent}} logs in the environment where the {{site.data.keyword.agent}} is running.
{: tsCauses}

The {{site.data.keyword.agent}} log location depends on the environment where the {{site.data.keyword.agent}} is running.
{: tsResolve}

[Kubernetes]{: tag-iks}

* For {{site.data.keyword.containerlong_notm}} do the following:

   The {{site.data.keyword.agent}} daemonset runs on each pod. To list all pods for the `log-agent` daemonset run:

    ```sh
    kubectl get pods -n ibm-observe -o wide -l app=logs-agent
    ```
    {: codeblock}

    To look at the logs for a specific pod run the following command where `<POD_NAME>` is the pod name.

    ```sh
    kubectl logs -n ibm-observe <POD_NAME>
    ```
    {: codeblock}


* For {{site.data.keyword.openshiftlong_notm}} do the following:

    The {{site.data.keyword.agent}} daemonset runs on each pod. To list all pods for the `log-agent` daemonset run:

    ```sh
    oc get pods -n ibm-observe -o wide -l app=logs-agent
    ```
    {: codeblock}

    To look at the logs for a specific pod run the following command where `<POD_NAME>` is the pod name.

    ```sh
    oc logs -n ibm-observe <POD_NAME>
    ```
    {: codeblock}

[Linux]{: tag-linux}

To view logs for the {{site.data.keyword.agent}} running in Linux, from the Linux system run the following:

```sh
journalctl -u fluent-bit.service
```
{: codeblock}
