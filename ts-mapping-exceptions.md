---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-20"

keywords: 

subcollection: cloud-logs

---


{{site.data.keyword.attribute-definition-list}}

# Why am I not seeing results from my {{site.data.keyword.frequent-search}} searches?
{: #ts-mapping-exceptions}
{: troubleshoot}
{: support}

When searching in {{site.data.keyword.logs_full}} using {{site.data.keyword.frequent-search}} I am not seeing the expected results returned. I know the fields I am searching for in my logs exist, but {{site.data.keyword.logs_full_notm}} doesn't seem to find them with my searches.
{: shortdesc}

Searching for field values does not return expected results.
{: tsSymptoms}

The problem is often related to a mapping exception.
{: tsCauses}

A mapping exception can happen if new log fields are ingested with field names that were previously ingested by {{site.data.keyword.logs_full_notm}}, but have a different value type.  When {{site.data.keyword.logs_full_notm}} indexes ingested data, it tries to map the fields to one of the following types:

* `String`
* `Numeric`
* `Object`
* `Array`

If, for example, the field `user` has been ingested and the first received value is “username”, {{site.data.keyword.logs_full_notm}} will create an index of type `string` for the field `user`:

```json
"user": “username”`
```
{: codeblock}

If later on a new log is ingested that also has a field named “user” that is formatted like this:

```json
"user": {
  “email”: “username@yourcompany.com”,
  ”login”: “username”`
}
```
{: codeblock}

A mapping exception is created in {{site.data.keyword.logs_full_notm}}. Any {{site.data.keyword.frequent-search}} searches looking for a field named `user` would be expected to have a `string` value based on the first log ingested with a `user` field.

Any {{site.data.keyword.frequent-search}} searches looking for a `user` with the `array` type (`user.email` or `user.login`) will not return any results due to the mapping exception.
{{_include-segments/mapping-exception-whatis.md}}

You can determine if there are mapping exceptions using the {{site.data.keyword.logs_full_notm}} UI.
{: tsResolve}

To identify mapping exceptions, complete the following steps:

1. Check the {{site.data.keyword.logs_full_notm}} UI for an icon next to the logs count:

   ![Mapping exceptions icon](../images/me_01a.png){: caption="Mapping exceptions icon" caption-side="bottom"}

   Hovering over the icon will display the number of logs with mapping exceptions within the query results in the selected timeframe.

2. To identify the specific logs that were not properly indexed, enable the `Show Mapping errors` option:

   ![Selecting how to show mapping errors. Click Settings and then click Show mapping errors.](../images/me_02a.png){: caption="Selecting how to show mapping errors" caption-side="bottom"}

3. After enabling this option, refresh your browser.

   An exclamation mark will be displayed on the fields that have mapping exceptions and were not indexed.

   ![Flagging of fields with mapping exceptions](../images/me_03a.png){: caption="Flagging of fields with mapping exceptions" caption-side="bottom"}

   Another way to quickly identify which fields have a mapping exception is to run the query: `_exists_: coralogix.failed_reason`

   ![Query to show mapping exceptions](../images/me_04a.png){: caption="Query to show mapping exceptions." caption-side="bottom"}

   This query will return only the log lines that have a mapping exception for the selected timeframe.

There are two ways you can resolve mapping exceptions:

- Option 1: Search without indexing.

   If you do not find a field when querying due to mapping exceptions, you can search in `All Logs` instead of `Priority Insights`. When searching in `All Logs`, indexing and mapping exceptions are bypassed by the search.

- Option 2: Fix log records at ingestion.

   You can fix new log records being ingested with the same field names but with different data types.



   1. Create a [RegEx expression](/docs/cloud-logs?topic=cloud-logs-parse-rules-regex) to replace the field name with the appropriate sufix. For example:

      `field_obj`
      :  If {{site.data.keyword.logs_full_notm}} is expecting a string, but found an object:
          * Regular Expression: `("field"\s*:\s*{)`
          * Replace with: `"field_obj":{`

      `field_arr`
      :  If {{site.data.keyword.logs_full_notm}} is expecting a string, but found an array:
         * Regular Expression: `("field"\s*:\s*[)`
         * Replace with: `"field_arr":[`

      `field_str`
      :  If {{site.data.keyword.logs_full_notm}} is expecting an object, but found a string:
         * Regular Expression: `("field"\s*:\s*")`
         * Replace with: `"field_str":"`

   2. Create a parsing [replace rule](/docs/cloud-logs?topic=cloud-logs-parse-replace-rule&interface=ui) to fix new logs using the RegEx.
