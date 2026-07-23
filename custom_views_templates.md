---

copyright:
  years:  2024, 2026
lastupdated: "2026-07-23"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a custom view as a template
{: #custom_views_templates}

In {{site.data.keyword.logs_full}}, you can create 1 or more views as templates.
{: shortdesc}

Consider the following information when creating a custom view as a template:

- A public custom view is visible to all team members who have `Reader`, `Writer` or `Manager` access.

- A private custom view is only visible to the user who created the view.

- Users with `Reader` role cannot create, modify or delete views.

- Users with `Writer` or `Manager` role can create, modify and delete views.





## Create the custom view as a template
{: #custom_views_templates_create}


Complete the following steps to create a custom view that you can use as a template:

1. [Launch the UI through the IBM Cloud UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

2. Click the **Explore logs** icon ![Explore logs icon](/icons/explore.svg "Explore logs"). Then, click **Logs**.

3. Set up the **Explore Logs** page with the column layout, view modes, and filters.

4. Click the three dots next to the view name and click **Save view**.

5. Enter a name that identifies the view. Use a naming convention so it is clear that you plan to use this view as a template, for example, you can name your template as follows `Template - <Title>`.

6. Select **Save query and filters** if you want filters and query to be part of the template.

7. Set the **Visibility** to **Public**.

8. Click **Save**.
