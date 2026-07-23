---

copyright:
  years:  2024, 2026
lastupdated: "2026-07-23"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Using public views as templates
{: #custom_views_templates}

In {{site.data.keyword.logs_full}}, you can use a public view to allow a team member publish a view that has a consistent column layout, view mode, and filter configurations. The team members can open the public view, and set it as their own default view.
{: shortdesc}


Complete the following steps to create a custom view that you can use as a template:

## Launch the {{site.data.keyword.logs_full_notm}} UI
{: #custom_views_templates_step1}
{: step}

[Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

## Create the custom view
{: #custom_views_templates_step2}
{: step}

1. Set up the **Explore Logs** page with the column layout, view modes, and filters.

2. Click the three dots next to the view name and click **Save view**.

3. Enter a name that identifies the view. Use a naming convention so it is clear that you plan to use this view as a template, for example, you can name your template as follows `Template - <Title>`.

4. Select **Save query and filters** if you want filters and query to be part of the template.

5. Set the **Visibility** to **Public**.

6. Click **Save**.

The custom view is visible to all team members who have *Reader*, *Writer* or `Manager` access.

Notice that users with `Reader` role cannot modify the view.
