---

copyright:
  years:  2024, 2025
lastupdated: "2025-10-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.logs_full_notm}} considerations for new alert and priority configuration
{: #new-version-considerations}



{{site.data.keyword.logs_full}} has made changes to the configuration and processing of alerts and how alert priorities are defined. These changes might impact any automation configured for your environment.
{: shortdesc}

## Change from alert severity to priority
{: #newconsider_priiority}



With the latest {{site.data.keyword.logs_full_notm}} release, {{site.data.keyword.logs_full_notm}} has changed the alert configuration from using a series of 4 alert severities to 5 alert priorities.

| Severity | Priority |
|----------|----------|
| `Critical` | `P1` |
| `Error` | `P2` |
| `Warning` | `P3` |
| `Info` `[*]` | `P4` |
| `Info` | `P5` |
{: caption="Mapping of old alert severity values to new priority values" caption-side="bottom"}

`[*]` - There is no equivalent severity value for priority `P4`. `P4` is logically mapped as `Info` along with `P5`.
{: note}

Any existing automation (API or Terraform) in your environment can continue using the old severity values and they will be mapped to the new priority values. However, to take advantage of all new alert API functionality, you will want to update your automation to use the [new API](/apidocs/logs-service-api).

## Alert configuration changes made by using the UI
{: #newconsider_UI}



With the latest {{site.data.keyword.logs_full_notm}} changes, configuring alerts in the UI and API has changed and added additional functionality including:

* [Changing from severity to priority](#newconsider_priiority)
* [Multi-condition support](/docs/cloud-logs?topic=cloud-logs-multi-condition)
* [Customizing the evaluation window](/docs/cloud-logs?topic=cloud-logs-eval-window)

If you configure alerts using the {{site.data.keyword.logs_full_notm}} [*Alerts Management* page](/docs/cloud-logs?topic=cloud-logs-alerts-config), any changes you make to an existing alert will automatically be upgraded to the latest functionality. This includes changing how the alert is configured in the API.

Because alerts are automatically upgraded, if you have any APIs, Terraform, or other automation referencing the updated alerts, you will need to update the automation to meet the [new alert API](/apidocs/logs-service-api) definition.
{: attention}


## Changes to API support for alerting
{: #newconsider_API}

The latest {{site.data.keyword.logs_full}} version also includes changes to the {{site.data.keyword.logs_full}} alerts API.

The following table outlines the key changes between the previous and the current API. This information will help you understand the capabilities and limitations of each version when creating, updating, or querying alerts.

| Feature | Prior API | Current API | Notes |
|---------|-----------|-------------|-------|
| [Alert priorities](/docs/cloud-logs?topic=cloud-logs-priorities) | [Not supported]{: tag-red}  \n  \n API uses `severity` instead. | [Supported]{: tag-green}  \n  \n The `priority` value replaces the old `severity` value. | The prior API does not recognize the `P1-P5` priority values. Alerts with these values can result in the prior API not being able to process alerts with priority values. |
| [Multi-condition alerts](/docs/cloud-logs?topic=cloud-logs-multi-condition) | [Not supported]{: tag-red}  \n  \n Only one rule is supported per alert. | [Supported]{: tag-green} | The prior API will ignore any extra rules defined in an alert. |
| [Customizing the evalution window](/docs/cloud-logs?topic=cloud-logs-eval-window) | [Not supported]{: tag-red} | [Supported]{: tag-green} | The `evaluationDelay` field will be ignored by the prior API. |
| Anomaly detection alert sensitivity | [Not supported]{: tag-red} | [Supported]{: tag-green} | The prior API cannot interpret or trigger alerts based on deviation percentages. |
| Dynamic duration | [Supported]{: tag-green}  \n  \n Supported with `evaluationWindow`. | [Not supported]{: tag-red} \n  \n Replaced by rolling evaluation window. | If an alert configured in the prior API is processed by the current API, the `evaluationWindow` will be processed as a rolling evaluation window. |
{: caption="Differences between the prior and current API" caption-side="bottom"}

## Changes to the {{site.data.keyword.en_short}} payload
{: #newconsider_EventNotificationPayload}

The latest {{site.data.keyword.logs_full}} version includes changes in the {{site.data.keyword.en_full_notm}} payload. Your existing {{site.data.keyword.en_short}} configuration and payload will continue to work unchanged. Changes are only required if you want to take advantage of the new functionality.

The following new fields are available:

- `priority` is a new field added to the payload under the parent `data` field. This supports the change from `severity` to `priority`. There is no change to the `severity` field in the Event Notification payload. The value of the Event Notification `severity` field will be mapped as explained in [Change from alert severity to priority](#newconsider_priiority)
- `versioned_id` is a new field added to the payload. This is the ID which is generated when the alert is updated.
- The `id` field contains the `unique_identfier` value of the alert. This ID is generated when the alert is created and remains unchanged.

For more details, see:

- [Event Payload](/docs/cloud-logs?topic=cloud-logs-event-payload)
- [Event Severities](/docs/cloud-logs?topic=cloud-logs-event-severities)
