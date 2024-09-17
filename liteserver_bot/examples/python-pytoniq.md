# Python: pytoniq

<pre><code><strong>import requests
</strong>from pytoniq import LiteBalancer
<strong>
</strong><strong>config = requests.get('LINK_FROM_BOT').json()
</strong>provider = LiteBalancer.from_config(config=config, trust_level=2)

await client.start_up()
result = await client.run_get_method(address='EQBvW8Z5huBkMJYdnfAEM5JqTNkuWX3diqYENkWsIL0XggGG', method='seqno', stack=[])

</code></pre>
