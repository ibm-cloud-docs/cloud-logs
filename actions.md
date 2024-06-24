---

copyright:
  years:  2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}


# Using actions in {{site.data.keyword.logs_full_notm}} to integrate with third-party services
{: #actions}

In {{site.data.keyword.logs_full_notm}}, you can trigger third-party services based on your search results and values and send data to those services.
{: shortdesc}

## Creating an action
{: #create-action}

To create an action:

1. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

2. In the **Logs** view, click the ![Settings icon](/icons/setting.svg "Settings icon") **Settings**. This settings icon is not the same as the icon in the left navigation. The settings icon can be found in the logs view in the upper-right of the page.

3. Click **Manage Actions**.

4. Click **Add New Action**.

5. For **Untitled Action**, specify a name for your action.

6. In the **URL TEMPLATE**, enter the URL for the external service. For example, `https://test-my-url.com?type={{ $m.subsystemName === "frontend" ? "Front" : "Back" }}`. Only `http://` and `https://` are supported.

   JavaScript syntax is supported. For example, you can specify conditions such as `{{ condition ? "true value" : "false value" }}`. Most JavaScript functions are supported.

   You can include [variables](#action-variables) to pass data on the URL. If you type double-curly braces (`{{}}`), a list of available variables is displayed.

7. Select the **data type** associated with the action. The action is displayed in the selected context.

8. Click **Advanced** to access optional settings.

9. To make the action public, toggle **Make Public when saved**.

10. To limit the action to specific **Applications** or **Subsystems**, select values from the list.

11. Click **Save Action**

## Editing an action
{: #edit-action}

To edit an existing action:

1. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

2. In the **Logs** view, click the ![Settings icon](/icons/setting.svg "Settings icon") **Settings**. This settings icon is not the same as the icon in the left navigation. The settings icon can be found in the logs view in the upper-right of the page.

3. In the list of actions, click the action to change.

4. Make your changes.

5. Click **Save Action** to save your changes or **Reset** to revert the action to the last saved version of the action.

## Cloning an action
{: #clone-action}

If you want to create a new action based on an existing action, you can clone an action.

1. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**

2. In the **Logs** view, click the ![Settings icon](/icons/setting.svg "Settings icon") **Settings**. This settings icon is not the same as the icon in the left navigation. The settings icon can be found in the logs view in the upper-right of the page.

3. In the list of actions, hover over the action you want to clone.

4. Click the **Clone** icon. A duplicate of your action is created.

5. [Edit](#edit-action) the cloned action and make your changes.

6. Click **Save Action** to save your changes.

## Displaying and hiding actions on the actions menu
{: #action-display}

You can configure whether actions can be [triggered](#action-trigger) by users.

1. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

2. In the **Logs** view, click the ![Settings icon](/icons/setting.svg "Settings icon") **Settings**. This settings icon is not the same as the icon in the left navigation. The settings icon can be found in the logs view in the upper-right of the page.

3. In the list of actions, click the action that you want to configure.

4. Click the **Hide from actions menu** icon to not have the action included for users in the actions menu. Click the **Show on actions menu** icon to have the action included in th actions menu.

## Triggering an action
{: #action-trigger}

Trigger an action by doing the following steps:

1. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

2. Click displayed data in view. A menu is displayed.

3. Hover over actions. The list of available actions is displayed.

4. Click the action to trigger the action.

   Only actions configured to be [displayed in the actions menu](#action-display) are listed in the actions menu.
   {: note}


## Deleting an action
{: #action-delete}

1. In the left navigation, click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs") > **Logs**.

2. In the **Logs** view, click the ![Settings icon](/icons/setting.svg "Settings icon") **Settings**. This settings icon is not the same as the icon in the left navigation. The settings icon can be found in the logs view in the upper-right of the page.

3. In the list of actions, click the action that you want to delete.

4. Click **Delete**.

   The deletion is done immediately. You are not asked to confirm that you want the action to be deleted.
   {: important}


## Variables that can be included in an action
{: #action-variables}

You can specify variables in a URL template to pass information to your external service.

The following variables are supported:

`$m.<metadata>`
:   Metadata variables are available in the logs. For example, `$m.applicationName` or `$m.timestamp`.

`$d.<key>.<subkey>` 
:   Data that is available in the log. For example, `$d.kubernetes.labels.my_label`.

`$p.start_time`
:   The start of the selected time range as a Unix epoch timestamp, in milliseconds.

`$p.end_time`
:   The end of the selected time range as a Unix epoch timestamp, in milliseconds.

`$p.selected_value`
:   The value selected by the user in the UI. If activated by clicking a key, the entire value of the key is included.

## Example action
{: #action-example}

The following action generates a Jira issue.

```text
http://<company_name>.atlassian.net//secure/CreateIssueDetails!init.jspa?pid=<Jira_PID>&issuetype=<Jira_issueType>&description={{$d.logRecord.body}}&summary={{$d.msg}}
```
{: codeblock}

