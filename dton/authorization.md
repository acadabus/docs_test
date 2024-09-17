# Authorization

For most of the queries and mutations, you must be authorized.&#x20;

Currently, there are a few ways to do so.

## GraphQL API

A key can be provided either in URL or in headers. You can create, edit and/or delete your keys at any moment in [@dtontech\_bot](https://t.me/dtontech\_bot) or over GraphQL API

***

### URL

You can provide your key directly in the URL. This key will be used to authorize you and check your rate limit.

{% hint style="info" %}
_Example_**: https://dton.io/{your\_key}/graphql**&#x20;
{% endhint %}

***

### Header

Alternatively, you can provide your key in HTTP header **Authorization**

{% hint style="info" %}
_Example_**: "Authorization" : "Bearer {your\_key}"**
{% endhint %}

{% hint style="info" %}
While using sessions you are not required to provide a GrpahQL key but note that a random key of yours will be used
{% endhint %}

***

### Unauthorized

If none of the above is done, you will be treated as an unauthorized user with limited access to some functionalities and low amount of requests per second.
