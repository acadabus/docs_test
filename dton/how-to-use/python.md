# Python

## Python requests

To get started, you will need to install the `requests` packages using pip. You can install them by running the following command in your terminal:

```
pip install requests graphql
```

Once you have installed the packages, you can use the following code to query data from your GraphQL API:

```
endpoint = 'https://dton.io/graphql/'

query = '''
  query {
    # Your GraphQL query
  }
'''

response = requests.post(endpoint, json={'query': query})

if response.status_code == 200:
  data = response.json()['data']
  print(data)
else:
  print(response.json())

```
