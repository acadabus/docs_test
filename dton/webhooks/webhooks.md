---
description: Creating a webhook to subscribe to updates on the blockchain.
---

# Webhooks

### How does it work?

The `profile_webhook_setup` mutation allows you to subscribe to events on the blockchain by creating webhooks.\
All transactions in the blockchain are divided into shards, which are processed by our indexer. By creating a webhook, the indexer will apply your filters each time and send a request to the URL you specify with the data received from the shard

### Mutation

Method allows you to create new webhooks and edit existing ones. To edit, you need to send a request with the same webhook\_id and modified parameters. If you don't want to change the filters completely, but only extend them, use `extend_filters`

#### Example

```graphql
mutation {
  profile_webhook_setup(
    webhook_id: 1
    endpoint: "https://your-service.url/endpoint"
    filters: {
      address__friendly_in: [
        "EQB3ncyBUTjZUA5EnFKR5_EnOMI9V1tTEAAPaiU71gc4TiUt",
        "EQA-X_yo3fzzbDbJ_0bzFWKqtRuZFIRa1sJsveZJ1YpViO3r"
      ]
    }
    fields: ["address", "workchain", "in_msg_value_grams"]
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

#### Explanation of Parameters

* **`webhook_id`**: Integer - Webhook sequence number
* **`endpoint`**: String - URL of your service
* **`filters`**: Object - Data filtering parameters. Regular filters are supported, as well as filters via \_\_ (see [Filters](../filters.md) page)
* **`fields`**: List of Strings - List of fields expected in the response
* **`extend_filters`**: Object - Optional parameter to extend the filters of an existing webhook.\
  For the `__in` filter, the addition of lists is done. That is, if `fields__in: [3, 4]`, and the database already has a `field__in: [1, 2]`, the resulting filter value will be `field__in: [1, 2, 3, 4]`. \
  Note if a value is passed, the value of the `filters` is ignored.&#x20;

#### Response format

* **`success`**: Boolean - Webhook sequence number
* **`error_message`**: String - URL of your service
* **`webhook`**: Object - Сreated webhook

### Webhook

You will receive regular updates at the url you specified . The webhook will contain transactions filtered by the fields and filters

#### Example

```json
{
  "data": {
    "transactions": [
      {
        "address": "779DCC815138D9500E449C5291E7F12738C23D575B5310000F6A253BD607384E",
        "workchain": 0,
        "in_msg_value_grams": null
      },
      {
        "address": "3E5FFCA8DDFCF36C36C9FF46F31562AAB51B9914845AD6C26CBDE649D58A5588",
        "workchain": 0,
        "in_msg_value_grams": 1081397228
      }
    ]
  }
}
```

### Limits

Limitations on the number of webhooks, filter list length, field list length and number of unique accounts per request depend on the subscription rate.  You can find the latest information in our Telegram Bot [@dtontech\_bot](https://t.me/dtontech\_bot)
