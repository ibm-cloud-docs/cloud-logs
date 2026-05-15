---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Remove the OTel collector
{: #otel-collector-remove}

Complete the following steps to remove the OTel collector that is deployed in a Kubernetes cluster or an Openshift cluster:
{: shortdesc}


1. Login to IBM Cloud using the CLI.

    For detailed instructions about logging in using the IBM Cloud CLI, see [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login).

2. Check the Helm chart versions that are available. Identify the one that you want to upgrade to.

    For more information, see [Checking the available Helm chart versions](/docs-draft/cloud-logs?topic=cloud-logs-helm-chart-otel-versions).

3. Login to the cluster.

    [{{site.data.keyword.containershort}}]{: tag-iks} Log into your Kubernetes cluster. For more information, see [Accessing clusters](/docs/containers?topic=containers-access_cluster).

    [{{site.data.keyword.openshiftshort}}]{: tag-roks} Log into your OpenShift cluster. For more information, see [Accessing Red Hat OpenShift clusters](/docs/openshift?topic=openshift-access_cluster).

4. Run the following command to remove the OTel collector:

    ```text
    helm uninstall ibm-otel-collector -n ibm-observe
    ```
    {: codeblock}
