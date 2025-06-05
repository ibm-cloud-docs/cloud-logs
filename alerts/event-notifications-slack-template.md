---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-05"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Customizing Slack messages using the API
{: #event-notifications-slack-template}

You can customize the Slack messages sent through {{site.data.keyword.en_full_notm}} by using the API to create a template.
{: shortdesc}

To customize the Slack message you need to configure the template using the [{{site.data.keyword.en_full_notm}} API](/apidocs/event-notifications#create-template) not the UI.
{: important}

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

