# Example - Payment service

### Concept

In our application [@dtontech\_bot](https://t.me/dtontech\_bot) we have implemented a payment service based on webhooks. You can use a similar approach when developing your own product

### How does it work?

* The user makes a deposit to a hot wallet. For example, created via [gobicycle](https://github.com/gobicycle/bicycle)
* Webhook tracks transactions on users' hot wallets
* Microservice receives post requests from the webhook, makes a record in the database and changes the balance

### Example of a webhook for TON replenishment&#x20;

```graphql
mutation {
  profile_webhook_setup(
    webhook_id: 1
    endpoint: "https://your-service.url/endpoint"
    filters: {
      address__friendly_in: [
        "FIRST WALLET ADDRESS",
        "SECOND WALLET ADDRESS"
      ]
    }
    fields: [
      "workchain",
      "address",
      "in_msg_value_grams",
      "out_msg_value_grams"
    ]
  ) {
    success
    error_message
    webhook {
      webhook_id
      endpoint
      filters
      fields
    }
  }
}
```

### Example of a webhook for JETTON replenishment&#x20;

```graphql
mutation {
  profile_webhook_setup(
    webhook_id: 2
    endpoint: "https://your-service.url/endpoint"
    filters: {
      address__friendly_in: [
        "FIRST JETTON WALLET ADDRESS",
        "SECOND JETTON WALLET ADDRESS"
      ]
    }
    fields: [
      "workchain",
      "address",
      "parsed_jetton_wallet_balance",
      "parsed_jetton_wallet_data_is_approved"
    ]
  ) {
    success
    error_message
    webhook {
      webhook_id
      endpoint
      filters
      fields
    }
  }
}
```
