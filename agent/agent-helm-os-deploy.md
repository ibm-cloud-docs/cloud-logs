---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-03"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Deploying the {{site.data.keyword.agent}} for OpenShift clusters using a Helm chart
{: #agent-helm-os-deploy}

You can use a Helm chart to deploy the {{site.data.keyword.agent}} to collect and route infrastructure and application logs from an OpenShift cluster to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

Complete the following steps to deploy an agent on an OpenShift cluster:

## Before you begin
{: #agent-helm-os-deploy-prereqs}

- Make sure you have access to an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster with permissions to create namespaces and deploy the agent.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Openshift CLI to manage the cluster from the command line. [Learn more](/docs/openshift?topic=openshift-cli-install).

    - The latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases)

- Read about [the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about).

- Check the agent versions that are available. For more information, see [Checking the available agent versions](/docs/cloud-logs?topic=cloud-logs-check-agent-versions).  Note that the version of the Helm chart will match the version of the agent - for example, if you are using version 1.3.0 of the agent there's a Helm chart with version 1.3.0 that accompanies that version.


## Step 1. Define the authentication method for the agent
{: #agent-helm-os-deploy-step1}

Choose the type of identity and the authentication method for the agent. Then, create a trusted profile or an API key. The role that is required for sending logs to {{site.data.keyword.logs_full_notm}} is `Sender`.

You can use a service ID or a trusted profile as the identity that is used by the agent to authenticate with the {{site.data.keyword.logs_full}} service. For more information, see [Granting IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-permissions).

Choose one of the following options:

### Option 1: Authentication using a trusted profile
{: #agent-helm-os-deploy-step1-tp}

Create a Trusted Profile. For more information, see [Generating a Trusted Profile for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-trusted-profile).

### Option 2: Authentication using a service ID API key
{: #agent-helm-os-deploy-step1-key}

Generate an API Key for service ID authentication. For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-iam-ingestion-serviceid-api-key).


## Step 2. Configuring the Helm chart values file for the {{site.data.keyword.agent}}
{: #agent-helm-os-deploy-step2}

Complete the following steps:

1. Create a file named `logs-values.yaml` with the following content:

    This file contains the configurations that are specific to your deployment.{: note}

    ```yaml
    metadata:
      name: "logs-agent"
    image:
      version: "1.4.0"  # required

    clusterName: "ENTER_CLUSTER_NAME"     # Enter the name of your cluster. This information is used to improve the metadata and help with your filtering.

    # enableMultiline: true   # Set to true to enable multiline support for applications, like Java or Python, where errors and stack traces can span several lines, and each line is sent as a separate log entry.

    env:
      # ingestionHost is a required field. For example:
      # ingestionHost: "<logs instance>.ingress.us-east.logs.cloud.ibm.com"
      ingestionHost: "" # required

      # If you are using private CSE proxy, then use port number "3443"
      # If you are using private VPE Gateway, then use port number "443"
      # If you are using the public endpoint, then use port number "443"
      ingestionPort: "" # required

      iamMode: "TrustedProfile"
      # trustedProfileID - trusted profile id - required for iam trusted profile mode
      trustedProfileID: "Profile-yyyyyyyy-xxxx-xxxx-yyyy-zzzzzzzzzzzz" # required if iamMode is set to TrustedProfile

    scc:
      # true here enables creation of Security Context Constraints in Openshift
      create: true
    ```
    {: codeblock}

2. Update the fields in the yaml file with values specific to your environment.

    | Field Name | Description |
    |------------|-------------|
    | `image.version` | The version of the agent to be deployed [see Step 1](#agent-helm-os-deploy-step1) |
    | `clusterName`  | The name of the cluster - this will introduce the tag `kubernetes.cluster_name` into all log lines |
    | `env.ingestionHost` | The public or private ingress endpoint for the {{site.data.keyword.logs_full_notm}} instance to receive the logs |
    | `env.ingestionPort` | The ingress endpoint port  \n Public ingress endpoint = `443`  \n Private ingress endpoint(VPE) = `443`  \n Private ingress endpoint(CSE) = `3443` |
    | `env.iamMode` | `TrustedProfile` or `IAMAPIKey` based on the authentication method chosen in [Step 1](#agent-helm-os-deploy-step1) |
    | `env.trustedProfileID` | If `iamMode` is `TrustedProfile` then provide the Trusted Profile ID, otherwise this is not required (for example: `Profile-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` ). |
    | `env.iamEnvironment` | Dictates the correct IAM authentication endpoint. Valid values are `Production`, `PrivateProduction`, or `Custom`. If omitted, the default value is `Production`.|
    | `env.iamHost` | If `iamEnvironment` is `Custom`, then provide the IAM host (for example: `private.eu-de.iam.cloud.ibm.com`), otherwise this is not required. |
    | `scc.create` | Set to `true` in order to create the security constraints in Openshift |
    {: caption="Helm chart required parameters" caption-side="bottom"}

## Step 3. Install the Helm chart
{: #agent-helm-os-deploy-deploy-step3a}

If you are using the `iamMode` as `IAMAPIKey` then the apikey needs to be present in a Kubernetes secret named `logs-agent` with the key name `IAM_API_KEY`.  The secret can be created using the Helm chart by including the `--set secret.iamAPIKey=<your iamAPIKey>` option when running the helm install.  If the secret has been created manually or if you are using `iamMode=TrustedProfile` then do not include this option.
{: important}

Complete the following steps:

1. Log in to the cluster.

    {{site.data.keyword.openshiftlong_notm}} is integrated with IBM Cloud Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the Red Hat OpenShift console, your IAM identity is used to generate a Red Hat OpenShift login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the `oc login` command. For more information, see [Accessing Red Hat OpenShift clusters](/docs/openshift?topic=openshift-access_cluster#access_automation).

    For example, complete the steps in [Using a service ID to log in to clusters](/docs/openshift?topic=openshift-access_cluster#access_service_id) to log in to your cluster.

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

3. Perform a Helm dry run to see the resources that will be created by the Helm chart.

    If you are using the `iamMode`=`TrustedProfile` then the complete command is:

    ```sh
    helm install <install-name> --dry-run oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version> --values <PATH>/logs-values.yaml -n ibm-observe --create-namespace
    ```
    {: codeblock}

    If you are using the `iamMode`=`IAMAPIKey` then the complete command is:

    ```sh
    helm install <install-name> --dry-run oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version> --values <PATH>/logs-values.yaml -n ibm-observe --create-namespace --set secret.iamAPIKey=<APIKey-value> --hide-secret
    ```
    {: codeblock}

    where:

    - `<install-name>` is the name of the Helm installation (`logs-agent`)
    - `<chart-version>` is the version of the helm chart. The Helm chart version should match the agent image version. For more information, see [Helm chart versions](/docs/cloud-logs?topic=cloud-logs-agent-helm-template-clusters).
    - `<PATH>` is the directory path where the `logs-values.yaml` file is located.
    - `<APIKey-value>` is the IAM apikey associated with the ServiceID [setup in Step 1](#agent-helm-os-deploy-step1)
    - Add `--hide-secret` to hide the API key from showing in the output data after the command runs.

    If you would like to inspect the helm chart contents locally, you can download the helm chart to your computer using the command: `helm pull oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version>`.  The downloaded tgz file contains the chart contents.
    {: tip}

    For example, you can run the following command from the directory where the `logs-values.yaml` file is available:


    ```sh
    helm install logs-agent --dry-run oci://icr.io/ibm/observe/logs-agent-helm --version 1.5.0 --values ./logs-values.yaml -n ibm-observe --create-namespace --set secret.iamAPIKey=<secret> --hide-secret
    ```
    {: codeblock}




4. Once the resources to be created are verified, then run the Helm install without the `--dry-run` option

     If you are using the `iamMode`=`TrustedProfile` then the complete command is:

     ```sh
    helm install <install-name>  oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version> --values <PATH>/logs-values.yaml -n ibm-observe --create-namespace
    ```
    {: codeblock}

    If you are using the `iamMode`=`IAMAPIKey` then the complete command is:

    ```sh
    helm install <install-name> oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version> --values <PATH>/logs-values.yaml -n ibm-observe --create-namespace --set secret.iamAPIKey=<APIKey-value>
    ```
    {: codeblock}

    where:

    - `<install-name>` is the name of the Helm installation (`logs-agent`)
    - `<chart-version>` is the version of the helm chart. The Helm chart version should match the agent image version. For more information, see [Helm chart versions](/docs/cloud-logs?topic=cloud-logs-agent-helm-template-clusters).
    - `<PATH>` is the directory path where the `logs-values.yaml` file is located.
    - `<APIKey-value>` is the IAM apikey associated with the ServiceID [setup in Step 1](#agent-helm-os-deploy-step1)


## Step 4. Verify the agent is successfully deployed
{: #agent-helm-os-deploy-deploy-step4}

When the agent is deployed, check the following resources are created:
- The `ibm-observe` namespace.

    To list the namespaces in the cluster, run the following command:

    ```sh
    oc get namespace
    ```
    {: codeblock}

    You can also run the following command to search for the `ibm-observe` namespace:

    ```sh
    oc get namespace | grep ibm-observe
    ```
    {: codeblock}

- A config map `logs-agent` in the namespace `ibm-observe`.

    Run the following command to view the agent config details.

    ```sh
    oc get configmap logs-agent -n ibm-observe
    ```
    {: codeblock}

    You can also use the following command:

    ```sh
    oc describe configmaps logs-agent -n ibm-observe
    ```
    {: codeblock}

- A daemonset `logs-agent` in the namespace `ibm-observe`.

    Run the following command to view the daemonset:

    ```sh
    oc get ds -n ibm-observe
    ```
    {: codeblock}

- Retrieve the list of agent pods by using the following command:

    ```sh
    oc get pods -n ibm-observe -o wide
    ```
    {: pre}

    ```text
    NAME                  READY   STATUS    RESTARTS   AGE    IP              NODE           NOMINATED NODE   READINESS GATES
    logs-agent-4lwvt      1/1     Running   0          2d5h   172.17.61.181   192.168.16.4   <none>           <none>
    logs-agent-g7z87      1/1     Running   0          2d5h   172.17.0.48     192.168.32.4   <none>           <none>
    logs-agent-nw56s      1/1     Running   0          2d5h   172.17.32.232   192.168.0.10   <none>           <none>
    ```
    {: screen}

    The `READY` column shows `1/1` for all pods, with a `STATUS` of `Running`. Verify that an agent pod is ready for each node in your cluster.

    To check how many workers are available in your cluster, you can run the following command:

    ```sh
    oc get nodes
    ```
    {: codeblock}

    ```text
    NAME           STATUS   ROLES           AGE   VERSION
    192.168.0.10   Ready    master,worker   8d    v1.20.0+558d959
    192.168.32.4   Ready    master,worker   8d    v1.20.0+558d959
    192.168.16.4   Ready    master,worker   8d    v1.20.0+558d959
    ```
    {: screen}

    The number of items in each of these two lists need to be the same, and you can match the IP addresses in the node names with the values in the `NODE` column of the pod listing.

    If your nodes are not named by their IP, you can append the `-o wide` option and compare the values in the `INTERNAL-IP` column instead.

    To view the logs of a pod, run `oc logs <POD_NAME>> -n ibm-observe`{: tip}

## Step 5. Verify logs are being delivered to your target destination
{: #agent-helm-os-deploy-deploy-step5}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view. The {{site.data.keyword.agent}} tags log records with a kubernetes object that includes the cluster name.

    ```text
    kubernetes.cluster_name:<CLUSTER_NAME>
    ```
    {: codeblock}

    You can run the query `kubernetes.cluster_name:<YOUR_CLUSTER_NAME>` in your {{site.data.keyword.logs_full_notm}} instance to search for logs that are generated by your cluster.

## Step 6. Configure kube auditing
{: #agent-helm-os-deploy-deploy-step6}


{{../_include-segments/kube-config.md}}

For more information about the `input-kubernetes.conf` file, see [Configuring whether logs are included or excluded](/docs/cloud-logs?topic=cloud-logs-configure-include-exclude).
