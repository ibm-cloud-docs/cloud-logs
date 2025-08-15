---

copyright:
  years:  2024, 2025
lastupdated: "2025-08-15"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Checking the available Helm chart versions for agent versions up to v1.5.x
{: #helm-chart-versions-1}

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
    ibmcloud cr images --restrict ibm/observe | grep logs-agent
    ```
    {: codeblock}

    The following is an example results of the command:

    ```screen
    icr.io/ibm/observe/logs-agent-helm             1.3.0            811fac528db6   ibm         -               8.8 kB   -
    icr.io/ibm/observe/logs-agent-helm             1.3.1            da377c60f41e   ibm         -               8.8 kB   -
    icr.io/ibm/observe/logs-agent-helm             1.3.2            cac2720cb540   ibm         -               8.8 kB   -
    icr.io/ibm/observe/logs-agent-helm             1.3.3            e578a3b8fe56   ibm         -               9.5 kB   -
    icr.io/ibm/observe/logs-agent-helm             1.4.0            83d8272790fc   ibm         -               9.6 kB   -
    icr.io/ibm/observe/logs-agent-helm             1.4.1            5d6866063f12   ibm         -               9.9 kB   -
    icr.io/ibm/observe/logs-agent-helm             1.4.2            d2065465b3de   ibm         -               10 kB    -
    icr.io/ibm/observe/logs-agent-helm             1.5.0            4ddbd972486e   ibm         -               11 kB    -
    icr.io/ibm/observe/logs-agent-helm             1.5.1            c3de72fe617d   ibm         -               11 kB    -
    icr.io/ibm/observe/logs-agent-helm             1.5.2            28626db3c3ef   ibm         -               11 kB    -
    icr.io/ibm/observe/logs-agent-helm             1.6.0            d8d033ed0b23   ibm         -               18 kB    -
    icr.io/ibm/observe/logs-agent-helm             1.6.1            e8f973d5f42e   ibm         -               20 kB    -
    ```
    {: screen}
