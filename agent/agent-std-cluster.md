---

copyright:
  years:  2024, 2025
lastupdated: "2025-04-08"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Managing the {{site.data.keyword.agent}} for {{site.data.keyword.containerlong_notm}} clusters
{: #agent-std-cluster}

You can deploy the {{site.data.keyword.agent}} to collect and route infrastructure and application logs from an {{site.data.keyword.containerlong_notm}} cluster to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

This topic is superseded by [Deploying the Logging agent on Kubernetes using a Helm chart](/docs/cloud-logs?topic=cloud-logs-agent-helm-kube-deploy). While these instructions can still be used, deploying using the Helm chart is the preferred method.
{: important}

## Deploying the {{site.data.keyword.agent}}
{: #agent-std-cluster-deploy}

Complete the following steps to deploy the {{site.data.keyword.agent}} on an {{site.data.keyword.containerlong_notm}} cluster:

### Before you begin
{: #agent-std-cluster-deploy-prereqs}

- Make sure you have access to Kubernetes cluster with permissions to create namespaces and deploy the agent.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Kubernetes CLI to manage the cluster by using `kubectl` commands. [Learn more](/docs/containers?topic=containers-cli-install).

- Read about [the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about).

- Check the agent versions that are available. For more information, see [Checking the available agent versions](/docs/cloud-logs?topic=cloud-logs-check-agent-versions).

- [Download and install jq](https://stedolan.github.io/jq/){: external} to process output and query desired results.

- [Download and install yq](https://github.com/mikefarah/yq?tab=readme-ov-file#install){: external} to read, write, and manipulate YAML files in a similar way to using `jq` for JSON files.


### Step 1. Define the authentication method for the agent
{: #agent-std-deploy-step1}

Choose the type of identity and the authentication method for the agent. Then, create an API key if needed.

Complete the following steps:

1. Choose the type of identity: user, service ID, or trusted profile.

    You can use a user, a service ID, or a trusted profile as the identity that is used by the agent to authenticate with the {{site.data.keyword.logs_full}} service.

2. Grant permissions for ingestion to the identity that you have chosen.

    The role that is required for sending logs to {{site.data.keyword.logs_full_notm}} is `Sender`.

    For more information, see [Setting up IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).

3. Generate an API Key for user authentication or for service ID authentication.

    For authentication with trusted profiles, this step is not required.

    For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).





## Step 2. Setting up and deploying the {{site.data.keyword.agent}} configuration
{: #agent-std-deploy-step2}

Complete the following steps:

1. [Access your cluster](/docs/containers?topic=containers-access_cluster).

2. Configure the log collection behavior of the {{site.data.keyword.agent}}, see [Configuring whether logs are included or excluded](/docs/cloud-logs?topic=cloud-logs-configure-include-exclude).

3. Install the {{site.data.keyword.agent}}. Use the following `curl` command in your terminal:

    ```sh
    curl -sSL https://ibm.biz/logs-router-setup | bash -s -- \
      -v <agent_version> \
      -m <iam_auth_mode> \
      -i <trusted_profile_id> \
      -k <iam_api_key> \
      -t <cluster_type> \
      -d <directory> \
      -e PrivateProduction \
      -a <application_name> \
      -s <subsystem_name> \
      --send-directly-to-icl -h <target_host> -p <target_port>
    ```
    {: codeblock}

    Where:

    `-v <agent_version>`
    :   Agent version. Specify the version of the {{site.data.keyword.agent}}. To find the current supported versions, refer to [Checking available agent versions](/docs/cloud-logs?topic=cloud-logs-check-agent-versions).

    `-m <iam_auth_mode>`
    :   IAM authentication mode (`TrustedProfile` | `IAMAPIKey`).

    `-i <trusted_profile_id>`
    :   Trusted profile ID (required for `TrustedProfile` mode). Provide the Trusted Profile ID. When using trusted profiles, set to the ID configured in [Setting up Permissions for Ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions&interface=cli).

        For more information on Trusted Profiles, see [Creating a Trusted Profile](/docs/account?topic=account-create-trusted-profile). {: tip}

    `-k <iam_api_key>`
    :   IAM API key (required for `IAMAPIKey` mode). Make sure you follow the instructions in [Generating an API Key](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).

        For more information about IAM API Keys, see [Managing API Keys](/docs/account?topic=account-manapikey).
        {: tip}

    `-t <cluster_type>`
    :   Cluster type (`OpenShift` or `Kubernetes`). Specify if you are deploying the agent to an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) or {{site.data.keyword.containerlong_notm}} (`Kubernetes`) cluster.

    `-d <directory>`
    : Specify the directory containing the `logger-agent-iks.yaml` file configured in the previous step. For example, if your `logger-agent-iks.yaml` file is located in the `/path/to/directory` directory, you would simply specify the directory like this: `-d /path/to/directory`.

    `-a <application_name>`
    : Specify the application name that you want to see in your {{site.data.keyword.logs_full_notm}} instance. If in the metadata, the application name defaults to namespace name. You can also use variables from the environment, for example `'${NODE_NAME}'`.

    `-s <subsystem_name>`
    : Specify the subsystem name that you want to see in your {{site.data.keyword.logs_full_notm}} instance. If in the metadata, the subsystem name defaults to container name. You can also use variables from the environment, for example `'${NODE_NAME}'`.

    `-e PrivateProduction`
    : The agent needs access to {{site.data.keyword.iamlong}} (IAM). By detault the agent uses the public endpoint. To use the private endpoint, set this option. For more information, see [`IAM_Environment` plug-in parameter value](/docs/cloud-logs?topic=cloud-logs-agent-plugin-parameters#agent-plugin-parameters-authentication-parms). All valid `IAM_Environment` plug-in parameter values can be specified for `-e`.

    `--send-directly-to-icl`
    :   Set this parameter to send logs directly to {{site.data.keyword.logs_full_notm}}.

    `-h <target_host>`
    : The host for {{site.data.keyword.logs_full_notm}} ingestion, found in the `Endpoints` section of your {{site.data.keyword.logs_full_notm}} instance `Overview`. Use the ingress endpoint.

    `-p <target_port>`
    : Use `443`.


Notice the agent can only send logs through private endpoints.
{: important}

The following sample output shows a successful deployment of an agent in an Openshift cluster.

```screen
% curl -sSL https://ibm.biz/logs-router-setup | bash -s --   -v 1.0.5   -m IAMAPIKey   -k xxxxx   -t Kubernetes   -r eu-es   -p 443
Current kubectl context: mycluster-dallas/cm7g4rmd02o78j7gr670
========================================
       AGENT INSTALLATION DETAILS
========================================
Version               : 1.0.5
IAM Environment       : Production
IAM Auth Mode         : IAMAPIKey
Trusted Profile ID    :
IAM API Key           : **********
Cluster Type          : Kubernetes
Cluster Name          : mycluster-dallas
Region                : eu-es
Ingester Target Host  : ingester.private.eu-es.logs-router.cloud.ibm.com
Ingester Target Port  : 443
========================================
Downloading and applying configuration from https://logs-router-agent-config.s3.us.cloud-object-storage.appdomain.cloud/logger-agent-iks.yaml for agent version 1.0.5 in mycluster-dallas.
Warning: resource namespaces/ibm-observe is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
namespace/ibm-observe configured
serviceaccount/logger-agent-sa created
clusterrole.rbac.authorization.k8s.io/logger-agent-read-cr configured
clusterrolebinding.rbac.authorization.k8s.io/logger-agent-read-crb configured
secret/iam-api-key-secret created
configmap/logger-agent-config created
daemonset.apps/logger-agent-ds created
Configuration applied successfully.

====**** logger-agent version 1.0.5, installed successfully in mycluster-dallas ****====
```
{: screen}


### Step 3. Verify the agent is successfully deployed
{: #agent-std-deploy-step3}

When the agent is deployed by using the default configuration, check the following resources are created:
- A namespace `ibm-observe`.

    Run `kubectl get namespace` to list the namespaces in the cluster. You can also run `oc get namespace | grep ibm-observe` to search for the `ibm-observe` namespace.

- A config map `logger-agent-config` in the namespace `ibm-observe`.

    Run `kubectl get configmap logger-agent-config -n ibm-observe` to view the agent config details. You can also use `kubectl describe configmaps logger-agent-config -n ibm-observe`.

- A deamonset `logger-agent-ds` in the namespace `ibm-observe`.

    Run `kubectl get ds -n ibm-observe` to view the deamonset.

- Retrieve the list of agent pods by using the following command:

    ```sh
    kubectl get pods -n ibm-observe -o wide
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

    The `READY` column shows `1/1` for all pods, with a `STATUS` of `Running`. Verify that an agent pod is ready for each node in your cluster:

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

    The number of items in each of these two lists need to be the same,
    and you can match the IP addresses in the node names with the values in the `NODE` column of the pod listing.

    If your nodes are not named by their IP, you can append the `-o wide` option and compare the values in the `INTERNAL-IP` column instead.


### Step 4. Verify logs are being delivered to your target destination
{: #agent-std-deploy-step4}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view. The {{site.data.keyword.agent}} tags log records with a meta object that includes the cluster name.

    ```text
    meta.cluster_name:<CLUSTER_NAME>
    ```
    {: codeblock}

    You can run the query `meta.cluster_name:<YOUR_CLUSTER_NAME>` in your {{site.data.keyword.logs_full_notm}} instance to search for logs that are generated by your cluster.

### Step 5. (Optional) Add additional metadata fields
{: #agent-std-deploy-step5}

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

4. Restart the daemon set to apply the changes by running the following:

   ```sh
   kubectl rollout restart daemonset logger-agent-ds -n logger-agent
   ```
   {: codeblock}

## Updating the agent
{: #agent-std-cluster-update}

Complete the following steps to update the agent to the latest agent version.

1. [Access your cluster](/docs/containers?topic=containers-access_cluster).

2. To update the agent, complete the following steps used to initially deploy the agent:

    1. [Step 2](#agent-std-deploy-step2)
    2. [Step 3](#agent-std-deploy-step3)
    3. [Step 4](#agent-std-deploy-step4)

## Uninstalling the agent
{: #agent-std-remove}


Complete the following steps to remove an agent:

1. [Access your cluster](/docs/containers?topic=containers-access_cluster).

2. Delete the daemonset.

   ```sh
   kubectl delete ds logger-agent-ds -n ibm-observe
   ```
   {: pre}

3. Delete the configmap.

   ```sh
   kubectl delete cm logger-agent-config -n ibm-observe
   ```
   {: pre}

4. Delete the secrets by deleting the service account.

   ```sh
   kubectl delete sa logger-agent-sa -n ibm-observe
   ```
   {: pre}

   ```sh
   kubectl delete secret iam-api-key-secret -n ibm-observe
   ```
   {: pre}
