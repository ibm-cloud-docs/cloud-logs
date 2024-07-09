---

copyright:
  years:  2024
lastupdated: "2024-07-09"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.tco-optimizer}}
{: #tco-optimizer}

With {{site.data.keyword.logs_full}} data pipelines and the {{site.data.keyword.tco-optimizer}}, you can define the way logs are distributed across 3 distinct use cases. You can balance costs in the environment by using these pipelines.
{: shortdesc}

By defining the data pipeline based on the importance of the data to your business, the {{site.data.keyword.tco-optimizer}} can help you improve real-time analysis and alerting and helps you manage costs.

How logs are associated to pipelines is determined by policies. Policies are applied on combinations of applications, subsystems, and log severity as logs are ingested. Logs are assigned to the appropriate TCO pipeline based on the policy content. The default policy for all logs is high priority.

Policies simplify assigning TCO pipelines and capture applicable logs on ingestion. Each policy creates new default values for the logs for the applicable policy. If policies conflict, the first policy that is listed on the {{site.data.keyword.tco-optimizer}} page takes precedence.

The three TCO pipelines are:

{{site.data.keyword.frequent-search}}
:   Logs that require immediate access and full {{site.data.keyword.logs_full_notm}} analysis capabilities. These logs are typically high-severity or business-critical logs that need to be analyzed or queried individually.

{{site.data.keyword.monitoring}}
:   Logs that require processing and can be queried later if needed from an archive. These logs are typically logs used for monitoring and statistical analysis.

{{site.data.keyword.compliance}}
:   Logs that need to be kept for compliance or post-processing reasons but can be maintained and queried from an archive.

When you configure TCO policies, the selected priority determines the TCO pipeline for the logs that match the criteria.

| Priority value | TCO pipeline |
| -------------- | -------------- |
| `High` | {{site.data.keyword.frequent-search}} |
| `Medium` | {{site.data.keyword.monitoring}} |
| `Low` | {{site.data.keyword.compliance}} |
| `Blocked` | `[*]` |
{: caption="Table 1. Mapping of policy priority to TCO pipeline" caption-side="bottom"}
{: #tco_mapping}

`[*]` Logs matching policies with the `Blocked` priority are dropped and are not sent to any TCO pipeline.

All data is stored in the [{{site.data.keyword.cos_full_notm}} data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket), including logs that are `Blocked` by a policy.
{: note}

## Accessing the {{site.data.keyword.tco-optimizer}}
{: #tco-access}

Compete the following steps to access the {{site.data.keyword.tco-optimizer}}:

1. [Launch the {{site.data.keyword.logs_full_notm}} UI.](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

2. Click the **Data pipeline** icon ![Data pipeline icon](/icons/data-pipeline.svg "Data pipeline") > **TCO optimiser**.

The {{site.data.keyword.tco-optimizer}} page shows the percentage of ingested data that is flowing to each pipeline after the configured policies are applied.

## Creating a policy
{: #tco-optimizer-create-policy}

You must have a [{{site.data.keyword.cos_full_notm}} data bucket](/docs/cloud-logs?topic=cloud-logs-configure-data-bucket) configured before creating a policy.
{: important}

On the {{site.data.keyword.tco-optimizer}} page, complete the following steps to create a new policy:

1. Click **ADD NEW POLICY**.

2. Enter a policy name.

3. Enter the policy details with the relevant applications, subsystems, and severity. Add more criteria as needed.

   Logs received by {{site.data.keyword.logs_full_notm}} without a severity are treated as if their severity is `debug`.
   {: note}

   Create a parsing rule to set the priority of logs at ingestion when a priority value is not included.
   {: tip}

   For applications and subsystems, criteria can be specified when the value matches one of: `All`, `Is`, `Is Not`, `Includes`, or `Starts With`.

4. Set the priority for the policy. The priority determines the [pipeline](#tco_mapping) for logs that are matched by the policy.

5. Click **APPLY**.

## Modifying a policy
{: #tco-optimizer-modify-policy}

On the {{site.data.keyword.tco-optimizer}} page, complete the following steps to modify an existing policy:

1. Click the policy that you want to change.

2. Modify the criteria.

3. Click **APPLY**.

If you want to change the policy priority value, you can also change the priority in the **PRIORITY** drop-down list for the policy in the policy list. The priority determines the [pipeline](#tco_mapping) for logs that are matched by the policy.
{: tip}

## Deleting a policy
{: #tco-optimizer-delete-policy}

On the {{site.data.keyword.tco-optimizer}} page, complete the following steps to delete an existing policy:

1. Click the policy that you want to delete.

2. Click **DELETE**.

3. Confirm that you want to delete the policy.
