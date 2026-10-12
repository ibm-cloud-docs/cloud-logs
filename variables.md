---

copyright:
  years:  2024, 2026
lastupdated: "2026-10-10"

keywords:

subcollection: cloud-logs

---

{{site.data.keyword.attribute-definition-list}}

# Working with variables in {{site.data.keyword.logs_full_notm}} dashboards
{: #variables}

In {{site.data.keyword.logs_full}}, use variables to build flexible and interactive *Custom Dashboards*. A variable is a placeholder for a value that is used in queries. When used in custom dashboards, your dashboard's queries update to display data for the value of the variable that is selected.
{: shortdesc}

Variables make dashboards more interactive and dynamic. Instead of putting specific names for servers, applications, or sensors in your queries, you can use variables instead. You can easily switch between different data views. For example, if you have complex, high-cardinality metrics, you can add variables to zoom in on specific values that you care about. Variables can be used across widgets for all data types, regardless of the variable source type.

## Variable methods in {{site.data.keyword.logs_full_notm}} custom dashboards
{: #variables-methods}

A variable method defines how the values for the variable will be entered, retrieved, or calculated.

The following methods are availble:

Static-value variables
:   Use static-value variables to manually define a fixed list of variable values, such as a number or a string of numbers separated by a comma. For example, if you have country names that never change, you might want to create them as a static-value variable. Supports the following variable types: `single-string`, `multi-string`.

Query variable
:   Use query variables to retrieve values from logs or metrics data. For example, a query variable can generate a list of server names, sensor IDs, or data centers, dynamically updating the values by fetching options by using a data source query. Query variables are beneficial when multiple data source instances are managed, specially across diverse environments. Supports the following variable types: `single-string`, `multi-string`, `numeric`.

Text Box
:   Use a text box to allow users to enter manually input values. Supports the following variable types: `single-string`, `numeric` , `regex`, `Lucene`, `interval`

Some methods support both single and multiple values. A query-based method, for example, may return multiple values, but whether the variable accepts multiple selections depends on the value type (single-string vs. multi-string).

## Variable types in {{site.data.keyword.logs_full_notm}} custom dashboards
{: #variables-types}

A variable type determines which values the variable selects.

You can choose from different variable types and methods:

| Value Type              | Description                            | Supported Methods  | Example Use Cases    |
|-------------------------|----------------------------------------|--------------------|----------------------|
| **Single string**       | A single value is selected or entered  | [Static values](#static-values-method), [Text box](#text-box-method), all [Query](#query-method) (All sources: DataPrime, metrics, logs) | Filter one service or region   |
| **Multi-string**        | One or more values are selected        | [Static values](#static-values-method), [Query](#query-method) (All sources: DataPrime, metrics and logs) | Filter  multiple environments or error codes     |
| **Single Numeric**      | A single number is selected or entered | [Text box](#text-box-method), [Static values](#static-values-method), [DataPrime query](#dataprime)     | Filter a thresholds, percentile selection, or scaling factor  |
| **Regex**               | One or more values are selected based on the pattern-matching expression that is entered  | [Text box](#text-box-method)        | Filter values based on  logs that match the wildcard/pattern filter    |
| **Lucene Query**        | A structured Lucene query              | [Text box](#text-box-method)    |            |
| **Interval**            | A time duration (e.g., `15m`, `1h`, `1d`) is entered | [Static values](#static-values-method), [Text box](#text-box-method)       | Bucket size for charts, rolling windows, step sizes for range selectors |
{: caption="Variable types in Dashboards" caption-side="bottom"}



## How variable values are resolve in {{site.data.keyword.logs_full_notm}} dashboards
{: #variables-values}

Single-value
:   The user can choose only 1 value for a specific variable.

    Variables are inserted as-is.

    A `None` selection resolves to an empty string, for example, `Errors for ${service}` becomes `Errors for`.

Multi-value
:   The user can select multiple values within a specific variable.

    Variables are joined with a comma and a space, for example `service-a, service-b, service-c`.

    When the resolved list is too long to fit, the name truncates with an ellipsis and shows the full list in a tooltip on hover.

Include all
:   The user can select one or more values.

    When `All (*)` is selected, the name shows `All (*)`, or the custom label configured for the `Include All` option.



## Display options in {{site.data.keyword.logs_full_notm}} custom dashboards
{: #variables-display}

Display options in the variable editor control how the variable appears in the dashboard toolbar.

To define how a variable shows in the dashboard, choose one of the following options:

- **Name & Value**: Displays the variable's display name and its current selection. This is the default option.

- **Value Only**: Displays the selection alone, without the name.

    Use when the name is obvious from the values and you want to save toolbar space.

- **None**: The variable does not appear in the toolbar at all.

    Use to hide a variable that a query needs but a viewer should not change. It removes the control from the toolbar.

    For example, you can use it for a variable that only exists to feed another variable. The variable still resolves normally in every query that references it.


When you use the `Textbox` method for a variable, you also have the option to enable `Open as a full row`.
- When you turn on `Open as a full row`, the variable takes an entire row in the dashboard toolbar instead of sharing one with other variables.
- Use it for variables with long values or many selections, where the collapsed control would otherwise truncate.


## Format display values in {{site.data.keyword.logs_full_notm}} custom dashboards
{: #variables-format-display-values}

Use named regex capture groups to specify which part of the value should be displayed in the values list.

For example, if the query returns values like `service-dev` or `service-prod`, use `service-(\w+)` to display only dev and prod. The variable still resolves to the full original value in queries.

If no groups are defined, the full match is used for both display and value.


## Sort values in {{site.data.keyword.logs_full_notm}} custom dashboards
{: #variables-sort-display-values}

Sort values alphabetically by choosing `Alphabetical (asc)`or `Alphabetical (desc)`.

Unsorted keeps whatever order the source returned, which for a query-backed variable is the order the query produced.



## Filter display values in {{site.data.keyword.logs_full_notm}} custom dashboards
{: #variables-filter-display-values}

Filter the full list of values using a regex pattern.

Only values that match the pattern will appear in the dashboard.

For example, use `/frontend.*/` filters to display values for services starting with `frontend`.



## Adding variables in {{site.data.keyword.logs_full_notm}} custom dashboards
{: #variables-define}

Complete the following steps to add variables to {{site.data.keyword.logs_full_notm}} custom dashboards:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. [Access your {{site.data.keyword.logs_full_notm}} instance](/docs/cloud-logs?topic=cloud-logs-instance-launch#instance-launch-cloud-ui)

3. Click the **Dashboard** icon ![Dashboards icon](/icons/dashboards.svg "Dashboards icon") > **Custom dashboards**.

4. In a new or existing dashboard, click ![Managed Variable icon](/icons/dashboards.svg "Dashboed Variable iconards").

5. Add a new variable by clicking **+ Variable**.

6. In the *Details* section, configure the following fields:

   * `Variable name`: The text that is entered in this field determines how the variable name appears in your query, for example, `{{ podvalues }}`. No capital letters or spaces are allowed in the variable name.

   * `Display name` (optional). The text that is entered in this field appears in the selection as part of the drop-down list, for example, "My Pods".

   * `Description`: Description of the variable.

7. In the *Configuration* section, select a variable type and a method:

    * `Variable type`: Choose the type of value this variable should accept to determine how values can be entered or queried.

        Valid values are: `Multi-string`, `Single-string`, `Regex`, `Lucene query`, and `Interval`.

    * `Method`: Choose how values will be provided from a static list, query, or free-text input.

        Valid values are: `Static`, `Query`, and `Text Box`.

8. Configure the *Display Options* section.

9. Click **Save**.
