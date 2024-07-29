---

copyright:
  years:  2024
lastupdated: "2024-07-29"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Return code 500 returned when an alert is sent to {{site.data.keyword.en_full_notm}}
{: #troubleshoot-rc500}
{: troubleshoot}
{: support}

A return code 500 is returned when attempting to send an alert to {{site.data.keyword.en_full_notm}}.
{: shortdesc}


Sending an alert to {{site.data.keyword.en_full_notm}} fails with a 500 return code.
{: tsSymptoms}

The `group_by` value in the `condition` block in the alert payload is not identical to the `group_by_fields` value in the `notification_groups` block. These values must be the same.
{: tsCauses}


```json
"condition": {
        "more_than": {
            "parameters": {
                "threshold": 20,
                "timeframe": "timeframe_5_min_or_unspecified",
                "group_by": [
                    "coralogix.metadata.applicationName"
                ],
                "ignore_infinity": true,
                "relative_timeframe": "hour_or_unspecified"
            },
            "evaluation_window": "rolling_or_unspecified"
        }
    },
```
{: codeblock}

```json
"notification_groups": [
        {
            "group_by_fields": [
                "coralogix.metadata.applicationName"
            ],
            "notifications": [
                {
                    "integration_id": 81
                }
            ]
        }
    ],
```
{: codeblock}


Change the values so they are identical.
{: tsResolve}

