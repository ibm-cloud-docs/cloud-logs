---

copyright:
  years:  2024, 2025
lastupdated: "2025-11-13"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# NGINX extension
{: #extensions-nginx}

In {{site.data.keyword.logs_full}}, you can use the NGINX extension to gain insights into your nginx logs.
{: shortdesc}

## Before you begin
{: #extensions-nginx-overview}

With this extension, you can create a dashboard designed to visualize and analyze logs from nginx instances.

When deploying the extension you will need to select:

- `applicationName`: The application name is the environment that produces and sends logs to {{site.data.keyword.logs_full_notm}}.
- `subsystemName`: The subsystem name is the service or application that produces and sends logs to {{site.data.keyword.logs_full_notm}}.


## What this extension deploys
{: #extensions-activity-tracking-deploys}

This extension includes one or more items.

| Includes | Number |
|----------|--------|
| [Alerts](/docs/cloud-logs?topic=cloud-logs-alerts) | 8 |
| [Dashboards](/docs/cloud-logs?topic=cloud-logs-about_dashboards) | 1 |
| [Enrichments](/docs/cloud-logs?topic=cloud-logs-enriching-data) | 0 |
| [Events to metrics](/docs/cloud-logs?topic=cloud-logs-configure-event2metrics) | 1 |
| [Rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) | 1 |
| [Views](/docs/cloud-logs?topic=cloud-logs-custom_views) | 0  |
{: caption="Items included when extension is deployed" caption-side="bottom"}

Before deploying this extension, make sure that deploying the extension will not cause you to exceed [limits for your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-limits). If deploying the extension results in limits being exceeded, the deployment will fail.
{: tip}

## Deploying the extension
{: #extensions-nginx-deploy}

You can deploy this extension in any {{site.data.keyword.logs_full_notm}} instance that collects nginx logs. This extension includes a set of pre-configured resources that help you monitor critical metrics, identify anomalies, and optimize your system's performance.

For more information about deploying the extension, see [Deploying, managing, and removing {{site.data.keyword.logs_full_notm}} extensions](/docs/cloud-logs?topic=cloud-logs-extensions-mgmt).


{{/_include-segments/extensions-validate.md}}

## Parsing rule
{: #extensions-nginx-rules}

You can use the provided parsing rule to parse and extract log data to prepare for monitoring and analysis.

This extension assumes a certain structure for nginx logs. After deploying this extension you might need to change the deployed parsing rule. Make sure you keep the same fields names for the equivalent text values. For example, `client_ip` for the client, `status_code` for the request status, `request_uri` for the request url, `user_agent` for the actual user agent within the request, and so on.
{: important}

The parsing rule:

* Parses nginx logs sent as JSON validating and correcting the format.
* Parses unstructured nginx logs into JSON format.
* Extracts the log timestamp into the {{site.data.keyword.logs_full_notm}} JSON timestamp.
* Extracts the nginx `status_code` into the {{site.data.keyword.logs_full_notm}} severity.


## Dashboards
{: #extensions-nginx-dashboards}

One dashboard is provided providing data about nginx logs including:

* Events over time
* Status
* Request methods over time
* Top source IPs
* Top request methods
* Top request methods by status

## Alerts
{: #extensions-nginx-alerts}

You can deploy any of the following alerts:

* `More than usual 4xx responses`
* `Slow HTTP Denial of Service attack (DoS)`: Alerts when a large amount of data is sent slowly in an HTTP POST request.
* `More than usual non-GET/Post requests`
* `A new non-browser user-agent detected`
* `More than usual 5xx responses`
* `High ratio of 5xx responses over 8%`
* `High ratio of 4xx responses over 12%`
* `NGINX - No logs from NGINX`: Alerts if there are no nginx logs in the last 4 hours.

## Events to metrics
{: #extensions-nginx-e2m}

Events to metrics are configured to extract data from `status_code`, `method`, and `client_ip`.

