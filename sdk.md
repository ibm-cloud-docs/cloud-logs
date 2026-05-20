---

copyright:
  years:  2024, 2026
lastupdated: "2026-05-20"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud Logs Services Go SDK
{: #sdk}

You can use the {site.data.keyword.logs_full}} GO SDK to programmatically interact with the service.
{: shortdesc}

## Overview
{: #sdk-overview}

You can use the {{site.data.keyword.logs_full_notm}} Go SDK to programmatically interact with the service:

| Service Name	                    | Package Name |
|-----------------------------------|---------|
| [logs](/apidocs/logs-service-api) |	logsv0 |
{: caption="GO SDK for {{site.data.keyword.logs_full_notm}}" caption-side="top"}


## Pre-reqs
{: #sdk-prereqs}

* You must have access to an [IBM cloud](/cloud.ibm.com/registration) account.
* You must An IAM API key to allow SDK to access your account. Create one [here](/cloud.ibm.com/login?redirect=%2Fiam%2Fapikeys).
* Go version 1.19 or above


## Installation
The current version of SDK is 0.7.0.


## Go modules
If your application uses Go modules for dependency management, just add an import for each service that you will use in your application.
Here is an example:

import (
	"github.com/IBM/logs-go-sdk/logsv0"
)


Next run *go build* or *go mod tid* to download and install the new dependencies and update your application's *go.mod* life. In the example above, the *logsv0* part of the import path is the package name associated with the Logs service. See the service table above to find the appropriate package name for the services used by the application.


## *go get command*
Alternatvely, you can use the *go get* command to download and install the packages needed by your application:

```go
go get -u github.com/IBM/logs-go-sdk/logsv0
```
{: codeblock}

Be sure to use the appropriate package name from the service table above for the services used by your application.


## Using the SDK
Examples are given [here] (/github.com/IBM/logs-go-sdk/blob/main/example/v0/README.md). For general SDK usage information, see this [link](/github.com/IBM/ibm-cloud-sdk-common/blob/main/README.md).


## Questions
If you are facing difficulties using this SDK or have a question about the IBM Cloud Services, ask a question at [Stack Overflow](/stackoverflow.com/users/login?ssrc=anon_ask&returnurl=https%3a%2f%2fstackoverflow.com%2fquestions%2fask%3ftags%3dibm-cloud).


## Issues
If you encounter an issue with the project, you can submit a [bug report](/github.com/IBM/logs-go-sdk/issues). Before that, search for similar issues. It is possible that someone has already reported the problem.

## License
This SDK project is released under the Apache 2.0 license. The licensen's full text can be found in [License](/github.com/IBM/logs-go-sdk/blob/main/LICENSE).
