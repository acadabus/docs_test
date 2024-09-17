---
description: Those filters work in account_states and transactions tables
---

# Find needed account

## By address

### User-friendly

#### Account states & other tables

Example of query account actual balance:

```graphql
{
  raw_account_states(
    address__friendly: "EQAAFSPzZXu3pKo-VfQZRYcUjygur1-VLI9-wY9uwaobbUht"
  ) {
    account_storage_balance_grams
  }
}
```

#### Transactions

Example of query account balance changing by transactions:

```graphql
{
  raw_transactions(
    address__friendly: "EQAAFSPzZXu3pKo-VfQZRYcUjygur1-VLI9-wY9uwaobbUht"
  ) {
    account_storage_balance_grams
    gen_utime
  }
}
```

### Raw form only

Example of query account actual balance:

```graphql
{
  raw_account_states(
    address: "001523F3657BB7A4AA3E55F4194587148F282EAF5F952C8F7EC18F6EC1AA1B6D"
    workchain: 0
  ) {
    account_storage_balance_grams
  }
}
```

## By code or data hash

We not suggest finding accounts by code hash, better use filter by get methods

<table><thead><tr><th width="174">Contract</th><th width="427.3333333333333">Code hash</th><th data-type="content-ref">Verifier</th></tr></thead><tbody><tr><td>Wallet V1R1</td><td><code>A0CFC2C48AEE16A271F2CFC0B7382D81756CECB1017D077FAAAB3BB602F6868C</code></td><td><a href="https://verifier.ton.org/EQAAQ-CfIZkUjmZ6ES9D_keK2yHz10U1ba49K0S86Whva74Z">https://verifier.ton.org/EQAAQ-CfIZkUjmZ6ES9D_keK2yHz10U1ba49K0S86Whva74Z</a></td></tr><tr><td>Wallet V1R2</td><td><code>D4902FCC9FAD74698FA8E353220A68DA0DCF72E32BCB2EB9EE04217C17D3062C</code></td><td><a href="https://verifier.ton.org/EQAAVd4c_2pMb4Bp8BxumyV8jutdwJ9R-q0dBqQj7tj_W8SX">https://verifier.ton.org/EQAAVd4c_2pMb4Bp8BxumyV8jutdwJ9R-q0dBqQj7tj_W8SX</a></td></tr><tr><td>Wallet V1R3</td><td><code>587CC789EFF1C84F46EC3797E45FC809A14FF5AE24F1E0C7A6A99CC9DC9061FF</code></td><td><a href="https://verifier.ton.org/EQAAEgdraul87g9zvm5Lxtd9FNoebifojeyT90uG6zrWBvRh">https://verifier.ton.org/EQAAEgdraul87g9zvm5Lxtd9FNoebifojeyT90uG6zrWBvRh</a></td></tr><tr><td>Wallet V2R1</td><td><code>5C9A5E68C108E18721A07C42F9956BFB39AD77EC6D624B60C576EC88EEE65329</code></td><td><a href="https://verifier.ton.org/EQAAC2tOLQxG4KuFcS_pb2Rta1MDdgx8wAtZnGf5bIEIMLft">https://verifier.ton.org/EQAAC2tOLQxG4KuFcS_pb2Rta1MDdgx8wAtZnGf5bIEIMLft</a></td></tr><tr><td>Wallet V2R2</td><td><code>FE9530D3243853083EF2EF0B4C2908C0ABF6FA1C31EA243AACAA5BF8C7D753F1</code></td><td><a href="https://verifier.ton.org/EQAAnU-irJsuuljRAWBRUhdvFB-rvGRHbdQSWXPSQYND6MVb">https://verifier.ton.org/EQAAnU-irJsuuljRAWBRUhdvFB-rvGRHbdQSWXPSQYND6MVb</a></td></tr><tr><td>Wallet V3R1</td><td><code>B61041A58A7980B946E8FB9E198E3C904D24799FFA36574EA4251C41A566F581</code></td><td><a href="https://verifier.ton.org/EQAY_2_A88HD43S96hbVGbCLB21e6_k1nbaqICwS3ZCrMBaZ">https://verifier.ton.org/EQAY_2_A88HD43S96hbVGbCLB21e6_k1nbaqICwS3ZCrMBaZ</a></td></tr><tr><td>Wallet V3R2</td><td><code>84DAFA449F98A6987789BA232358072BC0F76DC4524002A5D0918B9A75D2D599</code></td><td><a href="https://verifier.ton.org/EQALgHQ-KpmkwftbsdeZdA4DvVDCYkKvria9llb7_RMeZj_8">https://verifier.ton.org/EQALgHQ-KpmkwftbsdeZdA4DvVDCYkKvria9llb7_RMeZj_8</a></td></tr><tr><td>Wallet V4R1</td><td><code>64DD54805522C5BE8A9DB59CEA0105CCF0D08786CA79BEB8CB79E880A8D7322D</code></td><td></td></tr><tr><td>Wallet V4R2</td><td><code>FEB5FF6820E2FF0D9483E7E0D62C817D846789FB4AE580C878866D959DABD5C0</code></td><td><a href="https://verifier.ton.org/EQDerEPTIh0O8lBdjWc6aLaJs5HYqlfBN2Ruj1lJQH_6vcaZ">https://verifier.ton.org/EQDerEPTIh0O8lBdjWc6aLaJs5HYqlfBN2Ruj1lJQH_6vcaZ</a></td></tr></tbody></table>

```graphql
{
  account_states(
    account_state_state_init_code_hash: "B61041A58A7980B946E8FB9E198E3C904D24799FFA36574EA4251C41A566F581"
  ) {
    address
    workchain
  }
}
```

## By get methods

`method_name` in Func is compiling to crc16 integer, you can filter transactions or accounts states by get any get method:

### Any get method

You can get account contain specific get method name crc16, for example all accounts with `seqno` method (85143):

```graphql
{
  raw_account_states(account_state_state_init_code_method_name: "get_wallet"){
    address
    workchain
  }
}
```

### Predefined get methods

Some of the methods predefined and contain special columns to query them. Example of query all NFTs in low-level manner:

```graphql
{
  raw_account_states(account_state_state_init_code_has_get_nft_data: 1) {
    address
    workchain
  }
}
```

<table><thead><tr><th width="432.3333333333333">Get method name</th><th>crc16</th></tr></thead><tbody><tr><td><code>dnsresolve</code></td><td>123660</td></tr><tr><td><code>get_jetton_data</code></td><td>106029</td></tr><tr><td><code>get_wallet_address</code></td><td>103289</td></tr><tr><td><code>get_collection_data</code>  </td><td>102491</td></tr><tr><td><code>get_nft_address_by_index</code></td><td>92067</td></tr><tr><td><code>get_nft_data</code></td><td>102351</td></tr><tr><td><code>royalty_params</code></td><td>85719</td></tr><tr><td><code>hello_world</code></td><td>113531 </td></tr><tr><td><code>get_owner</code></td><td>80293</td></tr><tr><td><code>seqno</code></td><td>85143 </td></tr><tr><td><code>get_public_key</code></td><td>78748</td></tr><tr><td><code>get_version</code></td><td>82320 </td></tr><tr><td><code>get_marketplace_address</code></td><td>91689</td></tr><tr><td><code>get_sale_data</code></td><td>72748</td></tr><tr><td><code>get_plugin_list</code></td><td>107653</td></tr><tr><td><code>is_plugin_installed</code></td><td>76407 </td></tr><tr><td><code>get_subwallet_id</code></td><td>81467 </td></tr><tr><td><code>get_editor</code></td><td>90228</td></tr><tr><td><code>get_is_closed</code></td><td>110449</td></tr><tr><td><code>get_reveal_mode</code></td><td>116695</td></tr><tr><td><code>get_reveal_data</code></td><td>93270 </td></tr><tr><td><code>get_wallet_data</code></td><td>97026 </td></tr><tr><td><code>get_telemint_token_name</code></td><td>69506</td></tr><tr><td><code>get_telemint_auction_state</code></td><td>122498</td></tr></tbody></table>

