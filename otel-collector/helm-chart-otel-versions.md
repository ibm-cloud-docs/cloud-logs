---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Checking the available Helm chart versions
{: #helm-chart-otel-versions}

You can use a Helm chart to deploy, upgrade, and remove the {{site.data.keyword.agent}} from a Kubernetes cluster or an Openshift cluster. Before specifying a version, you can check the available Helm chart versions.
{: shortdesc}

Do the following to check the available {{site.data.keyword.agent}} versions.

1. Login to IBM Cloud using the CLI.

    For detailed instructions about logging in using the IBM Cloud CLI, see [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login).
    {: tip}

2. Set the `cr` region to global by using the command:

    ```text
    ibmcloud cr region-set global
    ```
    {: codeblock}

3. Run the following command:

    ```text
    ibmcloud cr images --restrict 'icl-charts'
    ```
    {: codeblock}

    The following is an example results of the command:

    ```screen
    Repository                                    Tag                   Digest         Namespace    Created   Size    Security status
    icr.io/icl-charts/ibm-otel-collector-charts   v0.1.2-202605131059   6d9a55e2e6cb   icl-charts   -         48 kB   -
    icr.io/icl-charts/icl-otel-collecter-charts   v0.1.1-202604200934   5ed33a12a478   icl-charts   -         45 kB   -

    OK
    ```
    {: screen}
