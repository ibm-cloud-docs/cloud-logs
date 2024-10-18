---

copyright:
  years:  2024
lastupdated: "2024-09-30"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Uninstalling the {{site.data.keyword.agent}} using a Helm chart
{: #agent-helm-remove}

You can use a Helm chart to uninstall the {{site.data.keyword.agent}} from an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}


## Before you begin
{: #agent-helm-remove-prereqs}

- Make sure you have access to an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster with permissions to create namespaces and deploy the agent.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Openshift CLI to manage the cluster from the command line. [Learn more](/docs/openshift?topic=openshift-cli-install).

    - The latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases)

- Read about [the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about).


## Uninstall the {{site.data.keyword.agent}}
{: #agent-helm-remove-1}

Complete the following steps to remove a {{site.data.keyword.agent}}:

1. Log in to the cluster.

    {{site.data.keyword.openshiftlong_notm}} is integrated with IBM Cloud Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the Red Hat OpenShift console, your IAM identity is used to generate a Red Hat OpenShift login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the oc login command. For more information, see [Accessing Red Hat OpenShift clusters](/docs/openshift?topic=openshift-access_cluster#access_automation). For example, complete the steps in [Using a service ID to log in to clusters](/docs/openshift?topic=openshift-access_cluster#access_service_id) to log in to your cluster.

2. Run the helm uninstall to remove the resources created by the Helm chart

   ```sh
   helm uninstall <install-name>
   ```
   {: codeblock}

    where:

    - `<install-name>` is the name of the helm installation (ie. `logs-agent`)
