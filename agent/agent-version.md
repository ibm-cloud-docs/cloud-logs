---

copyright:
  years:  2024
lastupdated: "2024-09-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Checking the available agent versions
{: #check-agent-versions}

Before specifying a version, you can check the available Logging agent versions.
{: shortdesc}

Do the following to check the available agent versions.

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
    icr.io/ibm/observe/logger-agent-plugin   1.0.0    e37324ab54e0   ibm         3 months ago   77 MB    -
    icr.io/ibm/observe/logger-agent-plugin   1.0.1    ac53710f048e   ibm         3 months ago   77 MB    -
    icr.io/ibm/observe/logger-agent-plugin   1.0.2    9d7eeb343eac   ibm         3 months ago   94 MB    -
    icr.io/ibm/observe/logger-agent-plugin   1.0.3    801f6a859e7a   ibm         1 month ago    94 MB    -
    icr.io/ibm/observe/logger-agent-plugin   1.0.4    56a53b9a3f9b   ibm         4 weeks ago    98 MB    -
    icr.io/ibm/observe/logger-agent-plugin   1.0.5    504d0ba2fbac   ibm         21 hours ago   104 MB   -
    ```
    {: screen}

    Choose the desired version (for example 1.0.2 or 1.0.1) when running the installation command with the `-v` flag.
