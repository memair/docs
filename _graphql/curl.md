---
title: Curl Example
position: 3.0
description: Example Curl queries for Memair
right_code: |
  ~~~ json
  {
    "data": {
      "Biometrics": [{
        "timestamp": "2018-09-16T23:20:58Z",
        "value": 100.0,
        "biometric_type": {
          "name": "Body Weight",
          "unit": "Kilogram"
        }
      }]
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

query
: GraphQL query. See [above](#graphqlgraphiql) for more details

access_token
: access token with correct scopes for memories being accessed. See [Request Access Token](#authenticationrequest_access_token) for more details

~~~ bash
curl \
  -H 'access_token: 0000000000000000000000000000000000000000000000000000000000000000' \
  -d '{Biometrics(first: 1 order: desc order_by: timestamp type: weight) {timestamp value biometric_type {name unit}}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }
