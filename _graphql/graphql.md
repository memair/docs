---
title: /graphql
position: 1.1
type: post
description: A query language for Memair
right_code: |
  ~~~ json
  {
    "data": {
      "Biometrics": [
        {
          "value": 37.8,
          "timestamp": "2018-01-01T00:00:00Z",
          "type": "Internal Body Temperature"
        },
        {
          "value": 80,
          "timestamp": "2018-01-01T00:00:00Z",
          "type": "Weight"
        }
      ]
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "errors": [
      {
        "message": "Field 'foobar' doesn't exist on type 'Biometric'",
        "locations": [{"line":1,"column":32}]
      }
    ],
    "data": {}
  }
  ~~~
  {: title="Error" }
---

GraphQL provides a complete and understandable description of the data in Memair.

query
: GraphQL query. See [above](#graphqlgraphiql) for more details

access_token
: access token with correct scopes for memories being accessed. See [Request Access Token](#authenticationrequest_access_token) for more details

~~~ bash
curl \
  -F query='{Biometrics {value, timestamp, type}}' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.app_url }}/graphql
~~~
{: title="Curl" }

~~~ python
data = {
  'query' : '{Biometrics {value, timestamp, type}',
  'access_token': 'YOUR_APP_KEY'
}
import requests
r = requests.post("{{ site.app_url }}/graphql", data)
print(r.text)
~~~
{: title="Python" }
