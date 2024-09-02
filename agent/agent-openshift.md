---

copyright:
  years:  2024
lastupdated: "2024-09-02"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Managing the {{site.data.keyword.agent}} for {{site.data.keyword.openshiftlong_notm}} clusters
{: #agent-openshift}

You can deploy the {{site.data.keyword.agent}} to collect and route infrastructure and application logs from an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}


## Deploying the agent
{: #agent-openshift-deploy}

Complete the following steps to deploy an agent on an OpenShift cluster:

### Before you begin
{: #agent-openshift-deploy-prereqs}

- Make sure you have access to an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster with permissions to create namespaces and deploy the agent.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Openshift CLI to manage the cluster from the command line. [Learn more](/docs/openshift?topic=openshift-cli-install).

- Read about [the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about).

- [Download and install jq](https://stedolan.github.io/jq/){: external} to process output and query desired results.

- [Download and install yq](https://github.com/mikefarah/yq?tab=readme-ov-file#install){: external} to read, write, and manipulate YAML files in a similar way to using `jq` for JSON files.


### Step 1. Define the authentication method for the agent
{: #agent-openshift-deploy-step1}

Choose the type of identity and the authentication method for the agent. Then, create an API key if needed.

Complete the following steps:

1. Choose the type of identity: user, service ID, or trusted profile.

    You can use a user, a service ID, or a trusted profile as the identity that is used by the agent to authenticate with the {{site.data.keyword.logs_routing_full}} service.

2. Grant permissions for ingestion to the identity that you have chosen.

    The role that is required for sending logs to {{site.data.keyword.logs_full_notm}} is `Writer`.

    For more information, see [Setting up IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-agent-iam-permissions).

3. Generate an API Key for user authentication or for service ID authentication.

    For authentication with trusted profiles, this step is not required.

    For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-api-key).




### Step 2. Setting up and deploying the {{site.data.keyword.agent}} configuration
{: #agent-openshift-deploy-step2}

Complete the following steps:

1. Log in to the cluster.

    {{site.data.keyword.openshiftlong_notm}} is integrated with IBM Cloud Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the Red Hat OpenShift console, your IAM identity is used to generate a Red Hat OpenShift login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the `oc login` command. For more information, see [Accessing Red Hat OpenShift clusters](/docs/openshift?topic=openshift-access_cluster#access_automation).

    For example, complete the steps in [Using a service ID to log in to clusters](/docs/openshift?topic=openshift-access_cluster#access_service_id) to log in to your cluster.

2. Configure the log collection behavior of the {{site.data.keyword.agent}}, see [Configuring whether logs are included or excluded](/docs/cloud-logs?topic=cloud-logs-configure-include-exclude).

3. Install the {{site.data.keyword.agent}}. Use the following `curl` command in your terminal:

    ```sh
    curl -sSL https://ibm.biz/logs-router-setup | bash -s -- \
      -v <agent_version> \
      -m <iam_auth_mode> \
      -i <trusted_profile_id> \
      -k <iam_api_key> \
      -t <cluster_type> \
      -r <region> \
      -p <target_port>
      -d <directory>
      -e PrivateProduction
      -a <application_name>
      -s <subsystem_name>
      --send-directly-to-icl
    ```
    {: codeblock}

    The agent needs access to {{site.data.keyword.iamlong}} (IAM). By detault the agent uses the public endpoint. To use the private endpoint, specify:

    Where:

    `-v`
    :   Agent version. Specify the version of the {{site.data.keyword.agent}}. To find the current supported versions, see [Checking available agent versions](/docs/cloud-logs?topic=cloud-logs-check-agent-versions).

    `-m`
    :   IAM authentication mode (`TrustedProfile` | `IAMAPIKey`).

    `-i`
    :   Trusted profile ID (required for `TrustedProfile` mode). Provide the Trusted Profile ID. When using trusted profiles, set to the ID configured in [Setting up Permissions for Ingestion](/docs/cloud-logs?topic=cloud-logs-agent-iam-permissions&interface=cli).

        For more information on Trusted Profiles, see [Creating a Trusted Profile](/docs/account?topic=account-create-trusted-profile).
        {: tip}

    `-k`
    :   IAM API key (required for `IAMAPIKey` mode). Make sure you follow the instructions in [Generating an API Key](/docs/cloud-logs?topic=cloud-logs-api-key).

        For more information about IAM API Keys, see [Managing API Keys](/docs/account?topic=account-manapikey).
        {: tip}

    `-t`
    :   Cluster type (`OpenShift` or `Kubernetes`). Specify if you are deploying the agent to an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) or {{site.data.keyword.containerlong_notm}} (`Kubernetes`) cluster.

        Value is case-sensitive. `OpenShift` must be specified in this exact case.
        {: important}

    `-r`
    :   Specify the region where the {{site.data.keyword.logs_routing_full_notm}} Ingester endpoint is located (for example `us-east`).

    `-p`
    :   Target port for log ingestion. The default target port is `443`, which corresponds to the ingester target port.
    - Ingester target port: The port must be `443` if you are connecting using a VPE gateway, or port `3443` when connecting using CSEs.

    `-d`
    : Specify the directory containing the `logger-agent.yaml` file configured in the previous step. For example, if your `logger-agent.yaml` file is located in the `/path/to/directory` directory, you would simply specify the directory like this: `-d /path/to/directory`.

    `-a`
    : Specify the application name that you want to see in your {{site.data.keyword.logs_full_notm}} instance. If in the metadata, the application name defaults to namespace name. You can also use variables from the environment, for example `${NODE_NAME}`.

    `-s`
    : Specify the subsystem name that you want to see in your {{site.data.keyword.logs_full_notm}} instance. If in the metadata, the subsystem name defaults to container name. You can also use variables from the environment, for example `${NODE_NAME}`.

    `--send-directly-to-icl`
    :   (Optional) Directly send logs to {{site.data.keyword.logs_full_notm}} instead of through the {{site.data.keyword.logs_routing_full_notm}} data plane. This option is beneficial when managing multiple {{site.data.keyword.logs_full_notm}} instances within the same account for advanced logging configurations.

    For instance, this allows you to segregate logs from different environments (for example, development and production) into separate {{site.data.keyword.logs_full_notm}} instances.

    Ensure to specify the following details specific to your {{site.data.keyword.logs_full_notm}} instance when using this option:

    - `-h <target_host>`: The host for {{site.data.keyword.logs_full_notm}} ingestion, found in the `Endpoints` section of your {{site.data.keyword.logs_full_notm}} instance `Overview`. Use the ingress endpoint.

    - `-p <target_port>`
    : Use `443`.

        This option is particularly useful when managing multiple {{site.data.keyword.logs_full_notm}} instances within the same account, since  {{site.data.keyword.logs_routing_full_notm}} supports only one account tenant per region.
        {: note}

    - `-e PrivateProduction`
    : This option sets the [`IAM_Environment` plug-in parameter value](/docs/cloud-logs?topic=cloud-logs-routing-plugin-parameters#authentication_parms). All valid `IAM_Environment` plug-in parameter values can be specified for `-e`.

    - `--send-directly-to-icl`
    : You must set this parameter to send logs directly to {{site.data.keyword.logs_full_notm}}


The agent can only send logs through private endpoints.
{: important}

The following sample output shows a successful deployment of an agent in an Openshift cluster.

```text
========================================
       AGENT INSTALLATION DETAILS
========================================
Version               : 1.0.3
IAM Environment       : Production
IAM Auth Mode         : IAMAPIKey
Trusted Profile ID    :
IAM API Key           : **********
Cluster Type          : OpenShift
Cluster Name          : default
Region                : us-east
Ingester Target Host  : ingester.private.us-east.logs-router.cloud.ibm.com
Ingester Target Port  : 3443
========================================
Downloading and applying configuration from https://logs-router-agent-config.s3.us.cloud-object-storage.appdomain.cloud/logger-agent.yaml for agent version latest in default.
Warning: resource namespaces/logger-agent is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
namespace/logger-agent configured
serviceaccount/logger-agent-sa created
clusterrole.rbac.authorization.k8s.io/logger-agent-read-cr created
clusterrolebinding.rbac.authorization.k8s.io/logger-agent-read-crb created
securitycontextconstraints.security.openshift.io/hostmount-logger created
configmap/logger-agent-config created
daemonset.apps/logger-agent-ds created
Configuration applied successfully.

====**** logger-agent version 1.0.3, installed successfully in default ****====
```
{: screen}



### Step 3. Verify the agent is successfully deployed
{: #agent-openshift-deploy-step3}

When the agent is deployed, check the following resources are created:
- The `ibm-observe` namespace.

    Run `oc get namespace` to list the namespaces in the cluster. You can also run `oc get namespace | grep ibm-observe` to search for the `ibm-observe` namespace.

- A config map `logger-agent-config` in the namespace `ibm-observe`.

    Run `oc get configmap logger-agent-config -n ibm-observe` to view the agent config details. You can also use `oc describe configmaps logger-agent-config -n ibm-observe`.

- A deamonset `logger-agent-ds` in the namespace `ibm-observe`.

    Run `oc get ds -n ibm-observe` to view the daemonset.

- Retrieve the list of agent pods by using the following command:

    ```sh
    oc get pods -n ibm-observe -o wide
    ```
    {: pre}

    ```text
    NAME                     READY     STATUS    RESTARTS AGE    IP              NODE           NOMINATED NODE   READINESS GATES
    logger-agent-ds-4lwvt      1/1     Running   0          2d5h   172.17.61.181   192.168.16.4   <none>           <none>
    logger-agent-ds-g7z87      1/1     Running   0          2d5h   172.17.0.48     192.168.32.4   <none>           <none>
    logger-agent-ds-nw56s      1/1     Running   0          2d5h   172.17.32.232   192.168.0.10   <none>           <none>
    logger-agent-ds-wcpbl      1/1     Running   0          2d5h   172.17.6.190    192.168.0.9    <none>           <none>
    ```
    {: screen}

    The `READY` column shows `1/1` for all pods, with a `STATUS` of `Running`. Verify that an agent pod is ready for each node in your cluster.

    To check how many workers are available in your cluster, you can run the following command:

    ```sh
    oc get nodes
    ```

    ```text
    NAME           STATUS   ROLES           AGE   VERSION
    192.168.0.10   Ready    master,worker   8d    v1.20.0+558d959
    192.168.0.9    Ready    master,worker   8d    v1.20.0+558d959
    192.168.16.4   Ready    master,worker   8d    v1.20.0+558d959
    192.168.32.4   Ready    master,worker   8d    v1.20.0+558d959
    ```
    {: screen}

    The number of items in each of these two lists need to be the same, and you can match the IP addresses in the node names with the values in the `NODE` column of the pod listing.

    If your nodes are not named by their IP, you can append the `-o wide` option and compare the values in the `INTERNAL-IP` column instead.

The agent installation will always indicate that the command is done. However, if a connection to the cluster is lost, the installation will not correctly complete. If verifying your deployment indicates that the installation did not correctly complete, reconnect to your cluster and retry the installation.
{: tip}

### Step 4. Verify logs are being delivered to your target destination
{: #agent-openshift-deploy-step4}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.la_short}} instance.](/docs/log-analysis?topic=log-analysis-launch&interface=ui)

2. When your agent is correctly configured, you can see logs through the default dashboard view. The {{site.data.keyword.agent}} tags log records with a meta object that includes the cluster name.

    ```text
    meta.cluster_name:<CLUSTER_NAME>
    ```
    {: codeblock}

    You can run the query `meta.cluster_name:<YOUR_CLUSTER_NAME>` in your {{site.data.keyword.la_short}} instance to search for logs that are generated by your cluster.

### Step 5. (Optional) Add additional metadata fields
{: #agent-openshift-deploy-step5}

You can add additional metadata fields to the routed logs.

1. Edit the `logger-agent-config.yaml` file in the `logger-agent` namespace.

2. In the `fluent-bit.conf` section add your custom metadata using this structure.

   ```yaml
    [FILTER]
       Name record_modifier
       Match *
       Record <meta.key_name> <your_custom_value>
   ```
   {: codeblock}

   Where `<meta.key_name>` is the name of the metadata field to be added (for example, `meta.env`) and `<your_custom_value>` is the value to be assigned to the field (for example, the name of your environment).

   For example, if you want to add an environment and region name as metadata, the configuration would be similar to this:

   ```yaml
   [FILTER]
       Name record_modifier
       Match *
       Record meta.cluster_name my-cluster
       Record meta.env production
       Record meta.region us-east
   ```
   {: codeblock}

3. Save the configuration file.

4. Restart the daemonset to apply the changes by running the following:

   ```sh
   oc rollout restart daemonset logger-agent-ds -n logger-agent
   ```
   {: codeblock}

The cluster name cannot currently be changed. It will always be `default`.
{: restriction}

## Uninstalling the agent
{: #agent-openshift-remove}

Complete the following steps to remove a {{site.data.keyword.agent}}:

1. Log in to the cluster.

    {{site.data.keyword.openshiftlong_notm}} is integrated with IBM Cloud Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the Red Hat OpenShift console, your IAM identity is used to generate a Red Hat OpenShift login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the oc login command. For more information, see [Accessing Red Hat OpenShift clusters](/docs/openshift?topic=openshift-access_cluster#access_automation).

    For example, complete the steps in [Using a service ID to log in to clusters](/docs/openshift?topic=openshift-access_cluster#access_service_id) to log in to your cluster.

2. Delete the daemonset.

   ```sh
   oc delete ds logger-agent-ds -n ibm-observe
   ```
   {: pre}

3. Delete the configmap.

   ```sh
   oc delete cm logger-agent-config -n ibm-observe
   ```
   {: pre}

4. Delete the secrets by deleting the service account.

   ```sh
   oc delete sa logger-agent-sa -n ibm-observe
   ```
   {: pre}

   ```sh
   oc delete secret iam-api-key-secret -n ibm-observe
   ```
   {: pre}


    
