# Query speed optimization (timeout)

By default, all queries have timeout. If you have timeout error - try to implement speedup strategy.

We use clickhouse with partition by gen\_utime, shard, workchain.

1. Always use time filters: `gen_utime__gt` and `gen_utime__lt`, use your business logic to find the right numbers. Do not run search on all 500m transactions
2. Use more filters. If you know that it's NFT item - use get method filter, for example. More filter = fewer results = faster search.
3. Use less columns - query not all columns in database, just only needed ones.&#x20;
