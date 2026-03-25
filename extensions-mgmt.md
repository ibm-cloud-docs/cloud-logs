---

copyright:
  years:  2024, 2026
lastupdated: "2026-03-25"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Managing {{site.data.keyword.logs_full_notm}} extensions
{: #extensions-mgmt}

In {{site.data.keyword.logs_full_notm}}, extensions offer out of the box configurations to manage log data. An extension contains a set of pre-defined resource definitions such as alerts, parsing rules, dashboards, and more that you can use to get up and running fast monitoring and alerting on data that is relevant to the extension.
{: shortdesc}

- You can deploy all resources or a subset of resources of an extension in the context of selected applications and subsystems.
- You can manage an extesion graphically via UI or programmatically via API.
- After you deploy resources from an extension, you can customize them.

    To prevent overwritting custom changes to predefined resources, you must detach these resources from the extension deployment. You can only detach resources graphically via UI.
    {: important}

- Extensions are classified by type. Valid types are `Security`, and `Observability`.

- Extensions include labels that you can use to filter them. For example, the tag `IBM` is associated with extensions that you can use to monitor the {{site.data.keyword.cloud_notm}}.

- Extensions can include predefined alerts, parsing rules, Events to Metrics definitions, dashboards and enrichments.

## List of available extensions
{: #extensions-mgmt-list}

The following list outlines extensions that you can deploy to monitor logs:
- [System Monitoring](/docs/cloud-logs?topic=cloud-logs-extensions-system-monitoring): Use it to get insights into your system's performance and usage of an {{site.data.keyword.logs_full_notm}} instance. 
- [Activity Tracking](/docs/cloud-logs?topic=cloud-logs-extensions-activity-tracking): Use it to get insights into your {{site.data.keyword.cloud_notm}} activity tracking data.
- [{{site.data.keyword.containerlong_notm}}](/docs/cloud-logs?topic=cloud-logs-extensions-kubernetes):  Use it to get insights into your {{site.data.keyword.containerlong_notm}} logs.
- [{{site.data.keyword.databases-for-mysql_full}}](/docs/cloud-logs?topic=cloud-logs-extensions-db-mysql):  Use it to get insights into your {{site.data.keyword.databases-for-mysql_full}} logs.
- [{{site.data.keyword.databases-for-postgresql_full_notm}}](/docs/cloud-logs?topic=cloud-logs-extensions-db-postgresql):  Use it to get insights into your {{site.data.keyword.databases-for-postgresql_full_notm}} logs.

- [{{site.data.keyword.cloudantfull}}](/docs/cloud-logs?topic=cloud-logs-extensions-db-cloudant):  Use it to get insights into your {{site.data.keyword.cloudantfull}} logs.
- [Cloudflare](/docs/cloud-logs?topic=cloud-logs-extensions-cloudflare):  Use it to get insights into your Cloudflare logs.
- [{{site.data.keyword.databases-for-redis_full}}](/docs/cloud-logs?topic=cloud-logs-extensions-db-redis):  Use it to get insights into your {{site.data.keyword.databases-for-redis_full_notm}} logs.
- [Linux](/docs/cloud-logs?topic=cloud-logs-extensions-linux): Use it to get insights into your Linux logs.
- [MongoDB](/docs/cloud-logs?topic=cloud-logs-extensions-mongodb): Use it to get insights into your MongoDB logs.
- [NGINX](/docs/cloud-logs?topic=cloud-logs-extensions-nginx): Use it to get insights into your nginx logs.



## List of available extensions by ID
{: #extensions-mgmt-list-id}

The following table lists the IDs of the extensions that you must use when using the Extensions API:

| Extension                                                  | ID               |
|------------------------------------------------------------|------------------|
| System Monitoring                                          | `SystemMonitoring`    |
| Activity Tracking                                          | `ActivityTracking`    |
| {{site.data.keyword.containerlong_notm}}                   | `IBMCloudKubernetes`   |
| {{site.data.keyword.databases-for-mysql_full}}             | `IBMMySQL`        |
| {{site.data.keyword.databases-for-postgresql_full_notm}}   | `IBMPostgreSQL`   |
| {{site.data.keyword.cloudantfull}}                         | `IBMCloudant`         |
| Cloudflare                                                 | `Cloudflare` |
| {{site.data.keyword.databases-for-redis_full}}             | `IBMRedis` |
| Linux                                                      | `Linux` |
| MongoDB                                                    | `MongoDB` |
| NGINX                                                      | `NGINX` |
{: caption="Extension actions by using the {{site.data.keyword.logs_full_notm}} REST API" caption-side="top"}


## API methods
{: #extensions-mgmt-api}
{: api}

The following table lists the actions that you can run to manage extensions:

| Action                                 | REST API Method  | API_URL                                          |
|----------------------------------------|------------------|--------------------------------------------------|
| List extensions                        | `GET`            | `<ENDPOINT>/v1/extensions`              |
| Get an extension by ID                 | `GET`            | `<ENDPOINT>/v1/extensions/{id}`  |
| Get deployment details of an extension | `GET`            | `<ENDPOINT>/v1/extensions/{id}/deployment`  |
| Deploy an extension                    | `PUT`            | `<ENDPOINT>/v1/extensions/{id}/deployment`  |
| Update an extension                    | `PUT`            | `<ENDPOINT>/v1/extensions/{id}/deployment`  |
| Remove an extension                    | `DELETE`         | `<ENDPOINT>/v1/extensions/{id}/deployment`  |
{: caption="Extension actions by using the {{site.data.keyword.logs_full_notm}} REST API" caption-side="top"}

You can use the public or the private `ENDPOINT` to manage extensions. For more information on the endpoints, see [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).

For more information about the REST API, see [Extensions](/apidocs/logs-service-api#get-extension).
{: note}




## Get the list of available extensions through the UI
{: #determine-extensions-ui}
{: ui}

To see the extensions that are available through the {{site.data.keyword.logs_full_notm}} UI, complete the following steps:

{{site.data.content.launch-ui}}

2. Click the **Integrations** icon ![Integrations icon](/icons/integrations.svg "Integrations") > **Extensions**.

The list of available extensions is displayed.



## Get the list of available extensions by using the API
{: #determine-extensions-api}
{: api}

To get the list of extensions available for deployment, including additional details for the ones that are deployed, complete the following steps:

1. Get the authentication token. See [Authentication via API](/apidocs/logs-service-api#authentication).

2. Get the endpoint of the instance where you want to manage extensions. See [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).

3. List all extensions, including version and deployed resources per extension.

    ```text
    curl -X GET --location --header "Authorization: Bearer ${IAM_TOKEN}"   --header "Accept: application/json"   "https://<API_ENDPOINT>/v1/extensions"
    ```
    {: codeblock}



### Getting the list of deployed extensions by using the API
{: #determine-extensions-api-deployed-api}
{: api}

To get information about the extensions that are deployed in an {{site.data.keyword.logs_full_notm}} instance, you can use the method [Get list of extensions](/apidocs/logs-service-api#get-extensions).

For example, complete the following steps:

1. Get the authentication token. See [Authentication via API](/apidocs/logs-service-api#authentication).

2. Get the endpoint of the instance where you want to deploy an extension. See  see [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).

3. Get details of an deployed extensions.

    ```text
    curl -X GET --location --header "Authorization: Bearer ${IAM_TOKEN}"   --header "Accept: application/json"   "https://<API_ENDPOINT>/v1/extensions?deployed=true"
    ```
    {: codeblock}


### Getting the list of extensions that are not deployed by using the API
{: #determine-extensions-api-undeployed-api}
{: api}

To get information about the extensions that are not yet deployed in an {{site.data.keyword.logs_full_notm}} instance, you can use the method [Get list of extensions](/apidocs/logs-service-api#get-extensions).

For example, complete the following steps:

1. Get the authentication token. See [Authentication via API](/apidocs/logs-service-api#authentication).

2. Get the endpoint of the instance where you want to deploy an extension. See  see [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).

3. Get details of an deployed extensions.

    ```text
    curl -X GET --location --header "Authorization: Bearer ${IAM_TOKEN}"   --header "Accept: application/json"   "https://<API_ENDPOINT>/v1/extensions?deployed=false"
    ```
    {: codeblock}


## Deploying an extension by using the API
{: #extensions-mgmt-deploy-api}
{: api}

To deploy resources included in an extension, you can use the API method [Deploy or update deployment of an extension.](/apidocs/logs-service-api#update-extension-deployment).

Complete the following steps to deploy an extension:

1. Get the authentication token. See [Authentication via API](/apidocs/logs-service-api#authentication).

2. Get the endpoint of the instance where you want to deploy an extension. See  see [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).

3. Get the ID of the extension and that you want to deploy. See [List of available extensions](#extensions-mgmt-list).

4. Get details of an extension by ID including information about deployed resources.

    ```text
    curl -X GET --location --header "Authorization: Bearer ${IAM_TOKEN}"   --header "Accept: application/json"   "https://<API_ENDPOINT>/v1/extensions/<ExtensionID>"
    ```
    {: codeblock}

    For example, to get the information for the Kubernetes extension, run:

    ```text
    curl -X GET --location --header "Authorization: Bearer ${IAM_TOKEN}"   --header "Accept: application/json"   "https://<ENDPOINT>/v1/extensions/IBMCloudKubernetes"
    ```
    {: codeblock}

    You will see a response that looks as follows:

    ```text
    {
    "id": "IBMCloudKubernetes",
    "name": "IBM Cloud Kubernetes Service",
    "revisions": [
        {
            "version": "1.0.0",
            "description": "# IBM Cloud Kubernetes Service\nThe dashboard provides an in-depth analysis of IBM Cloud Kubernetes Service, offering a comprehensive view of cluster performance, node activity, pod logs, and error analysis. It enables quick issue identification, trend analysis, and efficient Kubernetes monitoring.\n",
            "excerpt": "",
            "labels": [
                "IBM",
                "Kubernetes",
                "Сluster",
                "K8S",
                "Cloud",
                "Compute",
                "Observability"
            ],
            "items": [
                {
                    "id": "1405e028-dd50-48a0-86c5-b361e029a3f1",
                    "name": "IBM Kubernetes",
                    "description": "Dashboard for IBM Cloud Kubernetes Service.",
                    "target_domain": "dashboard"
                },
                {
                    "id": "93cda01a-526e-4872-b29a-125645abf784",
                    "name": "IBM Kubernetes - No logs from service",
                    "description": "No logs have been received from the kubernetes service, indicating potential issues with logging configuration, service downtime, or connectivity problems affecting log transmission.",
                    "target_domain": "alert"
                },
                {
                    "id": "9e2099ee-78f4-4070-a1fd-7be109f136ce",
                    "name": "IBM Kubernetes - More than 5 erroneous cluster logs within 15 minutes",
                    "description": "Over five error logs have been recorded at the cluster level within a 15-minute window, indicating potential issues affecting the Kubernetes cluster's overall health or configuration.",
                    "target_domain": "alert"
                },
                {
                    "id": "f242dd8a-138a-4dcc-92b9-09f5ec1b4840",
                    "name": "IBM Kubernetes - More than 5 erroneous pod logs within 15 minutes",
                    "description": "More than five error logs have been detected in pod-level operations within 15 minutes, suggesting issues with workloads or pod-level configurations.",
                    "target_domain": "alert"
                },
                {
                    "id": "504c4f1a-4185-4619-bc7c-9d011b3f3245",
                    "name": "IBM Kubernetes - Host change",
                    "description": "A host change event has been detected, which might indicate a node replacement, scaling operation, or unexpected infrastructure changes.",
                    "target_domain": "alert"
                },
                {
                    "id": "c179c165-b12e-4f40-8e87-e4627d6dbdef",
                    "name": "IBM Kubernetes - Permission denied",
                    "description": "A permission denial has occurred during a Kubernetes operation, possibly caused by misconfigured access controls or insufficient permissions for the requested action.",
                    "target_domain": "alert"
                }
            ]
        }
    ],
    "changelog": [
        {
            "version": "1.0.0",
            "description_md": "### Changed\nRelease of an extension for the IBM Cloud Kubernetes Service.\n"
        }
    ]
    }
    ```
    {: screen}



5. Run the the API call. For example, you can run the following cURL command for the Kubernetes extension that creates a dashboard and 2 alerts:

    ```text
    curl -X PUT --location --header "Authorization: Bearer ${IAM_TOKEN}"   --header "Accept: application/json"   --header "Content-Type: application/json"   --data   '{
    "version": "1.0.0",
    "item_ids": [
      "1405e028-dd50-48a0-86c5-b361e029a3f1",
      "93cda01a-526e-4872-b29a-125645abf784",
      "9e2099ee-78f4-4070-a1fd-7be109f136ce"
    ],
    "applications": [
      "myapp"
    ],
    "subsystems": [
      "mysubsystem"
    ]
  }'   "https://<ENDPOINT>/v1/extensions/IBMCloudKubernetes/deployment"
    ```
    {: codeblock}



## Updating an extension by using the API
{: #extensions-mgmt-update-api}
{: api}

You might want to deploy a new version of an extension, deploy additional resources, or modify the appliations and subsystems that are configured as sources of data relevant to the extension. To update resources that are included in an extension, you can use the API method [Deploy or update deployment of an extension.](/apidocs/logs-service-api#update-extension-deployment).

Complete the following steps to update an extension:

Make sure that you specify in the API call all the resources from that extension that are currently deployed. If you have modified any resources previously deployed from this extension, detach the resources before running the update. If you do not include all resources previously deployed, they ones that are not included are removed.
{: important}

1. Get the authentication token. See [Authentication via API](/apidocs/logs-service-api#authentication).

2. Get the endpoint of the instance where you want to deploy an extension. See  see [Service API endpoints](/docs/cloud-logs?topic=cloud-logs-endpoints_api).

3. Get the ID of the extension and that you want to deploy. See [List of available extensions](#extensions-mgmt-list).

4. Get details of an extension by ID including information about deployed resources. Check the deployment section to see what resources are already deployed.

    ```text
    curl -X GET --location --header "Authorization: Bearer ${IAM_TOKEN}"   --header "Accept: application/json"   "https://<API_ENDPOINT>/v1/extensions/<ExtensionID>"
    ```
    {: codeblock}

5. Run the the API call. For example, you can run the following cURL command for the Kubernetes extension that keeps only the dashboard and 1 alert:

    ```text
    curl -X PUT --location --header "Authorization: Bearer ${IAM_TOKEN}"   --header "Accept: application/json"   --header "Content-Type: application/json"   --data   '{
    "version": "1.0.0",
    "item_ids": [
      "1405e028-dd50-48a0-86c5-b361e029a3f1",
      "93cda01a-526e-4872-b29a-125645abf784",
      "9e2099ee-78f4-4070-a1fd-7be109f136ce"
    ],
    "applications": [
      "myapp"
    ],
    "subsystems": [
      "mysubsystem"
    ]
  }'   "https://<ENDPOINT>/v1/extensions/IBMCloudKubernetes/deployment"
    ```
    {: codeblock}

## Deploying an extension
{: #extensions-mgmt-deploy-ui}
{: ui}

To deploy an extension, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Integrations icon** ![Integrations icon](/icons/integrations.svg "Integrations") > **Extensions**.

4. Click **Deploy** on the tile of the extension you want to deploy.

5. Select the *Applications* and *Subsystems* where the extension will be applied.

6. By default everything defined in the extension will be deployed. You can remove the checkmark for any item you don't want to deploy.

7. Click **+ Deploy** to install the extension in your {{site.data.keyword.logs_full_notm}} instances.


## Modifying a deployed extension dashboard
{: #extensions-mgmt-modify-ui}
{: ui}


After deploying an extension you can change a deployed custom dashboard by [modifying the dashboard](/docs/cloud-logs?topic=cloud-logs-create_dashboards#modify_dashboard).

You can also change the *Applications* and *Subsystems* associated with the deployed extension.

If you have modified assets deployed by the extension (for example, dashboards), make sure that you keep a copy of those assets by editing them and saving them with **Save As** before updating the *Applications* and *Subsystems* associated with the deployed extension. When you update the *Applications* and *Subsystems* values in the extension, all assets are updated with the default extension assets and are associated with the new *Applications* and *Subsystems* values.
{: attention}

Complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Integrations icon** ![Integrations icon](/icons/integrations.svg "Integrations") > **Extensions**.

4. Click the tile of the deployed extension you want to modify.

5. Change the *Applications* and *Subsystems* values as needed.

6. Click **Update**.

## Removing an extension
{: #extensions-mgmt-remov-ui}
{: ui}


To remove an extension you already have deployed in your instance, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Integrations icon** ![Integrations icon](/icons/integrations.svg "Integrations") > **Extensions**.

4. Click the tile of the deployed extension you want to remove.

5. Click **- Remove**.

6. Select if your want to delete or keep the deployed assets.

   If you choose to delete the deployed assets, the extension is deleted along with the assets deployed by the extension in your {{site.data.keyword.logs_full_notm}} instance.

   If you choose to keep the deployed assets when deleting the extension, the assets deployed by the extension will remain in your {{site.data.keyword.logs_full_notm}} instance, but will no longer be associated with the extension. If you deploy the extension again, a new copy of the extension will be deployed and the assets previously deployed will remain in your {{site.data.keyword.logs_full_notm}} instance and will not be overwritten.

7. Click **Remove**.

## Removing an extension
{: #extensions-mgmt-remove-api}
{: api}


To delete an extension, you can run the following API call:

```text
% curl -X DELETE --location --header "Authorization: Bearer ${IAM_TOKEN}"   --header "Accept: application/json"   "https://<ENDPOINT>/v1/extensions/<ExtensionID>/deployment"
```
{: codeblock}
