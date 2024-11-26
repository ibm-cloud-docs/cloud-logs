---

copyright:
  years:  2024
lastupdated: "2024-11-26"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



#  Sending logs by using the API
{: #send-logs-api}

You can send logs to an {{site.data.keyword.logs_full_notm}} instance by using the ingestion API.
{: shortdesc}


## Authenticate by using a bearer token
{: #send-logs-token}
{: step}

You must get an {{site.data.keyword.iamlong}} (IAM) access token to authenticate your requests.

To obtain your token by using the IBM Cloud CLI, complete the following steps:
1. Log in to {{site.data.keyword.cloud_notm}}.

    Make sure the entity with which you log in has the `Sender` role for the {{site.data.keyword.logs_full_notm}} service.

2. Run the following command:

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

3. Place this token in the Authorization header of the HTTP request in the form Bearer <token>.




For example, you can retrieve your IAM bearer token and export it as an environment variable by running the following CLI command:

```sh
export IAM_TOKEN=`ibmcloud iam oauth-tokens --output json | jq -r '.iam_token'`
```
{: pre}

## Send logs by using cURL
{: #send-logs-curl}
{: step}

The following table outlines the endpoint details:

| Detail         | Value |
|----------------|-------|
| `URL`          | `<INSTANCE_ID>.ingress.<REGION>.logs.cloud.ibm.com/logs/v1/singles` |
| `HTTP Method`  | `POST` |
| Header `Content-Type` | `application/json`|
| Header `Authorization` | `Bearer $IAM_TOKEN` |
{: caption="Singles ingestion endpoint details" caption-side="top"}

Where

- `INSTANCE_ID`: GUID of the {{site.data.keyword.logs_full_notm}} instance where you want to send logs.
- `REGION`: Region where the {{site.data.keyword.logs_full_notm}} instance is located.
- `IAM_TOKEN`: [IAM bearer token](#send-logs-token) used to request authorization to seng to logs. The pemission `logs.data.send` is required.


Use the following cURL command to send a log line:

```sh
curl -v --location "<INSTANCE_ID>.ingress.<REGION>.logs.cloud.ibm.com/logs/v1/singles" \
--header "Content-Type: application/json" \
--header "Authorization: $IAM_TOKEN" \
--data '[{
      "applicationName": "ENTER_APPLICATION_NAME",
      "subsystemName": "ENTER_SUBSYSTEM_NAME",
      "severity": "ENTER_SEVERITY",
      "computerName": "ENTER_VALUE",
      "text": ENTER_LOG_LINE,
      "category": "ENTER_VALUE",
      "className": "ENTER_VALUE",
      "methodName": "ENTER_VALUE",
      "threadId": "ENTER_VALUE"
    }]'
```
{: pre}

The following table outlines the JSON objects that you can include per log line in a request:


| Property name      | Property type |  Required	 | More information |
|--------------------|---------------|---------------|-----------|
| `applicationName`	 | `string`	     | Yes         | |
| `subsystemName`    | `string`      | Yes         | |
| `text`             | `string/json` | Yes         | If you are using Ajax or a similar technology, you might need to send the data with JSON.stringify(). |
| `severity`         | `number`	     |  No             | `1 – Debug`  \n `2 – Verbose`  \n `3 – Info`  \n `4 – Warn`  \n `5 – Error`  \n `6 – Critical`  \n If not specified, `1 – Debug` will be used.  |
| `timestamp`        | `number`	     | No              | UTC milliseconds. If not specified the time when the log reaches the gate way will be used. |
| `computerName`     | `string`	     | No              | |
| `category`         | `string`      | No              | |
| `className`        | `string`      | No              | |
| `methodName`	     | `string`      | No              | |
| `threadId`         | `string`	     | No              | |
| `hiResTimestamp`   | `string`      | No              | UTC nanoseconds |
{: caption="Array of JSON objects" caption-side="top"}

If you do not specify `severity`, logs are assigned the severity of `1 – Debug`.
{: note}


You can send up to 2MB per request, which is approximately 3,000 medium-sized logs.
{: note}


For example, you can run the following command to send logs to an instance in the `eu-es` region:

```sh
curl -v --location "https://90d208cc-e1dd-4fb2-a938-358e5996f056.ingress.eu-es.logs.cloud.ibm.com/logs/v1/singles" \
--header "Content-Type: application/json" \
--header "Authorization: $IAM_TOKEN" \
--data '[{
      "applicationName": "cs-rest-test3",
      "subsystemName": "cs-rest-test3",
      "computerName": "computer test3",
      "text": {"key":"value","message":"148.145.31.214 - user [24/Oct/2023:15:54:46 +0000] \"PATCH /maximized/Triple-buffered_Managed/core.hmtl HTTP/1.1\" 400 7074 1.666 \"-\" \"Mozilla/5.0 (Macintosh; PPC Mac OS X 10_6_4 rv:6.0) Gecko/1929-02-10 Firefox/37.0\" \"-\"","countryme":"Italy"},
      "category": "cat-1",
      "className": "class-1",
      "methodName": "method-1",
      "threadId": "thread-1"
    }]'
```
{: pre}

The `-v` option provides verbose output which can help you determine if the command completed successfully or if there were authorization or connectivity issues.
{: tip}
