---

copyright:
  years:  2024, 2025
lastupdated: "2025-11-13"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# MongoDB extension
{: #extensions-mongodb}

In {{site.data.keyword.logs_full_notm}}, you can use the MongoDB extension to gain security insights using the logs that are generated in an {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

MongoDB is a source-available, cross-platform, document-oriented database program. Classified as a NoSQL database product, MongoDB utilizes JSON-like documents with optional schemas.

## What this extension deploys
{: #extensions-mongodb-deploys}

This extension includes one or more items.

| Includes | Number |
|----------|--------|
| [Alerts](/docs/cloud-logs?topic=cloud-logs-alerts) | 8 |
| [Dashboards](/docs/cloud-logs?topic=cloud-logs-about_dashboards) | 5 |
| [Enrichments](/docs/cloud-logs?topic=cloud-logs-enriching-data) | 0 |
| [Events to metrics](/docs/cloud-logs?topic=cloud-logs-configure-event2metrics) | 5 |
| [Rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) | 1 |
| [Views](/docs/cloud-logs?topic=cloud-logs-custom_views) | 0  |
{: caption="Items included when extension is deployed" caption-side="bottom"}

Before deploying this extension, make sure that deploying the extension will not cause you to exceed [limits for your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-limits). If deploying the extension results in limits being exceeded, the deployment will fail.
{: tip}

## Deploying the extension
{: #extensions-mongodb-deploy}

You can deploy this extension in any {{site.data.keyword.logs_full_notm}} instance that collects MongoDB logs. The MongoDB extension includes security alerts and custom dashboards that provide insights into various components of MongoDB.

For more information about deploying the extension, see [Deploying, managing, and removing {{site.data.keyword.logs_full_notm}} extensions](/docs/cloud-logs?topic=cloud-logs-extensions-mgmt).


{{/_include-segments/extensions-validate.md}}

## Dashboard
{: #extensions-mongodb-dashboards}

Five dashboards are provided providing data about MongoDB logs.

### MongoDB - Client Metadata Overview
{: #extensions-mongodb-db1}

This dashboard provides an overview of MongoDB client metadata. The dashboard includes:

* Client metadata connections over time by context
* Total unique client metadata connections
* Latest activity
* Top source IPs
* Source country distribution
* Top application names
* Driver names and versions
* Platform distribution
* OS architecture distribution


### MongoDB - Access Overview
{: #extensions-mongodb-db2}

This dashboard provides an overview of the access component, authentication, and authorization activity in MongoDB. The dashboard includes:

* Access activity over time by message
* Successful authentication
* Failed authentication
* Failed authorization
* Authentication DB distribution
* Authentication mechanism distribution
* Speculative authentication status distribution
* Latest successful authentication events
* Latest failed authentication events

### MongoDB - General Overview
{: #extensions-mongodb-db3}

This dashboard provides a general overview of MongoDB activity over all components. This dashboard includes:

* Events by components
* Last activity
* Top-10 messages
* Top source IPs
* Distribution of source countries
* Distribution of events per component

### MongoDB - Network Overview
{: #extensions-mongodb-db4}

This dashboard provides an overview of network component activity. The dashboard includes:

* Network events over time
* Connection count over time
* Connection count
* Source country distribution
* Latest activity
* Top source IPs
* Top-10 messages


### MongoDB - Other Components Overview
{: #extensions-mongodb-db5}

This dashboard provides an overview of the `SHARDING`, `STORAGE`, and `CONTROL` MongoDB components. The dashboard includes:

* Events over time by component
* `SHARDING` events by context
* Last `SHARDING` messages
* Top `SHARDING` messages
* `STORAGE` events by context
* Last `STORAGE` messages
* Top `STORAGE` messages
* `CONTROL` events by context
* Last `CONTROL` messages
* Top `CONTROL` messages

## Alerts
{: #extensions-mongodb-alerts}

You can deploy any of the following alerts:

* `MongoDB - Possible Brute Force Detected`: This alert will trigger when receiving a MongoDB `ACCESS` log indicating a series of failed authentication attempts originating from different users in a short period of time.

* `MongoDB - Authentication Succeeded for Same User from different IPs`: This alert will trigger when receiving a MongoDB `ACCESS` log indicating a successful authentication was made for the same user from different IP in a short period of time (impossible traveler scenario).

* `MongoDB - Authentication Succeeded from Public IP`: This alert will trigger when receiving a MongoDB `ACCESS` log indicating a successful authentication being made from a public IP.

* `MongoDB - Authentication Failed`: This alert will trigger when a MongoDB `ACCESS` log indicating a failed authentication attempt is receive.

* `MongoDB - Checking Authorization Failed`: This alert will trigger when a MongoDB `ACCESS` log indicating a that an authorization check failed is detected.

* `MongoDB - Fatal Event Detected`: This alert will trigger when a MongoDB log with a `Severity level` of `Fatal` is detected. See the [MongoDB documentation](https://www.mongodb.com/docs/manual/reference/log-messages/#std-label-log-severity-levels){: external} for information about the MongoDB log severity levels.

* `MongoDB - Error Event Detected`: This alert will trigger when a MongoDB log with a `Severity level` of `Error` is detected. See the [MongoDB documentation](https://www.mongodb.com/docs/manual/reference/log-messages/#std-label-log-severity-levels){: external} for information about the MongoDB log severity levels.

* `MongoDB - Warning Event Detected`: This alert will trigger when a MongoDB log with a `Severity level` of `Warning` is detected. See the [MongoDB documentation](https://www.mongodb.com/docs/manual/reference/log-messages/#std-label-log-severity-levels){: external} for information about the MongoDB log severity levels.

## Rules
{: #extensions-mongodb-rules}

One rule is provided to extract IP and port information from the log message.

## Events to metrics
{: #extensions-mongodb-e2m}

You can deploy any of the following events to metrics configurations. For details about the created metrics, see the events to metrics definitions.

These events to metrics configurations are used by the extension dashboards. If a dashboard is missing data, make sure the event to metrics configuration is deployed and working correctly for your environment.

* `MongoDB_Access_Metrics`
* `MongoDB_General_Metrics`
* `MongoDB_Client_Metadata_Metrics`
* `MongoDB_Network_Metrics`
* `MongoDB_Other_Component_Metrics`
