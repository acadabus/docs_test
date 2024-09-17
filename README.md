# About dton.io

Welcome to the documentation for [dton](https://dton.io), our blockchain scanner that provides all the features you need, such as a [GraphQL API](https://dton.io/graphql/) for TON nodes and websocket subscriptions for new data.

To create dton, we started with a custom C++ block parser that parses all TLB data into JSON and sends it to our Kafka brokers. Then, we developed a Python parser that takes the JSON data and stores it in Clickhouse. Finally, we built a GraphQL and websocket API on top of Clickhouse.

We're very proud of our system because it's scalable, fast, and reliable for working with block data. In this documentation, we'll describe how you can use dton in your own projects. Please keep in mind that the dton.io frontend is simply a React app on top of the GraphQL API, so all of this information can be used in your own projects. Thanks for choosing dton!

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td>Mainnet</td><td></td><td><a href="https://dton.io/">https://dton.io/</a></td></tr><tr><td></td><td>Testnet</td><td></td><td><a href="https://testnet.dton.io">https://testnet.dton.io</a></td></tr><tr><td></td><td>Support group</td><td></td><td><a href="https://t.me/dtontech">https://t.me/dtontech</a></td></tr></tbody></table>
