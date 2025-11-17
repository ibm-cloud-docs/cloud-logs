---

copyright:
  years:  2024, 2025
lastupdated: "2025-11-17"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


# Cloudflare extension
{: #extensions-cloudflare}

In {{site.data.keyword.logs_full_notm}}, you can use the Cloudflare extension to gain security insights using the logs that are generated in an {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

Cloudflare is an internet infrastructure provider that delivers services such as a DNS, a content delivery network (CDN) and many other additional services to make websites faster and more secure. Cloudflare acts as an intermediary between a client and a server, using a reverse proxy to mirror and cache websites. By storing web content for delivery on the closest edge server, it is able to optimize loading times. This intermediary design is also how Cloudflare offers a level of filtration for security. By sitting between the client and the hosting server, it can detect malicious traffic, intercept distributed denial-of-service attacks, deflect attacks from bots, remove bot traffic and limit spam.

Cloudflare audit logs summarize the history of changes made within your Cloudflare account. Audit logs include account level actions such as login and logout, DNS record changes, API token changes, Firewall rule changes and more.

## What this extension deploys
{: #extensions-cloudflare-deploys}

This extension includes one or more items.

| Includes | Number |
|----------|--------|
| [Alerts](/docs/cloud-logs?topic=cloud-logs-alerts) | 51 |
| [Dashboards](/docs/cloud-logs?topic=cloud-logs-about_dashboards) | 3 |
| [Enrichments](/docs/cloud-logs?topic=cloud-logs-enriching-data) | 3 |
| [Events to metrics](/docs/cloud-logs?topic=cloud-logs-configure-event2metrics) | 5 |
| [Rules](/docs/cloud-logs?topic=cloud-logs-log_parsing_rules) | 1 |
| [Views](/docs/cloud-logs?topic=cloud-logs-custom_views) | 0  |
{: caption="Items included when extension is deployed" caption-side="bottom"}

Before deploying this extension, make sure that deploying the extension will not cause you to exceed [limits for your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-limits). If deploying the extension results in limits being exceeded, the deployment will fail.
{: tip}

## Deploying the extension
{: #extensions-cloudflare-deploy}

You can deploy this extension in any {{site.data.keyword.logs_full_notm}} instance that collects Cloudflare logs. The Cloudflare extension includes alerts and dashboards for the following Cloudflare services: `WAF`, `DNS`, and `Audit`.

The Cloudflare `WAF` alerts and dashboards are based on various attack scenarios. Some are based on the Cloudflare **WAF Attack Score** feature, which needs to be enabled based on the Cloudflare service subscription plan. If the feature is not enabled, some related alerts and dashboards will not work since you will not have the relevant logs in the system to be monitored.
{: important}

For more information about deploying the extension, see [Deploying, managing, and removing {{site.data.keyword.logs_full_notm}} extensions](/docs/cloud-logs?topic=cloud-logs-extensions-mgmt).


{{/_include-segments/extensions-validate.md}}

## Dashboard
{: #extensions-cloudflare-dashboards}

Three dashboards are provided providing data about Cloudflare logs.

Dashboards are based on the Events to Metrics feature. The Events to Metrics required are included in this extension but require an [{{site.data.keyword.logs_full_notm}} metrics bucket](/docs/cloud-logs?topic=cloud-logs-configure-metrics-bucket) to be configured for the dashboards to work.
{: requirement}

### Cloudflare WAF Insights
{: #extensions-cloudflare-db1}

This dashboard provides an overview of Cloudflare `WAF` insights. The dashboard includes:

* `WAF` events over time
* `WAF` traffic by top source IPs
* `WAF` traffic by top requested hosts
* `WAF` traffic by top requested URLs
* Security actions taken by `WAF`
* Top `WAF` rules
* Top user agents
* Edge-origin response codes
* Source countries
* `WAF` attack score distribution
* `WAF` `RCE` attack score distribution
* `WAF` `XSS` attack score distribution
* `WAF` `SQLi` attack score distribution

### Cloudflare - DNS - Overview
{: #extensions-cloudflare-db2}

This dashboard provides an overview of Cloudflare `DNS` insights. The dashboard includes:

* `DNS` activity over tie - by colocation
* `DNS` activity over time - by query type
* `DNS` activity over time - by response code
* `DNS` query response code distribution
* `DNS` query type distribution
* Top queried DNS domains
* Top source IPs
* Top source IPs of all DNS queries in the selected timeframe
* Latest DNS queries
* Top A record queried
* Top AAAA record queried
* Top NS record queried
* Top CNAME record queried
* Top MX record queried
* Top TXT record queried

### Cloudflare - Audit - Overview Dashboard
{: #extensions-cloudflare-db3}

This dashboard provides an overview of Cloudflare audit insights. The dashboard includes:

* Audit logs - by resource type
* Top actors
* Resource type distribution
* Latest user activity
* Latest client device activity
* Latest certificate pack activity

## Alerts
{: #extensions-cloudflare-alerts}

You can deploy any of the following alerts.

### WAF alerts
{: #extensions-cloudflare-alerts-waf}

[Enterprise]{: tag-teal} - Alerts with this tag require that your Cloudflare plan be at least at the Enterprise level. These alerts will not trigger for Cloudflare plans less than the Enterprise level.
{: requirement}

* `Cloudflare - WAF - A New Client Request Host Detected`: This alert detects when a new host is requested by the client. This alert will be active (after being deployed) after the configured alert time window which is 7 days. This is so the algorithm can train on the new values for the key tracked, capture the baseline, and prevent false notifications.

* `Cloudflare - WAF - High error ratio of 5xx origin response, over 5% in 30min`: This alert detects when the 5xx origin response error codes exceed 5% of the total count of origin response status codes in 30 minutes. This alert will calculate the ratio between error code 5xx to the overall number of response codes in 30 minutes. If the ratio exceeds 5%, it will be triggered. The origin response indicates that the error response was generated by your origin web server.

* `Cloudflare - WAF - More than usual 5xx edge response errors (at least 10)`: This alert detects when 5xx edge response errors are generated more than the usual number. If the status code exceeds the threshold value of 10 above the usual number, then the alert will be triggered. The 'usual number' is calculated by the algorithm dynamically based on the pattern of the previous 7 days of data. The algorithm takes one week to learn the traffic pattern. The edge response status code is an HTTP response code sent from Cloudflare to the client (end user).

   Since this alert will start alerting only after 1 week of being deployed, users can also make use of the similar alert `Cloudflare - High error ratio of 5xx edge response, over 5% in 30min`. This alert will start alerting on the anomalies right after being deployed.

* `Cloudflare - WAF - More than usual 4xx origin response errors (at least 10)`: This alert detects when 4xx origin response errors are generated more than the usual number. If the status code exceeds the threshold value of 10 above the usual number, then the alert will be triggered. The 'usual number' is calculated by the algorithm dynamically based on the pattern of the previous 7 days of data. The algorithm takes one week to learn the traffic pattern. The origin response status code is an HTTP response code sent from the origin server to Cloudflare.

* `Cloudflare - WAF - More than usual 4xx edge response errors (at least 10)`: This alert detects when 4xx edge response errors are generated more than the usual number. If the status code exceeds the threshold value of 10 above the usual number, then the alert will be triggered. The 'usual number' is calculated by the algorithm dynamically based on the pattern of the previous 7 days of data. The algorithm takes one week to learn the traffic pattern. The edge response status code is an HTTP response code sent from Cloudflare to the client (end user).

   Since this alert will start alerting only after 1 week of being deployed, users can also make use of the similar alert `Cloudflare - High error ratio of 4xx edge response, over 15% in 30min`. This alert will start alerting on the anomalies right after being deployed.

* `Cloudflare - WAF - More than usual 5xx origin response errors (at least 10)`: This alert detects when 5xx origin response errors are generated more than the usual number. If the status code exceeds the threshold value of 10 above the usual number the alert will be triggered. The 'usual number' is calculated by the algorithm dynamically based on the pattern of the previous 7 days of data. The algorithm takes one week to learn the traffic pattern. The origin response indicates that the error response was generated by your origin web server.

   Since this alert will start alerting only after 1 week of being deployed, users can also make use of the similar alert `Cloudflare - High error ratio of 5xx origin response, over 5% in 30min`. This alert will start alerting on the anomalies right after being deployed.

* `Cloudflare - WAF - High Volume of Bot Requests`: This alert detects high volume of bot requests. A bot is an autonomous program on a network that can interact with computer systems or users, imitating or replacing a human user's behavior, and performing repetitive tasks. 

* [Enterprise]{: tag-teal} `Cloudflare - WAF - Potential SQLi Attack`: This alert will trigger when a large number of logs containing Cloudflare WAF SQLi Attack Score values indicate an attack (score between 1 to 20). For more information about the Cloudflare WAF Attack Score, see [WAF attack score](https://developers.cloudflare.com/waf/detections/attack-score/){: external}.

* `Cloudflare - WAF - Possible Information Disclosure`: This alert detects when a successful HTTP GET request (2XX response) targets a URL that ends with a set of specific file extension (such as `txt` files) that can contain information that shouldn't be disclosed directly to the internet.

   The following file extensions are detected by this alert:
   * Configuration files: .env, .config, .ini, .conf
   * Backup files: .bak, .old, .zip
   * Log Ffles: .log, .txt, .log.txt
   * Source code files:  .java, .py, .rb
   * Database dump files: .sql, .dump
   * Backup scripts: .sh, .bat, .ps1
   * Private Keys and Certificates: .pem, .key, .p12, .crt

   This alert might require tuning based on the web application usage (that is, if it serves any of the mentioned file extensions). File extensions can be added or removed and match condition can be tuned to lower or higher rate of occurrence to match the operation of the web application.

* `Cloudflare - WAF - XSS Attack`: This alert detects when a Cross Site Scripting (XSS) attack might take place. Alerting is based on triggered Cloudflare WAF rules that contain a certain set of keywords that represent XSS attacks, over a determined period of time, and in the context of a single IP address.

* `Cloudflare - WAF - SQLi Attack`: This alert detects when an SQL Injection (SQLi) attack might take place. Alerting is based on triggered Cloudflare WAF rules that contain a certain set of keywords that represent SQLi attacks, over a determined period of time, and in the context of a single IP address.

* `Cloudflare - WAF - Remote Code Execution Attack`: This alert detects when a Remote Code Execution (RCE) attack might take place Alerting is based on triggered Cloudflare WAF rules that contain a certain set of keywords that represent RCE attacks, over a determined period of time, and in the context of a single IP address.

* [Enterprise]{: tag-teal} `Cloudflare - WAF - Possible Bypass`: This alert detects, based on specific logic, that might indicate that the Cloudflare WAF is NOT BLOCKING potentially malicious requests.  This alerting is based on Cloudflare WAF Attack Scores indicating an attack.

   The alert will trigger if the WAF Action is "unknown" AND NOT "simulate" AND WAF Attack Score is between 1 and 50, indicating an attack or likely attack.

   For more information about the Cloudflare WAF Attack Score, see [WAF attack score](https://developers.cloudflare.com/waf/detections/attack-score/){: external}.

* `Cloudflare - WAF - Potential XSS Attack`: This alert will trigger when there are a large number of logs containing Cloudflare WAF XSS Attack Score values that indicate an attack (score between 1 to 20).

   For more information about the Cloudflare WAF Attack Score, see [WAF attack score](https://developers.cloudflare.com/waf/detections/attack-score/){: external}.

* `Cloudflare - WAF - Potential RCE Attack`: This alert will trigger when there are a large number of logs containing Cloudflare WAF RCE Attack Score values that indicate an attack (score between 1 to 20).

   For more information about the Cloudflare WAF Attack Score, see [WAF attack score](https://developers.cloudflare.com/waf/detections/attack-score/){: external}.

* `Cloudflare - WAF - Common Vulnerability Attack`: This alert triggers when logs containing triggered Cloudflare WAF rules have mentions of a CVE over a determined period of time in the context of a single IP address.

* `Cloudflare - WAF - Brute Force on Login URLs`: This alert triggers when a possible brute force attack is performed against a login page.

   Brute force attacks on login pages involve systematically attempting multiple combinations of usernames and passwords until a successful login is achieved. This technique relies on the assumption that weak or commonly used credentials can be guessed through exhaustive trial and error. 

* `Cloudflare - WAF - DDoS Attack Detected`: This alert triggers when Cloudflare detects a Layer 7 DDoS (L7 DDoS) attack. Cloudflare's Layer 7 Distributed Denial of Service (L7 DDoS) protection detects and mitigates attacks targeting the application layer of a web application. These attacks aim to overwhelm the application or its infrastructure by flooding it with a high volume of HTTP requests.

* `Cloudflare - WAF - Multiple Unknown Actions From Unique IPs`: This alert triggers when Cloudflare's Web Application Firewall (WAF) logs multiple distinct "unknown" actions from a single IP address within a short timeframe.

   You will want to fine-tune the threshold based on your environtment's traffic patterns. 


### DNS alerts
{: #extensions-cloudflare-alerts-dns}

* `Cloudflare - DNS - Excessive REFUSED Response Code Returned`: This alert detects when a high number of REFUSED response codes are returned as a result of DNS queries. REFUSED response code indicates that the DNS query failed because the server refused to answer the query. This could be due to policy reasons.

* `Cloudflare - DNS - Excessive SERVFAIL Response Code Returned`: This alert detects when a high number of SERVFAIL response codes are returned as a result of DNS queries. SERVFAIL response code is an indication of a server failure. This could be due to a technical problem with the DNS servers.

* `Cloudflare - DNS - High Number of NXDOMAIN Responses Returned`: This alert detects when a high number of NXDOMAIN response codes are returned as a result of DNS queries. NXDOMAIN response code indicates that the queried domain is non-existent.

* `Cloudflare - DNS - Anomalous Number of Uncommon DNS Record Types Observed`: This alert detects when a high number of DNS queries are seen from a host with uncommon record types such as `TXT`, `PTR`, and `NULL`.

   `TXT`: Indicates a text record. These records are often used for email security.
   `PTR`: Provides a domain name in reverse-lookups.
   `NULL`: Indicates a null resource record.


### Audit alerts
{: #extensions-cloudflare-alerts-dns}

* `Cloudflare - Audit - No Logs From Cloudflare in The Last 10 Minutes`: This alert detects when there are no logs seen from Cloudflare to the user account in the past 10 minutes.

* `Cloudflare - Audit - API Key Viewed`: This alert detects when the account-wide API token is viewed. API keys are the previous/legacy authorization scheme for interacting with the Cloudflare API. Cloudflare recommends using API tokens instead of API keys when possible. Cloudflare provides two types of API keys:

   * Global API Key: Serves as your main API key.
   * Origin CA Key: Only used when creating origin certificates using the API.

* `Cloudflare - Audit - API Token Rolled`: This alert detects when a Cloudflare user API token is rolled. If your token is lost or compromised, you can either create a new token or roll your token to generate a new secret. Rolling your API token into a new one will invalidate the previous token, but the access and permissions will be the same as the previous API token.

* `Cloudflare - Audit - API Token Created`: This alert detects when a Cloudflare user API token is created. Using the Cloudflare API requires authentication so that Cloudflare knows who is making requests and what permissions you have.

* `Cloudflare - Audit - A Worker Was Updated`: This alert detects every time an existing Cloudflare worker is updated. A Cloudflare worker is a platform for enabling serverless functions to run as close as possible to the end user.

* `Cloudflare - Audit - A Worker Was Created`: This alert detects every time a new worker is created. A Cloudflare worker is a platform for enabling serverless functions to run as close as possible to the end user.

* `Cloudflare - Audit - Account password changed`: This alert detects when a user resets the password by selecting the 'Forgot your password?' option on the account login page.

* `Cloudflare - Audit - Certificate Pack Created`: This alert is triggered in the case where a new Cloudflare Certificate Pack is created by a user. Certificate pack is a group of SSL/TLS certificates that share the same set of hostnames.

* `Cloudflare - Audit - A Firewall Rule Created or Updated`: This alert detects when a Cloudflare Firewall rule was created or updated.

* `Cloudflare - Audit - Certificate Pack Expired`: This alert is triggered when a Cloudflare Certificate Pack is about to expire or had expired. Certificate pack is a group of SSL/TLS certificates that share the same set of hostnames.
 
* `Cloudflare - Audit - Firewall Rule Deleted`: This alert is triggered when a Cloudflare Certificate Pack delete is requested by a user. Certificate pack is a group of SSL/TLS certificates that share the same set of hostnames.

* `Cloudflare - Audit - DNS A Record Deleted`: This alert detects when an `A` record was deleted.

   The main use of `A` record is for IPv4 address lookup. Using an `A` record, a web browser is able to load a website using the domain name.

* `Cloudflare - Audit - DNS NS Record Deleted`: This alert detects when a NS record was deleted.

   A nameserver (NS) record specifies the authoritative DNS server for a domain. The NS record helps point to where internet applications, such as a web browser, can find the IP address for a domain name. Multiple nameservers are usually specified for a domain.

* `Cloudflare - Audit - DNS AAAA Record Deleted`: This alert detects when an `AAAA` record was deleted.

   The main use of `AAAA` records is for IPv6 address lookup. Using an `AAAA` record, a web browser is able to load a website using the domain name.

   With an `AAAA` record, an adversary can create a custom domain or point existing domains to an attacker controlled IP.

* `Cloudflare - Audit - DNS PTR Record Deleted`: This alert detects when a `PTR` record was deleted.

   Pointer records (`PTR`) provides the domain name associated with an IP address. A DNS `PTR` record is the opposite of an `A` record, which provides the IP address associated with a domain name.

   DNS `PTR` records are used in reverse DNS lookups. When a user attempts to reach a domain name in their browser, a DNS lookup occurs, matching the domain name to the IP address. A reverse DNS lookup is the opposite of this process: it is a query that starts with the IP address and looks up the domain name.

* `Cloudflare - Audit - DNS TXT Record Deleted`: This alert detects when a `TXT` record was deleted.

   `TXT` records are a type of DNS record that contains text information for sources outside of your domain. You add these records to your domain settings.

   You can use `TXT` records for various purposes such as verifying domain ownership or Email security (as `DKIM` and `SPF` records).

* `Cloudflare - Audit - DNS MX Record Deleted`: This alert detects when a `MX` record was deleted.

   A mail exchange (`MX`) record, is a DNS record type that shows where emails for a domain should be routed to. In other words, a `MX` record makes it possible to direct emails to a mail server.

* `Cloudflare - Audit - DNS CAA Record Deleted`: This alert detects when a `CAA` record was deleted.

   `CAA` records allow domain owners to declare which certificate authorities are allowed to issue a certificate for a domain. They also provide a means of indicating notification rules in case someone requests a certificate from an unauthorized certificate authority. If no `CAA` record is present, any CA is allowed to issue a certificate for the domain. If a `CAA` record is present, only the CAs listed in the records are allowed to issue certificates for that hostname.

* `Cloudflare - Audit - DNS CNAME Record Deleted`: This alert detects when a CNAME record was deleted.

   `CNAME` (canonical name) is a DNS record that points a domain name (an alias) to another domain. In a `CNAME` record, the alias doesn't point to an IP address. The domain name that the alias points to is the canonical name.

* `Cloudflare - Audit - DNS AAAA Record Added or Updated`: This alert detects when an `AAAA` record was created or updated.

   The main use of `AAAA` records is for IPv6 address lookup. Using an `AAAA` record, a web browser is able to load a website using the domain name.

* `Cloudflare - Audit - DNS TXT Record Added or Updated`: This alert detects when a `TXT` record was created or updated.

   `TXT` records are a type of DNS record that contains text information for sources outside of your domain. You add these records to your domain settings.

   You can use `TXT` records for various purposes such as verifying domain ownership or email security (as `DKIM` and `SPF` records).

* `Cloudflare - Audit - DNS MX Record Added or Updated`: This alert detects when a `MX` record was created or updated.

   A mail exchange (`MX`) record, is a DNS record type that shows where emails for a domain should be routed. An MX record makes it possible to direct emails to a mail server.

* `Cloudflare - Audit - DNS PTR Record Added or Updated`: This alert detects when a `PTR` record was created or updated.

   Pointer records (`PTR`) provide the domain name associated with an IP address. A DNS `PTR` record is exactly the opposite of an `A` record, which provides the IP address associated with a domain name.

   DNS `PTR` records are used in reverse DNS lookups. When a user attempts to reach a domain name in their browser, a DNS lookup occurs, matching the domain name to the IP address. A reverse DNS lookup is the opposite of this process: it is a query that starts with the IP address and looks up the domain name.

* `Cloudflare - Audit - DNS CNAME Record Added or Updated`: This alert detects when a `CNAME` record was created or updated.

   `CNAME` (canonical name) is a DNS record that points a domain name (an alias) to another domain. In a`CNAME` record, the alias doesn't point to an IP address. And the domain name that the alias points to is the canonical name.

* `Cloudflare - Audit - DNS NS Record Added or Updated`: This alert detects when a `NS` record was created or updated.

   A nameserver (`NS`) record specifies the authoritative DNS server for a domain. The NS record  points to where internet applications like a web browser can find the IP address for a domain name. Multiple nameservers are usually specified for a domain.

* `Cloudflare - Audit - DNS CAA Record Added or Updated`: This alert detects when a `CAA` record was created or updated.

   `CAA` records allow domain owners to declare which certificate authorities are allowed to issue a certificate for a domain. They also provide a means of indicating notification rules in case someone requests a certificate from an unauthorized certificate authority. If no `CAA` record is present, any CA is allowed to issue a certificate for the domain. If a `CAA` record is present, only the CAs listed in the record(s) are allowed to issue certificates for that hostname.

* `Cloudflare - Audit - DNS A Record Added`: This alert triggers when a DNS `A` record is added.

## Rules
{: #extensions-cloudflare-rules}

One rule is provided which does the following:

* Extracts the event timestamp to the {{site.data.keyword.logs_full_notm}} timestamp
* Extracts the `EdgeResponseStatus` to the {{site.data.keyword.logs_full_notm}} severity

## Events to metrics
{: #extensions-cloudflare-e2m}

You can deploy any of the following events to metrics configurations. For details about the created metrics, see the events to metrics definitions.

These events to metrics configurations are used by the extension dashboards. If a dashboard is missing data, make sure the event to metrics configuration is deployed and working correctly for your environment.

* `Cloudflare_WAF_Client_Request_Metrics`: Cloudflare WAF client request metrics
* `Cloudflare_WAF_Attack_Scores_Metrics`: Cloudflare WAF attack scores metrics
* `Cloudflare_WAF_Client_GeoIP_Metric`: Cloudflare WAF client geoIP metrics
* `Cloudflare_WAF_Rules_Responses_Metrics`: Cloudflare WAF rules responses metrics
* `Cloudflare_DNS_Metrics`: Cloudflare metrics for DNS metrics


## Enrichments
{: #extensions-cloudflare-enrichments}

You can deploy any of the 3 enrichments.

* `Geo enrichment`: Enrich your logs with location data by automatically converting IPs to geo-points which can be used to aggregate logs by location.
* `Cloudflare DNS - DNS Record Types`: Enrich your data with DNS record type information.
* `Cloudflare DNS - DNS Response Codes`: Enrich your data with DNS response code information.
