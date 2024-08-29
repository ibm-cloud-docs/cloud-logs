---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-29"

keywords:

subcollection: logs-router

---

{{site.data.keyword.attribute-definition-list}}

# Configuring two targets of different types
{: #config-2-targets}

To facilitate the migration between two services, {{site.data.keyword.logs_routing_full_notm}} tenants can have two different targets.
Those targets must be of a different type.
For example, one target sending logs to {{site.data.keyword.la_full_notm}} and another one under the same tenant sending the same logs to {{site.data.keyword.logs_full_notm}}.
{: shortdesc}

## Before you begin
{: #2-targets-prereqs}

Be sure that you have completed the following steps:

1. Review [About {{site.data.keyword.logs_routing_full}}](/docs/logs-router?topic=logs-router-about) to understand concepts.

2. Review the [getting started](/docs/logs-router?topic=logs-router-getting-started) to understand configuration steps.

3. Install all prerequisite tools as described in the [getting started](/docs/logs-router?topic=logs-router-getting-started&interface=ui#getting-started-before-you-begin-2).

4. Set up permissions to manage targets in the account. For more information, see [Setting up IAM permissions for managing tenants](/docs/logs-router?topic=logs-router-tenant-iam-permissions).

5. To manage tenants by using the API, check that you can connect to {{site.data.keyword.logs_routing_full_notm}} by using the management API. For more information, see [Enabling connectivity to manage tenants in {{site.data.keyword.logs_routing_full}}](/docs/logs-router?topic=logs-router-tenant-enable-connectivity).

## Creating a tenant with two targets
{: #2-target-create-tenant}

To facilitate the migration between two services, {{site.data.keyword.logs_routing_full_notm}} tenants are enabled to have two different targets.
A tenant cannot have two targets of the same type.

To onboard as a {{site.data.keyword.la_full_notm}} tenant, you must supply information about the destination where you want logs delivered.
See [Retrieving your {{site.data.keyword.la_full_notm}} information](/docs/logs-router?topic=logs-router-onboard-log-analysis-tenant&interface=ui#onboard-log-analysis-tenant-retrieve-information) and [Retrieving your {{site.data.keyword.logs_full_notm}} information](/docs/logs-router?topic=logs-router-onboard-cloud-logs-tenant&interface=ui#onboard-cloud-logs-tenant-retrieve-information).
For a {{site.data.keyword.logs_full_notm}} target, you need to follow the steps for [creating a service to service authorization](/docs/logs-router?topic=logs-router-onboard-cloud-logs-tenant#onboard-cloud-logs-tenant-s2s).


### Creating a tenant with two targets by using the API
{: #2-target-create-tenant-api}
{: api}

To create a new tenant with two targets, use the appropriate [management endpoint URL for the correct region](/docs/logs-router?topic=logs-router-endpoints).


```sh
curl -X POST https://<MANAGEMENT-API-ENDPOINT>:<PORT>/v1/tenants \
-H "Content-Type: application/json" \
-H "Authorization: ${IAM_TOKEN}" \
-H 'IBM-API-Version: CURRENT_DATE' \
--data '{
    "name": "TENANT_NAME",
    "targets": [
        {
            "log_sink_crn": "LOG_SINK_CRN",
            "name": "TARGET_NAME",
            "parameters": {
                "host": "LOG_SINK_INGESTION_ENDPOINT",
                "access_credential": "LOG_SINK_INGESTION_KEY",
                "port": LOG_SINK_PORT
            }
        },
        {
            "log_sink_crn": "LOG_SINK_CRN",
            "name": "TARGET_NAME",
            "parameters": {
                "host": "LOG_SINK_INGESTION_ENDPOINT",
                "port": LOG_SINK_PORT
            }
        }
    ]
}'
```
{: pre}

Where

 `<MANAGEMENT-API-ENDPOINT>` is the {{site.data.keyword.logs_routing_full}} endpoint in the region where you plan to collect logs. For more information, see [Endpoints](/docs/logs-router?topic=logs-router-endpoints). Make sure to use the corresponding port.
- `TENANT_NAME`: Name of the tenant. The name must be unique across all tenants for this account and can be up to 35 characters long.
- `TARGET_NAME`: Name of the target destination. The name must be unique across all targets for this tenant and can be up to 35 characters long.
- `LOG_SINK_INGESTION_KEY`: The ingestion key of the target {{site.data.keyword.la_full_notm}} instance.
- `LOG_SINK_CRN`: CRN of the target instance.
- `LOG_SINK_INGESTION_ENDPOINT`: Full qualified ingestion endpoint for the log-sink.
- `CURRENT_DATE`: Specify the current date to request the latest version of the API. The valid format is `YYYY-MM-DD`. Any date up to the current date can be provided.

The following example shows the creation of a tenant in the `us-east` region by using the public endpoint, and specifying target information for an {{site.data.keyword.la_full_notm}} instance and an {{site.data.keyword.logs_full_notm}} instance which are also in `us-east`:

```sh
curl -X POST "https://management.us-east.logs-router.cloud.ibm.com/v1/tenants" \
--header "Authorization: Bearer TOKEN" \
--header 'Content-Type: application/json' \
--header 'IBM-API-Version: 2024-03-01' \
--data '{
    "name": "my-tenant",
    "targets": [
        {
            "log_sink_crn": "crn:v1:bluemix:public:logdna:us-east:a/3516b8fa0a174a71899f5affa4f18d78:3517d2ed-9429-af34-ad52-34278391cbc8::",
            "name": "my-log-analysis-target",
            "parameters": {
                "host": "logs.us-east.logging.cloud.ibm.com",
                "port": 8080,
                "access_credential": "an-ingestion-secret"
            }
        },
        {
            "log_sink_crn": "crn:v1:bluemix:public:logs:us-east:a/91d1d1e42f9b684df920bbd06461c222:743e3b4f-72bc-4669-9fa6-0e6621d0b232::",
            "name": "my-cloud-logs-target",
            "parameters": {
                "host": "743e3b4f-72bc-4669-9fa6-0e6621d0b232.ingress.us-east.logs.cloud.ibm.com",
                "port": 443
            }
        }
    ]
}'
```
{: pre}

If the creation (onboarding) request was successful, a response that contains your tenant metadata is returned. For example,

```json
{
    "id": "3517d2ed-9429-af34-ad52-34278391cbc8:",
    "created_at": "2023-10-20T18:30:00.143156Z",
    "updated_at": "2023-10-20T18:30:00.143156Z",
    "crn": "crn:v1:bluemix:public:logs-router:eu-de:a/3516b8fa0a174a71899f5affa4f18d78:3517d2ed-9429-af34-ad52-34278391cbc8::",
    "name": "tenant",
    "etag": "\"822b4b5423e225206c1d75666595714a11925cd0f82b229839864443d6c3c049\"",
    "targets": [
         {
            "id": "86432b-66a6-df12-7003-888a21a2b3",
            "log_sink_crn": "crn:v1:bluemix:public:logdna:us-east:a/3516b8fa0a174a71899f5affa4f18d78:3517d2ed-9429-af34-ad52-34278391cbc8::",
            "name": "my-log-analysis-target",
            "etag": "\"c3a43545a7f2675970671ac3a57b8db067a1866b2222e1b950ee8da612e347c6\"",
            "type": "logdna",
            "created_at": "2023-10-20T18:30:00.143156Z",
            "updated_at": "2023-10-20T18:30:00.143156Z",
            "parameters": {
                "host": "logs.us-east.logging.cloud.ibm.com",
                "port": 443
            }
        },
        {
            "id": "97543c-77b7-eg23-8114-999b31a2b3",
            "log_sink_crn": "crn:v1:bluemix:public:logs:us-east:a/91d1d1e42f9b684df920bbd06461c222:743e3b4f-72bc-4669-9fa6-0e6621d0b232::",
            "name": "my-cloud-logs-target",
            "etag": "\"6c73f4bdeea634776867ad6daae7bf203f7772a456c25431d8176c52bc2cc890\"",
            "type": "logs",
            "created_at": "2023-10-20T18:30:00.143156Z",
            "updated_at": "2023-10-20T18:30:00.143156Z",
            "parameters": {
                "host": "743e3b4f-72bc-4669-9fa6-0e6621d0b232.ingress.us-east.logs.cloud.ibm.com",
                "port": 443
            }
        }
    ]
}
```
{: codeblock}

## Adding a second target to an existing tenant
{: #2-target-add-target}
{: api}

It is possible to add a second target to an already existing tenant, if the tenant only contains one target and the new target is of a different type.

### Adding an {{site.data.keyword.la_full_notm}} target to an existing tenant using the API
{: #migration-add-la-target-api}
{: api}

To add a target, you must supply information about the destination where you want your logs delivered.

1. Follow the instructions in [Retrieving your {{site.data.keyword.la_full_notm}} information](/docs/logs-router?topic=logs-router-onboard-log-analysis-tenant&interface=ui#onboard-log-analysis-tenant-retrieve-information).

2. Run the following command to add a target sending logs to {{site.data.keyword.la_full_notm}} to a tenant which already has a target sending logs to {{site.data.keyword.logs_full_notm}}:

   ```sh
   curl -X POST https://<MANAGEMENT-API-ENDPOINT>:<PORT>/v1/tenants/<TENANT-ID>/targets \
   -H "Content-Type: application/json" \
   -H "Authorization: ${IAM_TOKEN}" \
   -H 'IBM-API-Version: CURRENT_DATE' \
   --data '{
           "log_sink_crn": "LOG_SINK_CRN",
           "name": "TARGET_NAME",
           "parameters": {
               "host": "LOG_SINK_INGESTION_ENDPOINT",
               "access_credential": "LOG_SINK_INGESTION_KEY",
               "port": LOG_SINK_PORT
               }
           }'
   ```
   {: pre}

   Where

   - `<MANAGEMENT-API-ENDPOINT>` is the {{site.data.keyword.logs_routing_full}} endpoint in the region where you plan to collect logs. For more information, see [Endpoints](/docs/logs-router?topic=logs-router-endpoints). Make sure to use the corresponding port in `<PORT>`.
   - `<TENANT-ID>`: The ID of your existing tenant where you want to add a target.
   - `TARGET_NAME`: Name of the target destination. The name must be unique across all targets for this tenant and can be up to 35 characters long.
   - `LOG_SINK_INGESTION_KEY`: The ingestion key of the target {{site.data.keyword.la_full_notm}} instance.
   - `LOG_SINK_CRN`: CRN of the target {{site.data.keyword.la_full_notm}} instance.
   - `LOG_SINK_INGESTION_ENDPOINT`: Full qualified ingestion endpoint for the log-sink. You can choose a public or a private ingestion endpoint. For more information, see [{{site.data.keyword.la_full_notm}} ingestion endpoints](/docs/log-analysis?topic=log-analysis-endpoints#endpoints_ingestion_public).
   - `LOG_SINK_PORT`: The corresponding port to the `LOG_SINK_INGESTION_ENDPOINT`.
   - `CURRENT_DATE`: Specify the current date to request the latest version of the API. The valid format is `YYYY-MM-DD`. Any date up to the current date can be provided.

The following shows an example of adding a target in `us-east` using the public endpoint and an existing tenant with ID `97543c-77b7-eg23-8114-999b31a2b3`:

```sh
curl -X POST "https://management.us-east.logs-router.cloud.ibm.com/v1/tenants/97543c-77b7-eg23-8114-999b31a2b3/targets" \
--header "Authorization: Bearer TOKEN" \
--header 'Content-Type: application/json' \
--header 'IBM-API-Version: 2024-03-01' \
--data '{
            "log_sink_crn": "crn:v1:bluemix:public:logdna:us-east:a/3516b8fa0a174a71899f5affa4f18d78:3517d2ed-9429-af34-ad52-34278391cbc8::",
            "name": "my-log-sink",
            "parameters": {
                "host": "logs.us-east.logging.cloud.ibm.com",
                "port": 8080,
                "access_credential": "an-ingestion-secret"
            }
        }'
```
{: pre}

If the creation request was successful, a response that contains your tenant metadata is returned.

### Adding an {{site.data.keyword.logs_full_notm}} target to an existing tenant using the API
{: #migration-add-logs-target-api}
{: api}

To add a target, you must supply information about the destination where you want your logs delivered.
Follow the instructions in: [Retrieving your {{site.data.keyword.logs_full_notm}} information](/docs/logs-router?topic=logs-router-onboard-cloud-logs-tenant&interface=ui#onboard-cloud-logs-tenant-retrieve-information) and [creating a service to service authorization](/docs/logs-router?topic=logs-router-onboard-cloud-logs-tenant#onboard-cloud-logs-tenant-s2s).

Run the following command to add a target sending logs to {{site.data.keyword.logs_full_notm}} to a tenant which already has a target sending logs to {{site.data.keyword.la_full_notm}}:

```sh
curl -X POST https://<MANAGEMENT-API-ENDPOINT>:<PORT>/v1/tenants/<TENANT-ID>/targets \
-H "Content-Type: application/json" \
-H "Authorization: ${IAM_TOKEN}" \
-H 'IBM-API-Version: CURRENT_DATE' \
--data '{
        "log_sink_crn": "LOG_SINK_CRN",
        "name": "TARGET_NAME",
        "parameters": {
            "host": "LOG_SINK_INGESTION_ENDPOINT",
            "port": LOG_SINK_PORT
        }'
```
{: codeblock}

Where

- `<MANAGEMENT-API-ENDPOINT>` is the {{site.data.keyword.logs_routing_full}} endpoint in the region where you plan to collect logs. For more information, see [Endpoints](/docs/logs-router?topic=logs-router-endpoints). Make sure to use the corresponding port in `<PORT>`.
- `<TENANT-ID>`: The ID of your existing tenant where you want to add a target.
- `LOG_SINK_CRN`: CRN of the target {{site.data.keyword.logs_full_notm}} instance.
- `LOG_SINK_INGESTION_ENDPOINT`: Full qualified ingestion endpoint for the log-sink.
- `LOG_SINK_PORT`: The corresponding port to the `LOG_SINK_INGESTION_ENDPOINT`.
- `CURRENT_DATE`: Specify the current date to request the latest version of the API. The valid format is `YYYY-MM-DD`. Any date up to the current date can be provided.

The following shows an example of adding a target in `us-east` using the public endpoint and an existing tenant with ID `97543c-77b7-eg23-8114-999b31a2b3`:

```sh
curl -X POST "https://management.us-east.logs-router.cloud.ibm.com/v1/tenants/97543c-77b7-eg23-8114-999b31a2b3/targets" \
--header "Authorization: Bearer TOKEN" \
--header 'Content-Type: application/json' \
--header 'IBM-API-Version: 2024-03-01' \
--data '{
            "log_sink_crn": "crn:v1:bluemix:public:logs:us-east:a/3516b8fa0a174a71899f5affa4f18d78:3517d2ed-9429-af34-ad52-34278391cbc8::",
            "name": "my-log-sink",
            "parameters": {
                "host": "743e3b4f-72bc-4669-9fa6-0e6621d0b232.ingress.eu-es.logs.cloud.ibm.com",
                "port": 443
                }
        }'
```
{: pre}

If the creation request was successful, a response that contains your tenant metadata is returned.

## Getting tenant information by using the API
{: #2-tenant-get-tenant-api}
{: api}

You can get the information about the complete tenant by following [Getting tenant information by using the API](/docs/logs-router?topic=logs-router-get-tenant&interface=api) or for all tenants in your account as described in [Listing tenants by using the API](/docs/logs-router?topic=logs-router-list-tenants&interface=api).



## Updating one or both targets of the tenant using the API
{: #2-tenant-update-tenant-api}
{: api}

It is possible to update one target at a time.
For more information, follow the documentation on [Updating a target by using the API](/docs/logs-router?topic=logs-router-update-tenant&interface=api).



## Deleting a target using the API
{: #2-tenant-delete-target-api}
{: api}

If your tenant has two targets, you can delete one of them.

You cannot delete all targets because this will result in an empty tenant.

To delete the complete tenant, follow the instruction on [deleting (offboarding) a tenant by using the API](/docs/logs-router?topic=logs-router-offboarding-tenant&interface=api).

Run the following to delete a target from a tenant in the {{site.data.keyword.logs_routing_full_notm}} service:

```sh
curl -X DELETE  https://management.${REGION}.logs-router.cloud.ibm.com/v1/tenants/${TENANT_ID}/targets/${TARGET_ID} \
-H "IBM-API-Version: 2024-03-01" \
-H "Authorization: ${IAM_TOKEN}"
```
{: pre}

Where:

- `IAM_TOKEN` is the IAM token that you must use to authenticate the request.
- `TENANT_ID` defines the ID of the tenant that you are removing which was returned when the service was created (onboarded).
- `TARGET_ID` defines the ID of the target that you are removing which was returned when the service was created (onboarded).
- `REGION` defines the region where your tenant is located.

