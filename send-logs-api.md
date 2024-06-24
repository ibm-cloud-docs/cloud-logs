---

copyright:
  years:  2024
lastupdated: "2024-04-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



#  Sending logs by using the API
{: #send-logs-api}

You can send logs to an {{site.data.keyword.logs_full_notm}} instance by using the ingestion API.
{: shortdesc}

The following table outlines the endpoint details:

| Detail         | Value |
|----------------|-------|
| `URL`          | `<INSTANCE_ID>.ingress.<REGION>.logs.cloud.ibm.com/logs/v1/singles` |
| `HTTP Method`  | `POST` |
| Header `Content-Type` | `application/json`|
| Header `Authorization` | `Bearer $IAM_TOKEN` |
{: caption="Table 1. Singles ingestion endpoint details" caption-side="top"}

Where

- `INSTANCE_ID`: GUID of the {{site.data.keyword.logs_full_notm}} instance where you want to send logs.
- `REGION`: Region where the {{site.data.keyword.logs_full_notm}} instance is located.
- `IAM_TOKEN`: [IAM bearer token](#send-logs-token) used to request authorization to seng to logs. The pemission `logs.data.send` is required.


You can send up to 2MB per request, which is approximately 3,000 medium-sized logs.
{: note}

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
{: caption="Table 2. Array of JSON objects" caption-side="top"}

If you do not specify `severity`, logs are assigned the severity of `1 – Debug`.
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



Where

- `INSTANCE_ID`
- `REGION`
- `IAM_TOKEN` is your [IAM bearer token](#send-logs-token)
- `APPLICATION_NAME`
- `SUBSYSTEM_NAME`
- `COMPUTER_NAME`
- `SEVERITY`
- `MESSAGE`
- `CATEGORY`
- `CLASS`
- `METHOD`
- `THREAD_ID`


The `-v` option provides verbose output which can help you determine if the command completed successfully or if there were authorization or connectivity issues.
{: tip}



```sh
curl -v --location "https://90d208cc-e1dd-4fb2-a938-358e5996f056.ingress.eu-es.logs.cloud.ibm.com/logs/v1/singles" \
--header "Content-Type: application/json" \
--header "Authorization: $IAM_TOKEN" \
--data '[{
      "applicationName": "app2",
      "subsystemName": "cs-rest-test3",
      "computerName": "computer test3",
      "text": "this is a verbose text message",
      "category": "cat-1",
      "className": "class-1",
      "methodName": "method-1",
      "threadId": "thread-1"
    }]'

```
{: pre}

## Retrieving the IAM bearer token
{: #send-logs-token}


You must get an {{site.data.keyword.iamlong}} (IAM) access token to authenticate your requests.

For example, you can retrieve your IAM bearer token and export it as an environment variable by running the following CLI command:

```sh
export IAM_TOKEN=`ibmcloud iam oauth-tokens --output json | jq -r '.iam_token'`
```
{: pre}
