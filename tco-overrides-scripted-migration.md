---

copyright:
  years:  2024, 2026
lastupdated: "2026-11-25"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# How to convert TCO overrides to policies
{: #tco-overrides-policies}

A TCO override reroutes a subset of logs that would otherwise match a broader TCO policy. For an application and subsystem pair, you can set a different priority for all of its logs or only for specific log severities.
{: shortdesc}


## How do I convert an override to a policy using UI
{: #tco-overrides-policies-UI}
{: ui}

Overrides are a temporary mechanism that is being deprecated. You can convert an override to a TCO policy. All override rules are eventually converted to TCO policies automatically.

When you convert an override:

* The rule is removed from the override table.
* A new TCO policy is created with the same conditions and settings.
* The new policy is added to the top of the policy list and follows the policy execution order.
* You cannot move the policy back to the override table.

Complete the following steps to convert an override to a policy:

1. Open the {{site.data.keyword.tco-optimizer}} page. For more information, see [Accessing the {{site.data.keyword.tco-optimizer}}](/docs/cloud-logs?topic=cloud-logs-tco-optimizer#tco-access)

2. In the *Log overrides* section, select one of the override rule you want to convert. 

3. Click **Convert to policy**

4. In the **Convert override — confirmation required** window, click **Convert Override**.

To cancel the conversion, click **Cancel**.
A message confirms that the override rule was converted to a regular TCO rule. The new policy is displayed at the top of the policy list.


## How do I convert an override to a policy using script
{: #tco-overrides-policies-scripts}

An automated backend migration script converts all legacy TCO overrides in your account into standard TCO policies.

The migration has the following characteristics:

* **No policy limit check:** The script converts all existing overrides regardless of your account's policy limits. If the account has more than 200 policies after the migration, the migration still completes successfully.
* **Fixed global limit:** The global limit remains at 200 policies across all instances. The script doesn't raise this limit.


## Operational state and system behavior in the UI and API
{: #tco-overrides-using-script-behavior}

| Operational state       | System behavior and constraints  |
|-------------------------|-----------------------------------|
| Rendering and viewing   | UI displays accounts with more than 200 policies normally, and no data is lost |
| Modifying polices       | Update and edit existing policies normally, even when the account total exceeds 200    |
| Creating new policies   | Cannot create a new policy when the account has 200 or more policies. There are [X] of 200 policies. Delete one or more policies, and then try again | 
| Remediation path        | Administrators must delete unnecessary policies to bring the active count below 200. New policy creation is then unlocked |
{: caption="Operational state and system behavior" caption-side="bottom"}




