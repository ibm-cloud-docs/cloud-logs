---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}

# Uninstalling the agent
{: #agent-remove}

You can remove a {{site.data.keyword.logs_routing_full_notm}} agent from an {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

This article might be outdated and contain incomplete or incorrect information.
{: attention}

## Step 1. Log in to the Red Hat OpenShift cluster
{: #agent-remove-step1}

Complete the following steps:

1. Log in to {{site.data.keyword.cloud_notm}} by using the [IBM Cloud CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

   ```text
   ibmcloud login
   ```
   {: pre}

2. Set the infrastructure target to **gen 2**.

   ```text
   ibmcloud is target --gen 2
   ```
   {: pre}

3. Save the endpoint of the VPE that you created to an environment variable. Run the following commands:

    ```sh
    export VPE_NAME=MY_VPE_GW
    export INGESTION_HOST=$(ibmcloud is endpoint-gateways --output json | jq -r '.[] | select(.name==env.VPE_NAME) | .service_endpoint ')
    ```
    {: pre}

    Where **MY_VPE_GW** is the name of the VPE gateway that you created.

4. Log in to the {{site.data.keyword.openshiftlong_notm}} cluster where you plan to deploy the {{site.data.keyword.logs_routing_full_notm}} agent.

    See [Accessing Red Hat OpenShift Clusters](https://cloud.ibm.com/docs/openshift?topic=openshift-access_cluster) if you need help logging in to the cluster.


## Step 2. Uninstalling the {{site.data.keyword.logs_routing_full_notm}} agent
{: #agent-remove-step2}

Run the following `curl` command in your terminal:

```sh
curl -sSL https://ibm.biz/logs-router-uninstall | bash -s -- -t <cluster_type>
```
{: pre}

Where:

`-t`
:   Cluster type. Use this option to define the cluster type where the {{site.data.keyword.logs_routing_full_notm}} Agent is deployed. Choose either `OpenShift` for {{site.data.keyword.openshiftlong_notm}} or `Kubernetes` for {{site.data.keyword.containerlong_notm}}.
