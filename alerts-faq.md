---

copyright:
  years:  2024, 2026
lastupdated: "2026-08-10"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for the alerts
{: #alerts_faq}

Frequently asked questions about the alerts.
{: shortdesc}

## Why does my query return results in the Logs Explorer but the alert does not fire?
{: #alert_faq_query_return}
{: faq}

The **Logs Explorer** and the alerting engines are independent query engines with different Luecne implementations. A query that returns result in the **Log Explorer** is not guaranteed to behave the same way in an alert.

* Rewrite the query by using the `.keyword` sub-field with a regex pattern. For example, use field `.keyword:/.*value.*/` instead of a plain field query.

* Escape any special characters in the value. 

* Confirm that the logs you want to alert are assigned to the medium or high TCO tiers. The alert engine do not evaluate logs in the low tier.
* Validate the query results in **Priority Insights** before you save the alert.

## Why did my less-than or absence alert fire even though the logs are present?
{: #alert_faq_absence_fire}
{: faq}

The alert query most likely failed to match the logs that are present, which caused the absence condition to be met unintentionally. This can happen for two reasons:

- The query value contains a special character such as a hyphen (`-`) that the Lucene analyzer treats as a token delimiter, splitting the value into separate tokens that do not match as expected.
- The query value contains a token that is shorter than three characters, such as `v2` or `01`, which the Lucene analyzer drops during indexing.

To resolve this issue, check the below:

- Rewrite the query by using the `.keyword` sub-field with a regex pattern and escape any special characters. 


## Why does .* not work when I use it inside double quotation marks?
{: #alert_faq_double_quotation}
{: faq}

When a value is enclosed within double quotation marks, it is considered as a literal phrase. The characters .* are not intepreted as a regex program. Regex matching is supported only on the `.keyword` sub-field, and only when the pattern is qrapped in forward-slash delimiters.  


## Why is the vertify graph empty?
{: #alert_faq_graph_empty}
{: faq}

The most likely cause is that no logs matching the alert query criteria were ingested in the past 24 hours. To confirm this, you can search for logs that match the alert conditions in the **Logs Explorer** and filter the time range to the past 24 hours. 


## Can I use numeric comparison operators such as greater than or less than in the alert query?
{: #alert_faq_comparison_operators}
{: faq}

Numeric camparion operators such as `>` and `<` are not supported in alert queries. To alert on a numeric threshold, use *Events2Metrics* to convert the log field into a metric. Then configure a metric alert with the required threshold condition.


## Are DataPrime queries supported in alerts?
{: #alert_faq_dataprime_queries}
{: faq}

Dataprime queries are not supported in alerts. Alert queries use only Lucene syntax. If you need to apply aggregation logic in an alert, use Events2Metrics to convert the log field into a metric. 


## Why has alert not changed after I edited it?
{: #alert_faq_edit}
{: faq}

After you save changes in an alert, allow up to 15 minutes for the alert engine to apply the updated query. The alert continues to evaluate logs against the previous query untill the updated configuration is active. 

