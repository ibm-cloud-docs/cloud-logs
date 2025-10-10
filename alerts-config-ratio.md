---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-10"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Configuring ratio alerts
{: #alerts-config-ratio}

You can calculate a ratio between two log queries and trigger an alert when the ratio reaches a set threshold.
{: shortdesc}

Example uses can include:

Operational health: Monitor the number of outgoing responses to incoming requests or the ratio of specific error codes to the overall number of errors.

Marketing: Monitor the ratio between traffic from specific regions to overall traffic following regional campaigns.

Security: Monitor the ratio of denied requests, specific administration operations, or requests originating from blocked network domains compared to all requests.


{{/_include-segments/alerts-prereq.md}}


{{/_include-segments/alerts-alerts-mgmt.md}}


{{/_include-segments/alerts-choose-type.md}}


{{/_include-segments/alerts-choose-logs.md}}

### Specify queries
{: #alerts-config-4a-ratio}

Specify the two queries whose results will be used to calcuate the ratio. For each query:

1. For the **Query Alias** specify a meaningful name for your query. The **Query Alias** will be included in your alert notifications.

2. Enter your query. Your query can include regex.

3. Indicate if you want your query to be applied to specific **Applications** and **Subsystems** or if it should apply to all.

4. Specify if your query should be applied to specific **Severities** or if it should apply to all severities.

#### Example queries
{: #alerts-config-query-example-ratio}

The following are example query combinations.

Example 1: Find the ratio between error code 504 and the overall number of response codes received. Higher-than-usual ratios might indicate operational issues.

* Query 1: `status:504`
* Query 2: `_exists_:status`


Example 2: Assuming addresses outside 172.xxx.xxx.xxx are restricted, an abnormal ratio of restricted traffic to all traffic might indicate an attack.

* Query 1: `NOT client_addr:/172\\.[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}/`
* Query 2: `_exists_:client_addr`

Example 3: Calculates how many requests were not answered successfully out of all successful requests. A higher-than-usual ratio might indicate operational issues.

* Query 1: `request_status:success`
* Query 2: `response_status:rejectrequest`


## Specify the triggering condition
{: step}
{: #alerts-config-4b-ratio}

Specify the triggering condition that is evaluated against the data included for analysis for this alert.

In **Alert if: Query 1 / Query 2 equals**, you must select whether the alert is triggered when the query is matched more or less than the threshold number within the defined time window.

- Choose `More than threshold` to be notified when the ratio between query results is more than the chosen threshold.

- Choose `Less than threshold` to be notified when the ratio between the query results is less than the chosen threshold.

If you are using the *Less than threshold* condition, you will have the option to manage undetected values.

Undetected values occur when a permutation of a *Less than threshold* alert stops being sent causing multiple triggers of the alert (for every timeframe in which it was not sent).

When you view an alert with undetected values, you have the option to retire these values manually, or select a time period after which undetected values will automatically be retired. You can also disable triggering on undetected values to immediately stop sending alerts when an undetected value occurs.

### Triggering alerts on infinity
{: #alerts-config-4a-tr}

If the second query result returns a zero value, the calculated ratio would be an infinite number.

You can specify whether or not to trigger the alert on this condition by selecting or deselecting **Do not tigger on Infinity**.


{{/_include-segments/alerts-group-by.md}}


{{/_include-segments/alerts-config-notif.md}}


{{/_include-segments/alerts-set-schedule.md}}


{{/_include-segments/alerts-save-config.md}}


{{/_include-segments/alerts-next-steps.md}}
