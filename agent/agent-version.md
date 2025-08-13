---

copyright:
  years:  2024, 2025
lastupdated: "2025-08-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Checking the available {{site.data.keyword.agent}} versions
{: #check-agent-versions}

Before specifying a version, you can check the available {{site.data.keyword.agent}} versions.
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
    ibmcloud cr images --restrict ibm/observe/logger-agent-plugin
    ```
    {: codeblock}

    The following is an example results of the command:

    ```screen
    Repository                               Tag      Digest         Namespace   Created        Size     Security status
    icr.io/ibm/observe/logger-agent-plugin   1.6.0   6a34ea510a4f   ibm         2 months ago    102 MB   -
    icr.io/ibm/observe/logger-agent-plugin   1.6.1   0265b85c698e   ibm         1 month ago     109 MB   -
    ```
    {: screen}

    Choose the desired version (for example 1.6.1) when running the installation command with the `-v` flag.
