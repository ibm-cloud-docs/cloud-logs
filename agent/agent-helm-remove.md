---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-18"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Uninstalling the {{site.data.keyword.agent}} using a Helm chart
{: #agent-helm-remove}

You can use Helm to uninstall the {{site.data.keyword.agent}} from a cluster.
{: shortdesc}


## Before you begin
{: #agent-helm-remove-prereqs}

- Make sure you have access to an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster with permissions to create namespaces and deploy the agent.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Kubernetes CLI to manage Kubernetes clusters by using `kubectl` commands. [Learn more](/docs/containers?topic=containers-cli-install).

    - The Openshift CLI to manage OpenShift clusters from the command line. [Learn more](/docs/openshift?topic=openshift-cli-install).

    - The latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases)

- Read about [the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about).


## Uninstall the {{site.data.keyword.agent}}
{: #agent-helm-remove-1}

Complete the following steps to remove a {{site.data.keyword.agent}}:

1. Log in to the cluster.

    To log in to a Kubernetes cluster, see [Access your cluster](/docs/containers?topic=containers-access_cluster).

    To log in to an Openshift cluster: {{site.data.keyword.openshiftlong_notm}} is integrated with IBM Cloud Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the Red Hat OpenShift console, your IAM identity is used to generate a Red Hat OpenShift login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the oc login command. For more information, see [Accessing Red Hat OpenShift clusters](/docs/openshift?topic=openshift-access_cluster#access_automation). For example, complete the steps in [Using a service ID to log in to clusters](/docs/openshift?topic=openshift-access_cluster#access_service_id) to log in to your cluster.

2. Log in to the Helm registry. Choose one of the following options:

    Option 1: Login to the Helm registry by running the `helm registry login` command:

    ```sh
    helm registry login -u iambearer -p $(ibmcloud iam oauth-tokens --output json | jq -r .iam_token | cut -d " " -f2) icr.io
    ```
    {: codeblock}

    [Windows]{: tag-windows} Windows PowerShell users should use this command instead:

    ```sh
    helm registry login -u iambearer -p ((ibmcloud iam oauth-tokens --output json | ConvertFrom-Json).iam_token -replace 'Bearer ', '') icr.io
    ```
    {: codeblock}

    For more information, see [Using Helm charts in Container Registry: Pulling charts from another registry or Helm repository](/docs/Registry?topic=Registry-registry_helm_charts#registry_helm_charts_pull)

    Option 2:  Log in to the Helm registry in {{site.data.keyword.registryshort}} by running the `ibmcloud cr login` command.

    You can use the `ibmcloud cr login` command before you perform a Helm dry run or install. For more information, see [Accessing {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry_access) and [ibmcloud cr login](/docs/Registry?topic=Registry-containerregcli#bx_cr_login).

    Run the following commands:

    ```sh
    ibmcloud cr region-set global
    ```
    {: codeblock}

    ```sh
    ibmcloud cr login [--client CLIENT]
    ```
    {: codeblock}

3. Run the helm uninstall to remove the resources created by the Helm chart

   ```sh
   helm uninstall <install-name>
   ```
   {: codeblock}

    where:

    - `<install-name>` is the name of the helm installation (`logging-agent`)
