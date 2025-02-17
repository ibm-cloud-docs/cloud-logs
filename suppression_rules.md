---

copyright:
  years:  2024, 2025
lastupdated: "2025-02-17"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Alert suppression rules
{: #suppression_rules}

{{site.data.keyword.logs_full}} suppression rules can be used to manage when alerts are triggered.
{: shortdesc}

With suppression rules, you can control when [alerts](/docs/cloud-logs?topic=cloud-logs-alerts-config) are triggered or suppressed.

You can configure 5 different suppression rule types.

Scheduled maintenance
:   You can suppress alerts during scheduled maintenance windows. Suppressing alerts during this time avoids unnecessary alerting when systems or applications are known to be unavailable due to scheduled maintenance activities.

Allow listing
:   Specifies conditions where conditions or sources trigger or suppress alerts. Allow listing can be used to ensure that critical alerts are still raised while lower-priority issues are suppressed.

Working hours
:   You can define working and nonworking hours when alerts are triggered or suppressed.

System upgrade
:   You can suppress alerts during system upgrades. Suppressing alerts during this time avoids unnecessary alerting when systems are known to not be available during system upgrades.

Blank rule
:   You might have specific organizational needs to suppress or allow alerts to trigger other than the 4 predefined rule types. With the *Blank rule* type, you can create suppression rules based on your specific operational requirements.

## Creating a suppression rule
{: #create_suppression_rule}

Complete the following steps:

1. In the console, click the **Navigation menu** icon ![Navigation menu icon](../icons/icon_hamburger.svg) > **Observability** > **Logging** > **Instances**.

2. Click **Dashboard** to open the dashboard of your {{site.data.keyword.logs_full_notm}} instance.

3. In the {{site.data.keyword.logs_full_notm}} navigation, click the **Alerts** icon ![Alerts icon](/icons/alerts_icon.svg "Alerts") > **Suppression rules**.

4. Click **New rule**.

5. Enter a `Rule Name`, `Description`, and `Label` for the new rule. You can use the labels to manage, filter, and organize your suppression rules.

6. Select the `key:value` pairs to be processed by the rule, or choose for the rule to process all selected alert activity during the specified time frame.

   * Select one or more `group-by` keys and enter the values to be matched by the rule. These values are defined in the alert settings and are aggregated into a histogram. An alert is triggered when the condition threshold is met for the aggregated values within the specified time frame.

   * For keys in an IP address format, you can select `IP IN SUBNET` for `VALUE` and then specify an IP range in CIDR format. A configured rule matches all notifications that originate from an address within a specified range. For example, `192.168.11/24`.

   * If you have multiple values for a single key, any specified value is matched.

   * If you configure multiple keys, all keys must appear in the alert for the rule to be matched.

   * By selecting **Suppress all selected alert activity**, all selected alerts are matched during the time frame, including alerts set to nofity immediately and alerts without a `group-by` key set.

7. Select if the rule suppresses or triggers alerts.

   * If `Suppress` is selected, when the rule is matched the alert is suppressed (not triggered). If the rule is not matched, the alert is triggered.

   * If `Triggered` is selected, when the rule is matched the alert is triggered. If the rule is not matched, the alert is suppressed.

8. Select how often the rule is processed. This frequency can be daily, weekly, or monthly. If `Always` is selected, the rule is always processed for recurring rules. If `Recurring` is selected, specify a termination date.

9. Specify the starting and ending dates and times for the rule, or the duration of the rule.

10. Select the alerts that are processed by the rule.

   * You can select whether the rule affects selected alerts, or all alerts that are configured with a specific label value.

   * By selecting `Apply to all existing and future system alerts`, the rule will also be applied to alerts created after the suppression rule is created when the suppression rule criterion applies.

11. Click **Save changes** to save your suppression rule definition.

## Viewing configured suppression rules
{: #view_suppression_rules}

1. In the console, click the **Navigation menu** icon ![Navigation menu icon](../icons/icon_hamburger.svg) > **Observability** > **Logging** > **Instances**.

2. Click **Dashboard** to open the dashboard of your {{site.data.keyword.logs_full_notm}} instance.

3. In the {{site.data.keyword.logs_full_notm}} navigation, click the **Alerts** icon ![Alerts icon](/icons/alerts_icon.svg "Alerts") > **Suppression rules**.

The **Suppression rules** page is displayed showing configured active and expired (past) rules. The list can be filtered and searched.

For each rule you can see the rule name, associated labels and values, the affected alerts, the time range, rule type, and if the rule is enabled.

## Managing suppression rules
{: #managing_suppression_rules}

From the **Suppression rules page** you can edit, clone, or delete a rule.

1. In the console, click the **Navigation menu** icon ![Navigation menu icon](../icons/icon_hamburger.svg) > **Observability** > **Logging** > **Instances**.

2. Click **Dashboard** to open the dashboard of your {{site.data.keyword.logs_full_notm}} instance.

3. In the {{site.data.keyword.logs_full_notm}} navigation, click the **Alerts** icon ![Alerts icon](/icons/alerts_icon.svg "Alerts") > **Suppression rules**.

4. Click the **ACTIVE RULES** or **PAST RULES** tab and find the rule that you want to manage.

5. Click the **Actions** icon ![Actions icon](/icons/horz-menu-icon.svg "Actions") next to the rule that you want to manage.

6. Select the action that you want to take on the rule:

   **EDIT** 
   :   Change the existing rule. Click **Save changes** to save your changes.

   **CLONE**
   :   Copy an existing rule to create a new rule. Change your cloned rule and click **Save changes**.

   **DELETE**
   :   Delete the existing rule. Confirm that you want to delete the rule.

## Considerations for Allow listing rules
{: #suppression-rules-allowlist}

For Allow listing rules, consider:

* The key name must be a key that is used in a `groupBy` section of an alert. In the alert `groupBy` you can use any key that is present in a log line, but for suppression rules only keys that are used in the alert `groupBy` are displayed as keys.

* Key values must be specified in lowercase.

* Allow listing suppression rules cannot be used with [standard alerts](/docs/cloud-logs?topic=cloud-logs-alerts-config-standard) that are configured to `notify immediately`. Allow listing suppression rules can be used with standard alerts that are configured with `more than`, `more than usual`, or `less than` conditions.
