---

copyright:
  years:  2024
lastupdated: "2024-09-26"

keywords: helm, agent

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Managing the {{site.data.keyword.agent}} for {{site.data.keyword.openshiftlong_notm}} clusters using a Helm chart
{: #agent-helm}

You can use a Helm chart to deploy the {{site.data.keyword.agent}} to collect and route infrastructure and application logs from an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster to an {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

## Deploying the agent
{: #agent-helm-deploy}

Complete the following steps to deploy an agent on an OpenShift cluster:

### Before you begin
{: #agent-helm-deploy-prereqs}

- Make sure you have access to an {{site.data.keyword.openshiftlong_notm}} (`OpenShift`) cluster with permissions to create namespaces and deploy the agent.

- Install the following CLIs:

    - The {{site.data.keyword.cloud_notm}} CLI to log in to the {{site.data.keyword.cloud_notm}} and manage {{site.data.keyword.cloud_notm}} services such as creating an API key.

    - The Openshift CLI to manage the cluster from the command line. [Learn more](/docs/openshift?topic=openshift-cli-install).

    - The latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases)

- Read about [the {{site.data.keyword.agent}}](/docs/cloud-logs?topic=cloud-logs-agent-about).

- Check the agent versions that are available. For more information, see [Checking the available agent versions](/docs/cloud-logs?topic=cloud-logs-check-agent-versions).  Note that the version of the Helm chart will match the version of the agent - for example, if you are using version 1.3.0 of the agent there's a Helm chart with version 1.3.0 that accompanies that version.

### Step 1. Define the authentication method for the agent
{: #agent-helm-deploy-step1}

Choose the type of identity and the authentication method for the agent. Then, create an API key if needed.

Complete the following steps:

1. Choose the type of identity: service ID or trusted profile.

    You can use a service ID or a trusted profile as the identity that is used by the agent to authenticate with the {{site.data.keyword.logs_full}} service.

2. Grant permissions for ingestion to the identity that you have chosen.

    The role that is required for sending logs to {{site.data.keyword.logs_full_notm}} is `Sender`.

    For more information, see [Setting up IAM permissions for ingestion](/docs/cloud-logs?topic=cloud-logs-agent-iam-permissions).

3. Generate an API Key for service ID authentication.

    For authentication with trusted profiles, this step is not required.

    For more information, see [Generating an API Key for ingestion](/docs/cloud-logs?topic=cloud-logs-api-key).


### Step 2. Configuring the Helm chart values file for the {{site.data.keyword.agent}}
{: #agent-helm-deploy-step2}

Complete the following steps:

1. Create a file named `logs-values.yaml` with the content below.  This file contains the configurations that are specific to your deployment.

```yaml
metadata:
  name: "logs-agent"
image:
  version: "1.3.0"  # required

clusterName: "" # recommended to improve the metadata

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
  trustedProfileID: "" # required if iamMode is TrustedProfile

scc:
  # true here enables creation of Security Context Constraints in Openshift
  create: true
```
{: codeblock}

2. Update the fields in the yaml file with values specific to your environment.

| Field Name | Description |
|------------|-------------|
| `image.version` | the version of the agent to be deployed [see Step 1](#agent-helm-deploy-step1) |
| `clusterName`  | the name of the cluster - this will introduce the tag `kubernetes.cluster_name` into all log lines |
| `env.ingestionHost` | the public or private ingress endpoint for the {{site.data.keyword.logs_full_notm}} instance to receive the logs |
| `env.ingestionPort` | the ingress endpoint port \nPublic ingress endpoint = `443`\nPrivate ingress endpoint(VPE) = `443`\n Private ingress endpoint(CSE) = `3443` |
| `iamMode` | `TrustedProfile` or `IAMAPIKey` based on the authentication method chosen in [Step 1](#agent-helm-deploy-step1) |
| `trustedProfileID` | If `iamMode` is `TrustedProfile` then provide the Trusted Profile ID, otherwise it's not required (for example: `Profile-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` ) |
| `scc.create` | set to `true` in order to create the Security Constraints in Openshift |
{: caption="Table 1. Helm chart required parameters" caption-side="bottom"}

### Step 3. Install the Helm chart
{: #agent-helm-deploy-step3a}

If you are using the `iamMode` as `IAMAPIKey` then the apikey needs to be present in a Kubernetes secret named `logs-agent` with the key name `IAM_API_KEY`.  The secret can be created using the Helm chart by including the `--set secret.iamAPIKey=<your iamAPIKey>` option when running the helm install.  If the secret has been created manually or if you are using `iamMode=TrustedProfile` then do not include this option.
{:important}

Complete the following steps:

1. Log in to the cluster.

    {{site.data.keyword.openshiftlong_notm}} is integrated with IBM Cloud Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the Red Hat OpenShift console, your IAM identity is used to generate a Red Hat OpenShift login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the `oc login` command. For more information, see [Accessing Red Hat OpenShift clusters](/docs/openshift?topic=openshift-access_cluster#access_automation).

    For example, complete the steps in [Using a service ID to log in to clusters](/docs/openshift?topic=openshift-access_cluster#access_service_id) to log in to your cluster.

2. Perform a Helm dry run to see the resources that will be created by the helm chart.

    ```sh
    helm install <install-name> --dry-run oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version> -f ./logs-values.yaml -n ibm-observe --create-namespace
    ```
    {: codeblock}

    where:

    - `<install-name>` is the name of the helm installation (ie. `logs-agent`)
    - `<chart-version>` is the version of the helm chart (which should match the image version)

    If you are using the `iamMode`=`IAMAPIKey` then the complete command is:

    ```sh
    install <install-name> --dry-run oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version> -f ./logs-values.yaml -n ibm-observe --create-namespace --set secret.iamAPIKey=<APIKey-value>
    ```
    {: codeblock}

    where:

    - `APIKey-value` is the IAM apikey associated with the ServiceID [setup in Step 1](#agent-helm-deploy-step1)

    If you would like to inspect the helm chart contents locally, you can download the helm chart to your computer using the command: `helm pull oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version>`.  The downloaded tgz file contains the chart contents.
    {: tip}


3. Once the resources to be created are verified, then run the Helm install without the `--dry-run` option

    ```sh
    helm install <install-name> oci://icr.io/ibm/observe/logs-agent-helm --version <chart-version> -f ./logs-values.yaml -n ibm-observe --create-namespace
    ```
    {: codeblock}


### Step 4. Verify the agent is successfully deployed
{: #agent-helm-deploy-step4}

When the agent is deployed, check the following resources are created:
- The `ibm-observe` namespace.

    Run `oc get namespace` to list the namespaces in the cluster. You can also run `oc get namespace | grep ibm-observe` to search for the `ibm-observe` namespace.

- A config map `logs-agent` in the namespace `ibm-observe`.

    Run `oc get configmap logs-agent -n ibm-observe` to view the agent config details. You can also use `oc describe configmaps logs-agent -n ibm-observe`.

- A daemonset `logs-agent` in the namespace `ibm-observe`.

    Run `oc get ds -n ibm-observe` to view the daemonset.

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

    ```text
    NAME           STATUS   ROLES           AGE   VERSION
    192.168.0.10   Ready    master,worker   8d    v1.20.0+558d959
    192.168.32.4   Ready    master,worker   8d    v1.20.0+558d959
    192.168.16.4   Ready    master,worker   8d    v1.20.0+558d959
    ```
    {: screen}

    The number of items in each of these two lists need to be the same, and you can match the IP addresses in the node names with the values in the `NODE` column of the pod listing.

    If your nodes are not named by their IP, you can append the `-o wide` option and compare the values in the `INTERNAL-IP` column instead.


### Step 5. Verify logs are being delivered to your target destination
{: #agent-helm-deploy-step5}

Complete the following steps:

1. [Go to the web UI for your {{site.data.keyword.logs_full_notm}} instance.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. When your agent is correctly configured, you can see logs through the default dashboard view. The {{site.data.keyword.agent}} tags log records with a kubernetes object that includes the cluster name.

    ```text
    kubernetes.cluster_name:<CLUSTER_NAME>
    ```
    {: codeblock}

    You can run the query `kubernetes.cluster_name:<YOUR_CLUSTER_NAME>` in your {{site.data.keyword.logs_full_notm}} instance to search for logs that are generated by your cluster.


## Uninstalling the agent
{: #agent-helm-remove}

Complete the following steps to remove a {{site.data.keyword.agent}}:

1. Log in to the cluster.

    {{site.data.keyword.openshiftlong_notm}} is integrated with IBM Cloud Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the Red Hat OpenShift console, your IAM identity is used to generate a Red Hat OpenShift login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the oc login command. For more information, see [Accessing Red Hat OpenShift clusters](/docs/openshift?topic=openshift-access_cluster#access_automation).

    For example, complete the steps in [Using a service ID to log in to clusters](/docs/openshift?topic=openshift-access_cluster#access_service_id) to log in to your cluster.

2. Run the helm uninstall to remove the resources created by the Helm chart

   ```sh
   helm uninstall <install-name>
   ```
   {: codeblock}

    where:

    - `<install-name>` is the name of the helm installation (ie. `logs-agent`)


## Helm Chart Configuration Options
{: #agent-helm-chart-options}

This table contains a list of all of the parameters that can be provided in the values.yaml file to adjust the agent configurations.

| Parameter | Description | Default |
|-----------|-------------|---------|
| metadata.name | The name used for all of the Kubernetes resources | required - no default |
| image.version | The version of the agent container image (ie. 1.3.0) | required - no default |
| env.ingestionHost | The Cloud Logs host to send the logs to | required - no default |
| env.ingestionPort | The Cloud Logs port to send the logs to | required - no default |
| env.iamMode | Indicate the IAM authentication mechanism used - `TrustedProfile` or `IAMAPIKey` | required - no default |
| env.trustedProfileID | The Trusted profile to use - required when iamMode=TrustedProfile | optional |
| secret.iamAPIKey | The APIKey used when iamMode=IAMAPIKey - only should be provided via the CLI - see below | optional |
| clusterName | The name of the kubernetes cluster | optional |
| scc.create | When to create the Secure Context Constraints in Openshift | false |
| defaultMetadata.subsystemName | static string to override the subsystemName in Cloud Logs | namespace that generated the log |
| defaultMetadata.applicationName | static string to override the applicationName in Cloud Logs | container name that generated the log |
| resources | Override the kubernetes resources allocated to the logs-agent | See below |
| additionalLogSourcePaths | The path of additional logs beyond the default /var/log/containers/*.log | optional - not set |
| excludeLogSourcePaths | Additional logs that should not be collected by the agent | optional - not set |
| selectedLogSourcePaths | Override /var/log/containers/*.log and only collect logs in these paths | optional - not set |
| includeAnnotations | Instruct the kubernetes plugin to include the container annotations with the log messages | false |
| retryLimit | Limit the number of retries that will be attempted | False - no retry limits |
| loggingLevel | The type of logs that should be reported by the agent itself (debug,info,error) | info |
| additionalMetadata | A list of key/value pair tags that can be added as metadata to every log line | optional - not set |
{: caption="Table 2. Helm chart parameters" caption-side="bottom"}

### env.iamMode
{: #agent-helm-chart-options-iammode}

This option allows you to choose to leverage an IAM APIKey instead of the default Trusted Profile configuration.

If `env.iamMode: "TrustedProfile"` is set, then the `env.trustedProfileID` variable must also be provided.

If `env.iamMode: "IAMAPIKey"` is set, then the configuration expects a secret to be defined that contains an IAM Apikey with permissions.
If the `secret.iamAPIKey` variable is provided on the helm command (ie. `--set secret.iamAPIKey=<your iamAPIKey>`), then the helm chart will create the Kubernetes secret.

Alternatively, you can create the secret ahead of time with the command:

```sh
kubectl create secret generic <helm install-name> -n ibm-observe --from-literal=IAM_API_KEY=<apikey>
```

```yaml
env:
  iamMode: IAMAPIKey
```

### defaultMetadata
{: #agent-helm-chart-options-defaultmetadata}

This section allows the user to override the default subsystemName and applicationName that are used in the environment.
By default, the values are not set and the output plugin will dynamically set the values to:

- subsystemName: the Kubernetes namespace that generated the log
- applicationName: the container name that generated the log

```yaml
defaultMetadata:
  subsystemName: ""
  applicationName: ""
```

### resources
{: #agent-helm-chart-options-resources}

This section allows the user to change the resources that are assigned to the agent container.  By default, the values
shown below are used.  If you need to update any of the values, the entire configuration must be provided even if you
don't update all of the values.

```yaml
resources:
  limits:
    cpu: 500m
    ephemeral_storage: 10Gi
    memory: 3Gi
  requests:
    cpu: 100m
    ephemeral_storage: 2Gi
    memory: 1Gi
```

### Log Source Paths configurations
{: #agent-helm-chart-options-log-source-paths}

The following additional variables can be provided to include, exclude or restrict the set of logs to be processed.

By default the agent will collect the logs from `/var/log/containers/*.log`.

- `additionalLogSourcePaths` adds locations to the default set of logs that will be processed.
- `excludeLogSourcePaths` ignores logs in the specified locations
- `selectedLogSourcePaths` overrides the default and ignores the additionalLogSourcePaths configurations

```yaml
# comma separated list, for example “/var/log/abc/*.log,/var/log/xyz/*.log”
additionalLogSourcePaths: ""
excludeLogSourcePaths: ""
selectedLogSourcePaths: ""
```

### iamEnvironment
{: #agent-helm-chart-options-iam-env}

This configurations controls the IAM endpoint used by the agent to exchange the tokens.  The default value of `Production` will be appropriate for most customers.

Valid values are :

- `Production` : `iam.cloud.ibm.com` (default)
- `ProductionPrivate` : `private.iam.cloud.ibm.com`

```yaml
iamEnvironment: "Production"
```

### includeAnnotations
{: #agent-helm-chart-options-include-annotations}

This configuration changes the setting for the Kubernetes filter to include the annotations from Kubernetes with the log records.  The default value for this setting is `false`.

```yaml
includeAnnotations: true
```

### retryLimit
{: #agent-helm-chart-options-retrylimit}

This configuration places a limit on the number of times the agent will retry sending if an error occurs that is considered to be retryable.  The default is False.  See the [Fluentbit documentation about retries](https://docs.fluentbit.io/manual/administration/scheduling-and-retries) to understand the implications of setting this value.  In some situations this setting could lead to log data being discarded by the agent due to the inability to send.

```yaml
retryLimit: 8
```

### additionalMetadata
{: #agent-helm-chart-options-additional-metadata}

This is a list of key/value pairs that will be added under the `meta` object to permit additional tags

```yaml
additionalMetadata:
  region: ca-tor
  env: production
```

The above example will result in the following additional fields added to each log line in Cloud Logs:

```json
{
  "meta": {
    "region": "ca-tor",
    "env": "production"
  }
}
```
