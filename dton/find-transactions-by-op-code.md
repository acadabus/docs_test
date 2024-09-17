# Find transactions by OP code

OP codes defined by first 32 bits in messages sent to smart contracts.

&#x20;

Most used OP codes are:

| OP Code (firs 32 bits of message body) | Description                                    |
| -------------------------------------- | ---------------------------------------------- |
| 0x0                                    | Text comment OP code for ordinary transactions |
| 0x5fcc3d14                             | NFT Transfer request                           |
| 0xf8a7ea5                              | Jetton Transfer request                        |
| 0x7362d09c                             | Jetton Transfer notification                   |

You can filter transactions by `OP` code in 32uint representation:

```graphql
{
  raw_transactions(in_msg_op_code: 1607220500) {
    in_msg_op_code
    out_msg_op_code
    address
    workchain
    parsed_nft_owner_address_address
    parsed_nft_owner_address_workchain
    account_state_state_init_code_has_get_nft_data
  }
}
```

Or by hex representation:

```graphql
{
  raw_transactions(in_msg_op_code_hex: "0x5fcc3d14") {
    in_msg_op_code
    out_msg_op_code
    address
    workchain
    parsed_nft_owner_address_address
    parsed_nft_owner_address_workchain
    account_state_state_init_code_has_get_nft_data
  }
}
```



&#x20;
