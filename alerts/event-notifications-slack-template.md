---

copyright:
  years:  2024, 2026
lastupdated: "2026-02-06"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Customizing Slack messages
{: #event-notifications-slack-template}

You can customize the Slack messages sent through {{site.data.keyword.en_full_notm}} by using a template. For more information, see [Creating an {{site.data.keyword.en_short}} template](/docs/cloud-logs?topic=cloud-logs-event-notifications-create-template).
{: shortdesc}


## Prereqs
{: #event-notifications-slack-template-prereqs}

Read the following information:
- [Slack](/docs/event-notifications?topic=event-notifications-en-destinations-slack).

    When a message of length greater than 3000 characters is sent to slack, the message text gets truncated with leaders [...].
	{: important}

- [Configuring a slack destination](/docs/event-notifications?topic=event-notifications-en-destinations-slack#en-slack-configure-destination)
- [Configuring a slack subscription](/docs/event-notifications?topic=event-notifications-en-destinations-slack#en-slack-configure-sub)
- [Testing a Slack destination configuration](/docs/event-notifications?topic=event-notifications-en-destinations-slack#en-slack-test-destination)
- [Slack retry policy](/docs/event-notifications?topic=event-notifications-en-destinations-slack#en-slack-retry)

    If a call to the Slack webhook URL fails even after retry attempts, the notification is lost.
	{: important}


## Create a template by uysing the API
{: #event-notifications-slack-template-api}


To customize the Slack message, you can configure the template by using the [{{site.data.keyword.en_full_notm}} API](/apidocs/event-notifications#create-template).

The following is an example Slack message template.

```json
{
    "attachments": [
        {
            {{#if (equal data.alert_definition.severity "Error")}}
            "color": "#dc143c",
            {{else}}
            "color": "#097969",
            {{/if}}
            "blocks": [
                {
                    "type": "section",
                    "text": {
                        "type": "mrkdwn",
                        "text": "*{{data.alert_definition.name}}*"
                    }
                },
                {
                    "type": "section",
                    "text": {
                        "type": "mrkdwn",
                        "text": "```{{data.log_example}}```"
                    }
                },
                {
                    "type": "section",
                    "text": {
                        "type": "mrkdwn",
                        "text": "<{{data.links.view_alert}}|View> | <{{data.links.edit_alert}}|Edit>"
                    }
                }
            ]
        }
    ]
}
```
{: codeblock}



The following is a sample Slack template for Kubernetes logs including an `errorMsg` field.

```json
{
	"blocks": [
		{
			"type": "header",
			"text": {
				"type": "plain_text",
				"text": "Alert name: {{data.alert_definition.name}}",
				"emoji": true
			}
		},
		{
			"type": "context",
			"elements": [
				{
					"type": "image",
					"image_url": "https://image.freepik.com/free-photo/red-drawing-pin_1156-445.jpg",
					"alt_text": "images"
				},
				{
					"type": "plain_text",
					"text": "Severity: {{data.alert_definition.severity}}"
				}
			]
		},
		{
			"type": "divider"
		},
		{
			"type": "section",
			"text": {
				"type": "mrkdwn",
				"text": "*Error message:* {{data.log_example.errorMsg}}"
			}
		},
		{
			"type": "divider"
		},
		{
			"type": "section",
			"text": {
				"type": "mrkdwn",
				"text": "*Cluster name:* {{data.log_example.[kubernetes.cluster_name]}}"
			}
		},
		{
			"type": "section",
			"text": {
				"type": "mrkdwn",
				"text": "*Namespace:*  {{data.log_example.[kubernetes.namespace_name]}} \n \n"
			}
		},
		{
			"type": "section",
			"text": {
				"type": "mrkdwn",
				"text": "*Pod name:* {{data.log_example.[kubernetes.pod_name]}}"
			}
		},
		{
			"type": "section",
			"text": {
				"type": "mrkdwn",
				"text": "*App label:* {{data.log_example.[kubernetes.labels.app]}}"
			}
		},
		{
			"type": "divider"
		},
		{
			"type": "section",
			"text": {
				"type": "mrkdwn",
				"text": "*Incident information in Cloud Logs:* <{{data.links.view_alert}}|View> | <{{data.links.edit_alert}}|Edit>"
			}
		}
	]
}
```
{: codeblock}

Before using the template with the API it must be converted to base64. After converting the template to base64 it can be included in the body of the API call. The following example uses the previous template converted to base64.

```sh
curl --request POST \
  --url https://<EVENT-NOTIFICATION-REGION>.event-notifications.cloud.ibm.com/event-notifications/v1/instances/<INSTANCE_ID>/templates \
  --header 'Authorization: Bearer <Access_token>' \
  --header 'Content-Type: application/json' \
  --data '{
	"name": "<NAME>",
	"description": "<DESCRIPTION>",
	"params": {
		"body": "ewogICAgImF0dGFjaG1lbnRzIjogWwogICAgICAgIHsKICAgICAgICAgICAge3sjaWYgKGVxdWFsIGRhdGEuYWxlcnRfZGVmaW5pdGlvbi5zZXZlcml0eSAiRXJyb3IiKX19CiAgICAgICAgICAgICJjb2xvciI6ICIjZGMxNDNjIiwKICAgICAgICAgICAge3tlbHNlfX0KICAgICAgICAgICAgImNvbG9yIjogIiMwOTc5NjkiLAogICAgICAgICAgICB7ey9pZn19CiAgICAgICAgICAgICJibG9ja3MiOiBbCiAgICAgICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAgICAgInR5cGUiOiAic2VjdGlvbiIsCiAgICAgICAgICAgICAgICAgICAgInRleHQiOiB7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0eXBlIjogIm1ya2R3biIsCiAgICAgICAgICAgICAgICAgICAgICAgICJ0ZXh0IjogIip7e2RhdGEuYWxlcnRfZGVmaW5pdGlvbi5uYW1lfX0qIgogICAgICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgICAgIH0sCiAgICAgICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAgICAgInR5cGUiOiAic2VjdGlvbiIsCiAgICAgICAgICAgICAgICAgICAgInRleHQiOiB7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0eXBlIjogIm1ya2R3biIsCiAgICAgICAgICAgICAgICAgICAgICAgICJ0ZXh0IjogImBgYHt7ZGF0YS5sb2dfZXhhbXBsZX19YGBgIgogICAgICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgICAgIH0sCiAgICAgICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAgICAgInR5cGUiOiAic2VjdGlvbiIsCiAgICAgICAgICAgICAgICAgICAgInRleHQiOiB7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0eXBlIjogIm1ya2R3biIsCiAgICAgICAgICAgICAgICAgICAgICAgICJ0ZXh0IjogIjx7e2RhdGEubGlua3Mudmlld19hbGVydH19fFZpZXc+IHwgPHt7ZGF0YS5saW5rcy5lZGl0X2FsZXJ0fX18RWRpdD4iCiAgICAgICAgICAgICAgICAgICAgfQogICAgICAgICAgICAgICAgfQogICAgICAgICAgICBdCiAgICAgICAgfQogICAgXQp9"
	},
	"type": "slack.notification"
}'
```
{: pre}

You will need to change `<EVENT-NOTIFICATION-REGION>`, `<INSTANCE-ID`>, `<NAME>`, and `<DESCRIPTION>` as appropriate for your environment.

You can also use a Terraform script to create the template.

```terraform
resource "ibm_en_slack_template" "slack_template" {
  instance_guid         = "<instance-id>"
  name                  = "Notification Template"
  type                  = "slack.notification"
  description           = "Slack template for event notification"
  params {
        body="ewogICAgImF0dGFjaG1lbnRzIjogWwogICAgICAgIHsKICAgICAgICAgICAge3sjaWYgKGVxdWFsIGRhdGEuYWxlcnRfZGVmaW5pdGlvbi5zZXZlcml0eSAiRXJyb3IiKX19CiAgICAgICAgICAgICJjb2xvciI6ICIjZGMxNDNjIiwKICAgICAgICAgICAge3tlbHNlfX0KICAgICAgICAgICAgImNvbG9yIjogIiMwOTc5NjkiLAogICAgICAgICAgICB7ey9pZn19CiAgICAgICAgICAgICJibG9ja3MiOiBbCiAgICAgICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAgICAgInR5cGUiOiAic2VjdGlvbiIsCiAgICAgICAgICAgICAgICAgICAgInRleHQiOiB7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0eXBlIjogIm1ya2R3biIsCiAgICAgICAgICAgICAgICAgICAgICAgICJ0ZXh0IjogIip7e2RhdGEuYWxlcnRfZGVmaW5pdGlvbi5uYW1lfX0qIgogICAgICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgICAgIH0sCiAgICAgICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAgICAgInR5cGUiOiAic2VjdGlvbiIsCiAgICAgICAgICAgICAgICAgICAgInRleHQiOiB7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0eXBlIjogIm1ya2R3biIsCiAgICAgICAgICAgICAgICAgICAgICAgICJ0ZXh0IjogImBgYHt7ZGF0YS5sb2dfZXhhbXBsZX19YGBgIgogICAgICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgICAgIH0sCiAgICAgICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAgICAgInR5cGUiOiAic2VjdGlvbiIsCiAgICAgICAgICAgICAgICAgICAgInRleHQiOiB7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0eXBlIjogIm1ya2R3biIsCiAgICAgICAgICAgICAgICAgICAgICAgICJ0ZXh0IjogIjx7e2RhdGEubGlua3Mudmlld19hbGVydH19fFZpZXc+IHwgPHt7ZGF0YS5saW5rcy5lZGl0X2FsZXJ0fX18RWRpdD4iCiAgICAgICAgICAgICAgICAgICAgfQogICAgICAgICAgICAgICAgfQogICAgICAgICAgICBdCiAgICAgICAgfQogICAgXQp9"
  }
  provider = ibm.ibm-en
}
provider.tf
provider "ibm" {
	alias  = "ibm-en"
    region = "jp-tok"
}
version.tf
terraform {
  required_version = ">= 1.5.0"
  required_providers {
    ibm = {
      source  = "IBM-Cloud/ibm"
      version = "1.70.0-beta0"
    }
  }
}
```
{: codeblock}

For more information about implementing Slack templates, see the {{site.data.keyword.en_full_notm}} documentation about [Slack notification templates](/docs/event-notifications?topic=event-notifications-en-slack-notification-template).
