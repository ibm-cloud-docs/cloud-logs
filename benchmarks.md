---

copyright:
  years:  2023, 2024
lastupdated: "2024-06-13"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}



# Using benchmark tags
{: #benchmarks}

Version benchmark tags can be used as a representation of any significant change or event that might impact your system. They can be received automatically from your CI/CD pipelines or inserted manually.
{: shortdesc}

Version benchmark tags are a way for you to understand your version status at a glance, integrate with your deployment pipeline, and get your latest build status. 


## Creating a benchmark tag
{: #create_tag}

<!-- Launch the UI step -->
{{site.data.content.launch-ui}}

2. Click the **Dashboards** icon ![Dashboards icon](/icons/dashboards.svg "Dashboards") > **Version benchmarks**.

3. Click **New Tag**.

4. Enter a description for the tag.

5. Enter the tag content including the timeframe associated with the tag and the applications and subsystems associate with the tag.

## Tag usage
{: #tag_usage}

Version benchmark tags can be used to track scenarios similar to the following:

* View the change in triggered anomalies, alerts, error volume, newly introduced errors, and high severity logs ratio since the tag time. Compare this to the corresponding timeframe in the comparison tag.

* View the number of errors since the tag in comparison to the period prior to the tag.

* View the number of alerts since the tag, grouped by alert name and compared to the previous period.

* View the errors that arrived in numbers greater than their normal ratio since the tag.

* View the logs appearing on your system for the first time since the tag.

<!--
Deployment Pipelines
Integrate with any of the following deployment pipelines.

Bitbucket
Azure DevOps Server
GitLab
Argo CD
Spinnaker
Heroku Pipelines
Version Tags using cURL
-->
