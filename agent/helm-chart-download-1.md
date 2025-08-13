---

copyright:
  years:  2024, 2025
lastupdated: "2025-08-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Downloading a Helm chart version for agent versions up to v1.5.x
{: #helm-chart-download-1}

Complete the following steps to download a Helm chart version for agent versions up to v1.5.x.
{: shortdesc}

1. Login to IBM Cloud using the CLI.

    For detailed instructions about logging in using the IBM Cloud CLI, see [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login).
    {: tip}

2. Check the Helm chart versions that are available. For more information, see [Checking the available Helm chart versions](/docs/cloud-logs?topic=cloud-logs-helm-chart-versions).

3. Login to the Helm registry by running the helm registry login command:

    ```text
    helm registry login -u iambearer -p $(ibmcloud iam oauth-tokens --output json | jq -r .iam_token | cut -d " " -f2) icr.io
    ```
    {: codeblock}

    [Windows]{: tag-windows} Windows PowerShell users should use this command instead:

    ```sh
    helm registry login -u iambearer -p ((ibmcloud iam oauth-tokens --output json | ConvertFrom-Json).iam_token -replace 'Bearer ', '') icr.io
    ```
    {: codeblock}

4. Run the following command to download a Helm chart:

    ```text
    helm pull oci://icr.io/ibm/observe/logs-agent-helm --version CHART_VERSION
    ```
    {: codeblock}

    A file named `logs-agent-helm-{CHART_VERSION}.tgz` is downloaded.

    For example, when you run `helm pull oci://icr.io/ibm/observe/logs-agent-helm --version 1.5.0`, the file *logs-agent-helm-1.5.0.tgz* is downloaded.

5. Run the following command to extract the chart files:

    ```text
    tar -xvf logs-agent-helm-{CHART_VERSION}.tgz
    ```
    {: codeblock}
