---

copyright:
  years:  2024, 2025
lastupdated: "2025-08-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Checking the available Helm chart versions
{: #helm-chart-versions}

Before specifying a version, you can check the available Helm chart versions.
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
    ibmcloud cr images --restrict ibm-observe | grep logs-agent
    ```
    {: codeblock}

    The following is an example results of the command:

    ```screen
    icr.io/ibm/observe/logs-agent-helm             1.6.0            d8d033ed0b23   ibm         -               18 kB    -
    icr.io/ibm/observe/logs-agent-helm             1.6.1            e8f973d5f42e   ibm         -               20 kB    -
    ```
    {: screen}
