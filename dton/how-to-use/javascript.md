# Javascript

## Javascript simple

To get started, you will need to install the graphql-request package which allows you to send GraphQL queries and mutations from JavaScript. You can install it using npm by running the following command:

```
npm install graphql-request
```

Once you have installed the package, you can use the following code to query data from your GraphQL API:

```
import { request, gql } from 'graphql-request'

const endpoint = 'https://dton.io/graphql/'

const query = gql`
  query {
    // Your GraphQL query
  }
`

request(endpoint, query).then((data) => {
  console.log(data)
}).catch((error) => {
  console.error(error)
})
```

Replace `// Your GraphQL` query with your actual GraphQL query. For example, if you want to query a list of NFT sale transactions with some useful data:

```
query {
    raw_transactions(parsed_seller_transaction_type: 10) {
      parsed_seller_nft_price
      gen_utime
      hash
      lt
      address
      workchain
      parsed_seller_nft_address_address
      parsed_seller_nft_address_workchain
      parsed_seller_nft_prev_owner_address_address
      parsed_seller_nft_prev_owner_address_workchain
      parsed_seller_nft_new_owner_address_address
      parsed_seller_nft_new_owner_address_workchain
      parsed_owner_is_seller
      parsed_seller_sell_transaction_verified
      in_msg_src_addr_address_hex
      in_msg_src_addr_workchain_id
    }
}
```

