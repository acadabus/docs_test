# Architecture

We use a column database to handle queries. This means that the fewer columns you query, the faster your query will be executed.

We also separate low-level work with data from high-level.

### Low-level methods

* `blocks` - all blocks in network
  * `blocksCount` - # total blocks in database
* `raw_transactions` - all transactions in network with actual account state on this transaction
  * `transactionsCount` - # total transactions in database
  * `accountTransactionCount` - count transactions by account
  * `transactionsAfterTimestamp` - get transactions after some time point
  * &#x20;`lastTransactionCountSegments` - transactions count by segment `'hour', 'minute', 'day'`
  * `lastTransactionCount` - # of transactions for 24h
* `raw_account_states` - the latest transaction (with block and account state inside) for each account on network, including deleted ones

Blocks and transactions contains all TLb fields from [block.tlb](https://github.com/ton-blockchain/ton/blob/master/crypto/block/block.tlb) separated by `_`

`Transactions` TLb scheme concatenated with `AccountStatus` which gave you ultimate opportunity to use accounts data & code for every transaction to validate data.

Also, we add many other fields for every model which are needed for development, more information can be founded in detailed model documentation.

### Aggregations

You can do aggregations for transactions and account\_states, check out:&#x20;

{% content-ref url="aggregations.md" %}
[aggregations.md](aggregations.md)
{% endcontent-ref %}

### Mutations

* `run_method` - run any method in smart contracts with low-level parameters

### Other methods

* `tonPrice` - get TON price by days
* `getTPS` - transactions per second
* `getTPM` - transactions per minute
* `run_transaction` - run any transaction in network

