# Aggregations

You can use the `groupTransactions` and `groupAccountStates` endpoints to perform aggregation operations. These endpoints support various aggregation functions and allow for grouping, sorting, and filtering of results.\
\
Example:

```graphql
{
  groupTransactions(
    by: ["parsed_dns_domain"],
    aggregations: [
      {field: "in_msg_value_grams", operation: "sum"},
      {operation: "count"}
    ],
    order_by: "in_msg_value_grams__sum",
    order_desc: true,
    page: 0,
    page_size: 5000,
    filter_by: {and__: [
      {parsed_dns_domain__contains: "ton"},
      {gen_utime__lt: "2024-01-01 00:00:00"}
    ]}
  ) {
    parsed_dns_domain
    count
    in_msg_value_grams__sum
  }
}
```

### Explanation of Parameters

* **`by`**: List of Strings -  Fields by which to group the results.
  * You can use all fields of block, transactions and account states. Check out raw\_transactions for all available fields in result.
  * For some fields, you can apply functions.&#x20;
    * For example, you want to group by month, you can use: `by: ["gen_utime__toYYYYMM"]`
    * Currently, allowed functions: `['toYYYYMMDD', 'toYYYYMM', 'toYear']`
* **`aggregations`**: List of Aggregation Objects - Specifies the fields to aggregate and the operations to perform. Each object includes:
  * **field**: The field to aggregate on (optional for `count`).
  * **operation**: The aggregation operation (e.g., `sum`, `count`).
* **`order_by`**: String - The field to sort the results by. Can be a simple field name or an aggregation field in the format `field__operation`.
* **`order_desc`**: Boolean - Specifies the sorting order. `true` for descending order, `false` for ascending order.
* **`page`**: Int - The page number for pagination (default is 0).
* **`page_size`**: Int - The number of results per page (default is 50).
* **`filter_by`**: Filtering Expression - A set of conditions to filter the data.

### Available Aggregation Operators

* **`count`**: Counts the number of items.
* **`sum`**: Sums the values of a field.
* **`min`**: Finds the minimum value of a field.
* **`max`**: Finds the maximum value of a field.
* **`avg`**: Calculates the average value of a field.
* **`argMax`**: Finds the value of another field corresponding to the maximum value of the target field.
* **`argMin`**: Finds the value of another field corresponding to the minimum value of the target field.
* **`least`**: Finds the least value among the specified fields.
* **`quantile`**: Calculates the quantile value of a field.

### Notes

Aggregation operations can be computationally expensive; consider limiting the scope using `filter_by` and pagination parameters (`page` and `page_size`).
