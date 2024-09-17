# Filters

### Filtering data in a request

You can apply filters to any field depending on type.\
Syntax:\
`field__filter`\
\
Example:

```graphql
{
  transactions(parsed_dns_domain__contains: "dton"){
    address
    workchain
    parsed_dns_domain
  }
}
```

**Available filters:**

* `exact` - Exact match (this is default one when you use `seqno: 1` e.g.)
* `contains` - Case-sensitive containment test
* `in` - In a given list
* `gt` - Greater than
* `gte` - Greater than or equal to
* `lt` - Less than
* `lte` - Less than or equal to
* `range` - In a given range `[val_from, val_to]`, both included
* `isnull` - Takes either `True` or `False`, which correspond to SQL queries of `IS NULL` and `IS NOT NULL`, respectively
* `friendly` - Filter by user-friendly form of address. Accepts bounceable, non-bounceable and raw form (workchain:address)
* `friendly_in` - Filter on a list of addresses in user-friendly form. Accepts bounceable, non-bounceable and raw form (workchain:address)

### AND / OR / NOT

1\. `and__`: This filter is used to apply a logical AND to multiple conditions. (default one when you use several keys: `{workchain: -1, seqno: 1}` = `workchain = 1 AND seqno = 1`

```graphql
{
  transactions(
    and__: [{workcain: -1, seqno: 1}, {seqno: 2}]
  ) {
    seqno
    workcain
  }
}
```

2\. `or__`: This filter is used to apply a logical OR to multiple conditions.

```graphql
{
  transactions(
    or__: [{seqno: 1}, {seqno: 2}]
  ) {
    seqno
    shard
  }
}
```

3\. `not__`: This filter is used to negate a condition.

```graphql
{
  transactions(
    not__: {seqno: 1}
  ) {
    seqno
    shard
  }
}
```

Nested Filters (max depth: 3)

```graphql
{
  transactions(or__: [
      {seqno: 0}, 
      {seqno: 1}, 
      {seqno: 2}, 
      {and__: {seqno__gt: 10, seqno__lte: 15}}]) {
    seqno
  }
}
```

