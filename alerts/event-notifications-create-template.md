---

copyright:
  years:  2024, 2026
lastupdated: "2026-02-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Creating an {{site.data.keyword.en_short}} template
{: #event-notifications-create-template}

An {{site.data.keyword.en_full_notm}} template defines the layout and content of notifications (email, webhook, Slack, etc.). Templates can include images, static text, and dynamic content (variables, conditional logic) based on events.
{: shortdesc}

{{site.data.keyword.en_short}} supports two types of templates:

1. User-defined templates: You can design your own templates to structure notification messages.

1. [Pre-defined templates](/docs/event-notifications?topic=event-notifications-en-predefinedTemplates): These are standard templates defined for a pair of specific source and destination. You can customize pre-defined templates to create a user defined template.


## Creating a user-defined template
{: #en-create-template}

1. In the {{site.data.keyword.cloud_notm}} console, click the **menu** icon ![hamburger icon](images/icon_hamburger.svg) > **Platform Automation** > **Event notifications**.
1. Click the name of your {{site.data.keyword.en_short}} instance.
1. Select **Templates** from the left panel. Then, click **Create**.
1. Enter details about the template such as the name and description.
1. Select a template type and add the template block.

    * [Custom Email Notification](/docs/event-notifications?topic=event-notifications-en-email-templates)
    * [Custom Email Invitation](/docs/event-notifications?topic=event-notifications-en-email-templates)
    * [Webhook Notification](/docs/event-notifications?topic=event-notifications-en-webhook-notifications-template)
    * [Slack Notification](/docs/event-notifications?topic=event-notifications-en-slack-notification-template)
    * [PagerDuty Notification](/docs/event-notifications?topic=event-notifications-en-pagerduty-notification-template)
    * [Event Streams Notification](/docs/event-notifications?topic=event-notifications-en-event-streams-notification-template)
    * [Code Engine Notification](/docs/event-notifications?topic=event-notifications-en-code-engine-notification-template&interface=ui)
    * [App Configuration Notification](/docs/event-notifications?topic=event-notifications-en-app-configuration-notification-template&interface=ui)

    For more information, see [{{site.data.keyword.en_short}} supported templates](/docs/event-notifications?topic=event-notifications-en-create-en-template#en-create-template).

1. Click **Add** to save your updates.


## Customize notification messages using template variables
{: #handlebars-integration}

Handlebars is a templating language that allows for dynamic content generation within templates. Handlebars can be used to customize notification messages using template variables ,conditional logic and various other helpers.

### Template Variables
{: #template-variables}

Template variables are placeholders within the notification message templates that get replaced with actual data when a notification is triggered. These variables allow users to personalize messages and include relevant information from the event being notified.

#### Usage:
{: #usage-template-variables}

```handlebars
{{variable_name}}
```

Example:
```handlebars
Event Name: {{event_name}}
```

### Conditional Logic Helper
{: #conditional-logic-helper}

Conditional logic allows users to define conditions within the message templates, enabling dynamic content generation based on the values of variables. This feature is useful for creating flexible notification messages that adapt to different scenarios.

#### Usage:
{: #usage-conditional-logic-helper}

```handlebars
{{#if condition}}
   
{{else}}
   
{{/if}}
```

Example:
```handlebars
{{#if severity}}
   Severity: {{severity}}
{{else}}
   No severity information available
{{/if}}
```

### Contains Helper
{: #contains-helper}

The contains helper allows users to check whether there is a specific word in any of the fields of the payload.

#### Example:
{: #example-contains-helper}

```
"data":
{
	"message": "this is test alert from dev account"
}
```
Use the contains helpers like:

```handlebars
{
{{#contains data.message "dev"}}
"environment": "development"
{{/contains}}
}
```

There are more helpers available for use that can be referenced from [here](https://github.com/aymerick/raymond?tab=readme-ov-file#built-in-helpers)
{: note}

### Examples:
{: #template-examples}

Payload:

```json
"data":
{
	"message": "this is test alert from dev account",
	"secrets": [
	{
		"event_time": "2025-01-24T00:45:01Z",
		"event_triggered_by": "SecretsManager",
		"secret_expiration": "2025-04-24T00:45:01Z"
	}
],
}
```

#### Using Conditional Logic Helpers along with Contains helpers
{: #conditional-contains-helpers}

```handlebars
{{#if (contains data.message "dev")}}
"color":"#1E90FF"
{{else if (contains ibmendefaultlong "prod")}}
"color":"#dc143c"
{{else}}
"color":"#097969"
{{/if}}
```

#### For loop to print each and every key value from array of map
{: #for-loop-1}

```handlebars
{
	{{#each data.secrets}}
	  {
	"type": "TextBlock",
	"text": "{{@key}}: {{this}}",
	"wrap": true
	},
	{{/each}}
}
```

#### For loop to print specific values from a array of map
{: #for-loop-2}

```handlebars
{{#each data.secrets}}
	{
	"secret_expiration": "{{secret_expiration}}",
	 "event_time": "{{event_time}}"
	 }
{{/each}}
```
#### Accessing value from payload where the key contains special chanracters

Payload:

```
"toolchain.tool-instance":{
	"name":"sample-date"
}
```
{: codeblock}
