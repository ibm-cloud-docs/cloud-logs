## Specify the logs that will be analyzed against the filtering criteria
{: step}
{: #alerts-config-3}
{: ui}


Complete the following steps to specify the logs that will be analyzed against the filtering criteria:

1. Specify a `Lucene` search query to specify the logs that will be returned as part of the alert.

    You can define a query that filters based on a free text string. For example, to trigger an alert when POST requests that have a return code of 403 are identified, you can enter `"POST 403"` as your search query. The query will look for logs that include the value `403` and `POST`.

    You can define a query that filters logs where a specific field matches the value in the query. For example, you can define a query to search for the value production in the environment field: `environment:"production"`

    You can define a query that filters logs where a specific field matches a range of numeric values using the format `[START_VALUE TO END_VALUE]`. For example, to search for logs that have 2xx status codes for a field `RC`, you can use the query: `rc.numeric:[400 TO 499]`

    You can define a query that filters logs where a specific field matches a regular expression (RegEx). Wrap the RegEx expression with `/`. For example, you can define a query to search for different regions such as `west-europe-1, west-europe-2, west-us-1` in a field region: `region:/west-(europe|us)-[12]/`

    You can define complex queries that use the Boolean operators `AND`, `OR`, and `NOT`. For example, you can define a query such as `environment:"production" AND status.numeric:[400 TO 499] NOT region:/west-(europe|us)-[12]/`

2. Add additional filtering of logs by choosing 1 or more applications.

3. Add additional filtering of logs by choosing 1 or more subsystems.

4. Add additional filtering of logs by choosing 1 or more log severites.

    Valid values are: `Debug`, `Verbose`, `Info`, `Warning`, `Error`, and `Critical`.
