# Python TonTools (deprecated)

To get started, you will need to install the `tontools` package using pip. You can install it by running the following command in your terminal:

```
pip install tontools
```

Once you have installed the package, you can use `DtonClient` class [supported](https://github.com/yungwine/TonTools/blob/master/TonTools/Providers/DtonClient.py) methods to send requests to the api:

```
from TonTools import DtonClient
import asyncio


dton = DtonClient()
async def main():
    trs = await dton.get_transactions('EQBvW8Z5huBkMJYdnfAEM5JqTNkuWX3diqYENkWsIL0XggGG', limit=5)
    print(trs)

if __name__ == '__main__':
    asyncio.run(main())
```

Or create instances of [supported](https://github.com/yungwine/TonTools/blob/master/README.md#contracts) contracts classes and specify `DtonClient` as provider:

```
from TonTools import DtonClient, Wallet
import asyncio


dton = DtonClient()
async def main():
    wallet = Wallet(address='EQBvW8Z5huBkMJYdnfAEM5JqTNkuWX3diqYENkWsIL0XggGG', provider=dton)
    trs = await wallet.get_transactions(limit=5)
    print(trs)

if __name__ == '__main__':
    asyncio.run(main())
```

#### Low-level methods

Currently, there are 5 methods for low-level tables: `raw_get_transactions`, `raw_get_account_states`, `raw_get_last_transaction_count_segments`, `raw_get_blocks`, `raw_run_method`.

All they work with automatic pagination, so you can specify `limit` kwarg or don't specify if you want to get all values.

**Some usage examples:**

* find messages senders by op code:

```
op_code = int('0x7362d09c', 16)
await dton.raw_get_transactions(
    fields=['in_msg_src_addr_address_hex', 'in_msg_src_addr_workchain_id'],
    in_msg_op_code=op_code, address_friendly='EQBvW8Z5huBkMJYdnfAEM5JqTNkuWX3diqYENkWsIL0XggGG')
```

or if you can get transactions regardless of account address:

```
op_code = int('0x7362d09c', 16)
await dton.raw_get_transactions(
    fields=['in_msg_src_addr_address_hex', 'in_msg_src_addr_workchain_id'],
    in_msg_op_code=op_code, limit=1000)
```

* find account by its code hash:

```
hash = 'BEB0683EBEB8927FE9FC8EC0A18BC7DD17899689825A121EAB46C5A3A860D0CE'  # standard jetton wallet code hash
accounts = await dton.raw_get_account_states(['workchain', 'address', 'parsed_jetton_wallet_balance'], account_state_state_init_code_hash=hash, limit=500)
print(accounts)
```

* find accounts by get methods ids or names:

```
get_nft_data_code = 102351

accounts = await dton.raw_get_account_states(['workchain', 'address', ], account_state_state_init_code_method=get_nft_data_code, limit=500)

accounts = await dton.raw_get_account_states(['workchain', 'address'], account_state_state_init_code_has_get_telemint_token_name=1, limit=500)
```

* find transactions by text comment:

```
transactions = await dton.raw_get_transactions(['address', 'account_storage_balance_grams'], in_msg_comment="hello", limit=500)
```

* get last transactions amount with nft:

```
trs = await dton.raw_get_last_transaction_count_segments(['cnt', 'segment'], parsed_nft_true_nft_in_collection=1)
```

or with jettons minters:

```
trs = await dton.raw_get_last_transaction_count_segments(['cnt', 'segment'], parsed_jetton_mintable=1)
```

#### searchNFTCollections

find 500 collections metadata url:

```
res = await dton.search_nft_collections([{'data': [{'collection_media': ['url']}]}], limit=500)
```

#### searchNFTs

get NFT sale params

```
res = await dton.search_nfts([{'data': ["nft_index", "sale_type", {"seller": ["nft_price"]}]}], nft_address={'addresses': [{'address_friendly': "EQDfcf2McE2NNz4j_S_cNG757kfj3Jio8BwTF8c-x1y4d4XM"}]})
```
