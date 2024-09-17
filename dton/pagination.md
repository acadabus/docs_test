# Pagination

### Pagination with cursor

{% hint style="info" %}
`page_size`parameter is diffrent for rates. Check [@dtontech\_bot](https://t.me/dtontech\_bot) for getting your rate max `page_size`
{% endhint %}

You can fetch transactions with `page_size` and cursor: `gen_utime__gt` or `lt__gt`

For raw\_transactions you can use `gen_utime__gte / lt__gte / gen_utime__lte / lt__lte`&#x20;

* Be careful, with `gte` you need to store transaction `hash`, and next request must be processed after `hash` column appears
* For account\_states you can also use `lt__gte` but if some accounts will be updated you will get duplicated `workchain` / `address` (with bigger `lt` than previous) so it's better to use dict and update result in dict for `workchain:address` key

```graphql
{
  raw_transactions(
    workchain: -1
    address: "5555555555555555555555555555555555555555555555555555555555555555"
    order_by: "lt"
    order_desc: true
    lt__gte: "40379620000003" # pass last lt from prev request here
    page_size: 150 # max transactions per 1 request
  ) {
    address
    workchain
    lt
    hash
  }
}
```

<details>

<summary>Pagination with page (not stable, deprecated)</summary>

We use pagination in every table, to use it, please, use `page` and `page_size` parameters.&#x20;

Max value for `page_size` in any table is 150.

`page` parameter started from `0`

Example usage:

```
{
  blocks(page: 0, page_size: 150) {
    gen_utime
    seqno
    workchain
    shard
  }
}
```

</details>

