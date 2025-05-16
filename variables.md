---

copyright:
  years:  2024, 2025
lastupdated: "2025-05-16"

keywords: 

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Creating and managing variables
{: #variables}

In {{site.data.keyword.logs_full}}, a variable is a placeholder for a value that is used in queries. When used in custom dashboards, your dashboard's queries update to display data for that value.
{: shortdesc}

Variables make dashboards more interactive and dynamic. Instead of putting specific names for servers, applications, or sensors in your queries, you can use variables instead. You can easily switch between different data views. This means that if you have complex, high-cardinality metrics, you can add variables to zoom in on specific values that you care about. Variables can be used across widgets for all data types, regardless of the variable source type.

## Variable types
{: #variables-types}

You can choose from different variable types.

Static-value variables
:   You can manually define a fixed list of variable values, such as a number or a string of numbers separated by a comma. For example, if you have country names that never change, you might want to create them as a static-value variable rather than a data source query variable.

Query variable
:   Variable values are retrieved from a logs or metrics data source query. For example, a query variable can generate a list of server names, sensor IDs, or data centers, dynamically updating the values by fetching options by using a data source query. Query variables are beneficial when multiple data source instances are managed, especially across diverse environments.

## Defining variables for custom dashboards
{: #variables-define}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Dashboard** icon ![Dashboards icon](/icons/dashboards.svg "Dashboards") > **Custom dashboards**.

4. In a new or existing dashboard, click the **Managed Variable** icon **{ }**.

5. Click **+ Variable**.

6. For all variable types, configure the following fields:

   * [Variable type.](#variables-types)

   * Variable name. The text that is entered in this field determines how the variable name appears in your query, for example, `{{ podvalues }}`. No capital letters or spaces are allowed in the variable name.

   * Display name (optional). The text that is entered in this field appears in the selection as part of the drop-down list, for example, "My Pods".

   * Selection option.

      Multi-value
      :   *Multi-value* specifies that the user can select multiple values within a specific variable. Some queries do not support multiple values, such as `{{ variablename }}`. Choose this option only if your query supports multiple values.

      Include all
      :    *Include all* can be selected when the multi-value option is enabled. The query will select all available and future values for a specific time frame, regardless of your specific selection.

      When both options are selected, all variable options are selected by default, and one or more can be deselected. If neither option is specified, you can select one variable value at a time.

7. For `query` type variables:

   * Specify the query source (`logs` or `metrics`).

   * For `variable type` specify `values` for `logs`. For `metrics` specify `metric names`, `metric labels`, or `label values`. If you select `metric labels`, select the label to be used for the displayed values.

   * For `logs`, define the field by selecting a log key that you want to query. A list of current variable values are displayed in the **Values Preview** in alphanumeric order.

   * For `metrics`, in **Metrics regex**, enter a regex expression to fetch the list of metrics that you would like displayed. For example, `^kube(.*)` returns all metric names that begin with kube.

      * For `label values`, for **Metric label**, choose the label for the displayed values. Make the label dynamic by inserting a variable, for example `Pod Name = {{ pod }}`.

      * For `label values`, for **Label filters**, create one or more nested variables and an extra filter layer for your query. For example, you can choose to filter the labels by cluster by selecting a value that is `{{ podvalue }}` or the hardcoded name of your cluster.

      * For `metrics`, for **Variable value display name**, define how the values are displayed in the drop-down selection list.

         A list of current variable values for the field is displayed in the **Values Preview**.

   * For **Sort values**, select how to sort the data in the **Values Preview**.

8. Click **Save**.

Variables can also be edited or deleted from the list of defined variables.

## Using variables in queries
{: #variables-queries}

In addition to using variable in custom dashboards, you can use defined variables in Lucene, DataPrime, and PromQL queries.

### Lucene queries
{: #variables-lucene}

You can use defined variables in Lucene queries. For example, `product_id:{{ pid }}` where `pid` is the variable name (not the display name),

### DataPrime queries
{: #variables-dataprime}

After a variable is created, the variable values that are chosen by the user can be used as [query parameters](/docs/cloud-logs?topic=cloud-logs-query-parameters) in a DataPrime query by using `$p.<variable_name>`.

### PromQL queries
{: #variables-promql}

Use `{{ variable_name }}` in the PromQL query language.

For example, the PromQL query `sum(kube_pod_owner{pod=~"{{ pod }}"})` is used to aggregate metrics that are related to Kubernetes pods. `{pod=~"{{ pod }}"}` is a label selector that filters the `kube_pod_owner` metric for the specific pod whose name matches the variable's value. The `{{ pod }}` placeholder is a template variable, which replaces the actual pod name when the query is run.

You can also use predefined variables in your PromQL query.

| Variable | Description | Examples |
|----------|-------------|---------|
| `${__range}` | This variable represents the duration of the dashboard time range. It is rendered as an interval string supported by PromQL. For example, if you select a time range from `13.00` to `14.30`, then the `${__range}` variable is calculated as `90m`. |	`1d`, `5m` |
| `${__range_s}` | Calculated as the number of seconds in the selected time frame. | `60s`, `180s` |
| `${__range_ms}` |	Calculated as the number of milliseconds in the selected time frame. | `60ms`, `180ms` |
{: caption="Predefined PromQL variables" caption-side="bottom"}

For example, you might use the `__range variable` in `sum_over_time`.

```text
sum_over_time(kube_pod_owner[${__range}])
```
{: codeblock}
