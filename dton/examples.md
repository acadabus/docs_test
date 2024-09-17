---
description: Usage examples
---

# Examples

<details>

<summary>Get all NFT items for collection</summary>

```graphql
{
  raw_account_states(
    account_state_state_init_code_method_name: "get_nft_data"
    parsed_nft_collection_address_address__friendly: "EQBPa7td5VDwGltzeSzsp32MkzqzlqHjAOsKtaX0mkMJhq_B"
    order_by: "parsed_nft_index"
    order_desc: true
    parsed_nft_true_nft_in_collection: 1, # Check that collection approve NFT with such address
    account_deleted: 0 # Account not deleted
  ){
    nft_address: address
    nft_workchain: workchain
    nft_index: parsed_nft_index
    
  	collection_address: parsed_nft_collection_address_address
    collection_workchain: parsed_nft_collection_address_workchain
    
    parsed_nft_content_storage_type
    parsed_nft_content_offchain_url
  }
}
```

</details>

<details>

<summary>Get all wallets for Jetton</summary>

```graphql
{
  jetton: raw_account_states(
    address__friendly: "EQALfk9nvSBhxD41SmFO3aM3R51CINSPs-ZUTAO2fz7bIJB8",
    account_deleted: 0 # Account not deleted
  ) {
    jetton_address: address
    jetton_workchain: workchain
    total_supply: parsed_jetton_total_supply
    symbol: parsed_jetton_content_symbol_value
    name: parsed_jetton_content_name_value
    image: parsed_jetton_content_image_value
  }
  
  wallets: raw_account_states(
    account_state_state_init_code_method_name: "get_wallet_data"
    parsed_jetton_wallet_jetton_address_address__friendly: "EQALfk9nvSBhxD41SmFO3aM3R51CINSPs-ZUTAO2fz7bIJB8"
    order_by: "parsed_jetton_wallet_balance"
    order_desc: true
    parsed_jetton_wallet_data_is_approved: 1, # Jetton is True in collection
    account_deleted: 0 # Account not deleted
  ) { 
    wallet_address: address
    wallet_workchain: workchain
    wallet_balance: parsed_jetton_wallet_balance
    owner_address: parsed_jetton_wallet_owner_address_address
    owner_workchain: parsed_jetton_wallet_owner_address_workchain
  }
}
```

</details>

<details>

<summary>Get TOP accounts by balance over all network</summary>

```graphql
{
  raw_account_states(
    order_by: "account_storage_balance_grams"
    order_desc: true,
    account_deleted: 0 
  ){
    balance: account_storage_balance_grams
    address
    workchain
    last_tx_at: gen_utime
  }
}
```

</details>

<details>

<summary>Get transaction for account</summary>

```graphql
{
  raw_transactions(address__friendly: "EQALfk9nvSBhxD41SmFO3aM3R51CINSPs-ZUTAO2fz7bIJB8"){
    gen_utime
    lt
    account_storage_balance_grams
    in_msg_op_code
    out_msg_count
    out_msg_body
  }
}
```

</details>

<details>

<summary>Batch load a LOT of transactions</summary>

```graphql
{
  raw_transactions(
    address__friendly: "Ef9VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVbxn"
    order_by: "lt"
    order_desc: true
    lt_gt: "40379620000003" # pass last lt from prev request here
    page_size: 150 # max transactions per 1 request
  ) {
    address
    workchain
    lt
  }
}
```

</details>

<details>

<summary>Get transactions count for smart contract hash or by OP code</summary>

```graphql
{
  by_code_hash: lastTransactionCountSegments(
    account_state_state_init_code_hash: "64A43970F2007A1DA6D6FC81773CC095D1CC270E81359E471F3B03469ABEB7B5"
    segmentation: "day"
    days: 7
  ) {
    segment
    cnt
  }
  
  by_op: lastTransactionCountSegments(
    in_msg_op_code: 1607220500
    segmentation: "hour"
  ) {
    segment
    cnt
  }
}
```

</details>

<details>

<summary>Find jetton wallets count for jetton (count of actual accounts by filters)</summary>

```graphql
{
  groupAccountStates(
    by: ["parsed_jetton_wallet_jetton_address_workchain", "parsed_jetton_wallet_jetton_address_address"]
    filter_by: {
      parsed_jetton_wallet_data_is_approved: 1, # Account wallet data is approved by jetton
      account_deleted: 0, # Account is not deleted
      parsed_jetton_wallet_jetton_address_address__friendly: "EQALfk9nvSBhxD41SmFO3aM3R51CINSPs-ZUTAO2fz7bIJB8"} # Master jetton address
    aggregations: [{operation: "count"}]
  ) {
    count
  }
}
```

</details>

<details>

<summary>Get all NFTs of wallet</summary>

```graphql
{
  raw_account_states(
    parsed_nft_owner_address__friendly: "EQDrLq-X6jKZNHAScgghh0h1iog3StK71zn8dcmrOj8jPWRA"
    order_by: "parsed_nft_index"
    order_desc: true
    parsed_nft_true_nft_in_collection: 1 # Check that collection approve NFT with such address
    account_state_state_init_code_method_name: "get_nft_data"
    account_deleted: 0 
    page_size: 10
    page: 0
  ){
    nft_address: address
    nft_workchain: workchain
    nft_index: parsed_nft_index
    
  	collection_address: parsed_nft_collection_address_address
    collection_workchain: parsed_nft_collection_address_workchain
  }
}
```

</details>

<details>

<summary>Jetton wallet trend balance by day</summary>

```graphql
{
  groupTransactions(
    by: ["gen_utime__toYYYYMMDD"]
    aggregations: [{field: "parsed_jetton_wallet_balance", operation: "max"}, {field: "parsed_jetton_wallet_balance", operation: "argMax"}, {operation: "count"}]
    page_size: 150
    filter_by: {address__friendly: "EQCrZoDpy_7u2olyH_8D0Lr__tTQ5eDpqMMnzLiALGOFYnr3"}
    order_by: "gen_utime__toYYYYMMDD"
  ) {
    gen_utime__toYYYYMMDD
    max_balance_in_day: parsed_jetton_wallet_balance__max
    end_of_the_day_balance: parsed_jetton_wallet_balance__argMax
    count_txs_in_day: count
  }
}
```

</details>

<details>

<summary>TOP Jettons by holders count</summary>

```graphql
{
  groupAccountStates(
    by: ["parsed_jetton_wallet_jetton_address_workchain", "parsed_jetton_wallet_jetton_address_address"]
    aggregations: [{operation: "count"}]
    filter_by: {
      account_deleted: 0, # Not deleted wallets
      parsed_jetton_wallet_data_is_approved: 1 # All wallets that are really in this Jettons
      parsed_jetton_wallet_balance__gt: 0 # All wallets with balance
    }
    order_by: "count"
    order_desc: true
  ) {
    users_count: count
    parsed_jetton_wallet_jetton_address_workchain
    parsed_jetton_wallet_jetton_address_address
  }
}
```

</details>

<details>

<summary>TOP Jettons by locked balances</summary>

```graphql
{
  wall_locks: groupAccountStates(
    by: ["parsed_jetton_wallet_jetton_address_workchain", "parsed_jetton_wallet_jetton_address_address"]
    filter_by: {
      parsed_jetton_owner_code_hash: "12D793F9C449BEF45C7BB43685DE21D4E03C7118B5D38F0BF3C7B9BEB497900D" # All jettons with lock smart contract owner
    }
    aggregations: [
      {field: "parsed_jetton_wallet_balance", operation: "sum"}, # Sum of locked balances 
      {operation: "count"} # Count of lock contracts
    ]
    order_by: "parsed_jetton_wallet_balance__sum"
    order_desc: true
  ) {
    parsed_jetton_wallet_jetton_address_workchain
    parsed_jetton_wallet_jetton_address_address
    count
    parsed_jetton_wallet_balance__sum
  }
}
```

</details>

<details>

<summary>Get all balances of Jetton wallets for user</summary>

```graphql
{
  raw_account_states(
    parsed_jetton_wallet_owner_address_address__friendly: "UQDfmsDtWQP5D_YkXX-XlULvs4HivRaKY38ftT2hS5yAAIma" # owner address
   account_deleted: 0 # account not deleted
    parsed_jetton_wallet_data_is_approved: 1 # wallet is real
    order_by: "parsed_jetton_wallet_balance"
    order_desc: true
  ){
    # Jetton address (concat workcahin:address for RAW form)
   parsed_jetton_wallet_jetton_address_address
    parsed_jetton_wallet_jetton_address_workchain
    
    # Balance of jetton
    parsed_jetton_wallet_balance
  }
}
```

</details>

<details>

<summary>Positive Jetton wallets top-up sum and average</summary>

```graphql
{
  groupTransactions(
    by: ["gen_utime__toYYYYMMDD"]
    aggregations: [
      {field: "parsed_jetton_wallet_balance_diff", operation: "sum"},
      {field: "parsed_jetton_wallet_balance_diff", operation: "avg"}]
    filter_by: {
      or__: [{address_friendly: "EQAFbVItAokA9p0I1SaZd2PEg7FZQIp449mTcAsD_Qrlfa9a"}], 
      gen_utime__gte: "2024-07-01 00:00:00",
      gen_utime__lt: "2024-08-01 00:00:00"
      parsed_jetton_wallet_balance_diff__gt: 0 # only positive balance topup
    }
  ) {
    parsed_jetton_wallet_balance_diff__sum
    parsed_jetton_wallet_balance_diff__avg
  }
}
```

</details>
