---

copyright:
  years:  2024, 2026
lastupdated: "2026-04-01"

keywords:

subcollection: cloud-logs


---

{{site.data.keyword.attribute-definition-list}}


#  Pipeline analyzer
{: #pipeline-analyzer}

In {{site.data.keyword.logs_full_notm}}, you can use the pipeline analyzer to .......
{: shortdesc}
In complex environments, logs often flow from multiple services, teams, and infrastructure. To handle this scale, many teams create customized processing pipelines—for security, compliance, observability, and more. These pipelines parse, enrich, and route logs based on TCO policies, enabling advanced monitoring and faster issue resolution.
But as environments grow, pipelines multiply, and misconfigurations, conflicting rules, or visibility gaps can lead to incorrect parsing, broken dashboards, and monitoring failures.
The Pipeline Analyzer is a no-code tool designed to solve these challenges. Use it to inspect logs in real time as they move through your pipelines, providing complete transparency into parsing, enrichment, and routing behavior.

(Image)
With the Analyzer, teams can trace log processing flows in order to:
- `Visualize the full processing flow of logs on demand`
- `Compare raw and modified logs`
- `Troubleshoot pipeline behaviour with pinpoint accuracy`

## How it Works
{: #pipeline-analyzer-how-it-works}
1. Parsing rules to extract structure
2. Enrichments to add context
3. TCO pipelines to optimize and route

(image)

At present, Pipeline Analyzer visualizes the parsing rule pipeline.

## Start using Pipeline Analyzer
{: #pipeline-analyzer-start-using-pipeline-analyzer}
To get started, navigate to **Data Flow > Pipeline Analyzer**

## Capture and Filter Logs on Demand
{: #pipeline-analyzer-capture-and-filter-logs-on-demand}
Use filters to capture only logs that match your criteria:
- `application`
- `subsystem`
- `severity`
- `regex`

Only those logs meeting your filter criteria are streamed.

## Inspect real-time Log Processing
{: #pipeline-analyzer-inspect-real-time-log-processing}
Watch logs as they’re ingested and see which parsing rules ran and how they affected the log.
Select Play to start streaming logs in real-time.

(Video)

As logs appear in the stream, each entry shows:
- `Timestamp`
- `rules summary (applied rules)`
- `raw log content`
- `ingested log (after parsing)`

Use Pause or Clear to stop or reset the stream.

## Simulate Parsing with Raw Logs
{: #pipeline-analyzer-simulate-parsing-with-raw-logs}
Double-click a log entry or select the arrow (▶) to view its raw and modified versions. This gives you a detailed view of how the log changes at each processing stage.
Paste a raw log sample into the Analyzer to test parsing behavior.
Hover over any ingested log to download the raw version.
To download the raw version of an ingested log, hover over the log entry and select  Download.

## View Applied Rules
{: #pipeline-analyzer-view-applied-rules}
Select one or more logs to view their applicable rules in the right-hand panel.

(Image)

The parsing rule panel displays:
- `All applicable rule groups`
- `The specific rules within each group`
- `The order of execution`
- `The option to Show only applied rules`
Use the Drawer toggle to expand or collapse the Rule Panel.

## Campare Raw and Parsed Logs
{: #pipeline-analyzer-compare-raw-and-parsed-logs}
Use Compare mode to see how parsing rules transform your logs. The view displays the raw log alongside the ingested log, allowing you to identify the changes that occurred during processing quickly.

### View Logs Side by Side
{: #pipeline-analyzer-view-logs-side-by-side}

Compare mode opens a split view:
- `The left panel shows the raw log exactly as it was received`
- `The right panel shows the ingested log after parsing rules are applied.`

Use this view to trace changes and confirm that your parsing rules work as intended.

### Identify Changes
{: #pipeline-analyzer-identify-changes}
Compare mode highlights differences between the two versions of the log so you can:
- `Move between rules using (arrow) and (downarrow.`
- `Track added, removed, or modified fields and values`
- `Verify how specific rules affected log content.`
- `Detect unexpected transformations or missing data.`
(Image)

Once you select a log, you can view all changes or focus on a specific rule group. To reduce noise, switch the rules view to Effective rules to focus on rules that changed the log.

### Inspect rule-level Transformations
{: #pipeline-analyzer-inspect-rule-level-transformations}
To analyze rule-level changes:
- `The left panel shows the log input before the rule is applied.`
- `The right panel displays the log output after the rule has run.`

This comparison helps you validate parsing logic, troubleshoot issues, and confirm that rule order and behavior match your expectations.

## Troubleshoot Parsing and Rule Behaviour
{: #pipeline-analyzer-troubleshooting-parsing-and-rule-behaviour}
Using the Analyzer, you can instantly identify:
- `which pipelines and rules modified a specific log.`
- `Logs affected by a particular rule.`
- `How a specific rule changes a log.`
- `Parsing issues caused by overlapping rules or incorrect configurations.`

## Permissions
{: #pipeline-analyzer-permissions}
To use the Pipeline Analyzer, users need the following permission:

(table)

See the full guide on roles and permissions.

## Limitations
{: #pipeline-analyzer-limitations}
- `Logs are not saved after you leave the page.`
- `Each session is limited to 2,000 logs or 10 minutes—whichever comes first.`
- `Currently supports parsing rules only (TCO and enrichment visibility coming soon)`
