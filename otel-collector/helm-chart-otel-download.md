---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Downloading a Helm chart version
{: #helm-chart-otel-download}

You can use a Helm chart to deploy, upgrade, and remove the OTel collector from a Kubernetes cluster or an Openshift cluster.
{: shortdesc}

Complete the following steps to download a Helm chart version:
1. Login to IBM Cloud using the CLI.

    For detailed instructions about logging in using the IBM Cloud CLI, see [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login).

2. Check the Helm chart versions that are available.

    For more information, see [Checking the available Helm chart versions](/docs/cloud-logs?topic=cloud-logs-helm-chart-otel-versions).

3. Run the following command to download a Helm chart:

    ```text
    helm pull oci://icr.io/icl-charts/ibm-otel-collector-charts --version CHART_VERSION
    ```
    {: codeblock}

    A file named `ibm-otel-collector-charts-v0.1.2-202605131059.tgz` is downloaded.

    For example, when you run `helm pull oci://icr.io/icl-charts/ibm-otel-collector-charts --version v0.1.2-202605131059`, the file *ibm-otel-collector-charts-v0.1.2-202605131059.tgz* is downloaded.

4. Run the following command to extract the chart files:

    ```text
    tar -xvf logs-agent-helm-{CHART_VERSION}.tgz
    ```
    {: codeblock}
