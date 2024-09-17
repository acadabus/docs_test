# FAQ

<details>

<summary>What will I get after the purchase?</summary>

After purchase, you get 2 servers in the form of:

IP address, Port, IP address int format, base64 public key (do not share), hex public key (do not share)

And also a link to global.config.json which is the same as [mainnet global config](https://ton.org/global.config.json), but uses only your private liteservers.



You can download the config and save it so you don't have to make requests every time. The config available at the link will NOT change.\


But don't forget to renew your servers.

</details>

<details>

<summary>How users are separated?</summary>

We generate a separate private key for each user, which is only available to you.

On our side, we use a C++ load balancer on 9 lite servers, between which we distribute the load.

If you need a dedicated solution: [contact us](https://t.me/tvorogme)

</details>

<details>

<summary>How do you guarantee stability?</summary>

On our side, we use a C++ load balancer on 9 lite servers, between which we distribute the load.

In addition, we provide 2 balancer servers so we can update them. We recommend using both servers and in case 1 is not responding - send requests to the second one. Downtime is possible only in case of server updates, and it is minimal.

Also, you can see the status and subscribe for updates on our status server: [https://tech.dton.io/status/](https://tech.dton.io/status/)

As well as on the site developed NOT by us: [https://tonstat.us/](https://tonstat.us/)

</details>

<details>

<summary>How messages are delivered to the network?</summary>

We distribute all messages from all tariffs to ALL our nodes around the world, as well as to third-party services and directly to network validators.

In case of high load, messages from more expensive tariffs are prioritised.

</details>

<details>

<summary>How to get blocks/data faster?</summary>

We recommend using [waitMasterchainSeqno](https://github.com/ton-blockchain/ton/blob/master/tl/generate/scheme/lite\_api.tl#L106) which allows you to execute an arbitrary function when publishing a block. For example, you can get the state of the desired account, or get the block as soon as at least one of our servers around the world gets a new block online.

</details>

<details>

<summary>What affects rate limit?</summary>

Each function in the [function liteserver list ](https://github.com/ton-blockchain/ton/blob/master/tl/generate/scheme/lite\_api.tl#L71)adds 1 request. The counter is reset every second.

</details>

<details>

<summary>Will it work more stable / deliver messages faster if I buy one more rate?</summary>

No, but at high load times we prioritize more expensive rates with additional messaging

</details>

<details>

<summary>My connection is not working, what do I do?</summary>

Check[ https://tech.dton.io/status/](https://tech.dton.io/status/)

If the liteservers works, most likely the error is on your side. Check open ports, try to change network provider or run the code on another server or locally.

If this doesn't help - write us in the [support chat](https://t.me/dtontech)

</details>
