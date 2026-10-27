---
title: Python Example
position: 4.0
description: A request with the requests library
right_code: |
  ~~~ json
  {
    "data": {
      "biometrics": {
        "nodes": [
          {
            "timestamp": "2026-10-26T12:30:00Z",
            "value": 80.2,
            "biometricType": {
              "name": "Body weight",
              "unitSymbol": "kg"
            }
          }
        ]
      }
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "errors": [
      {
        "message": "Field 'unit_symbol' doesn't exist on type 'BiometricType' (Did you mean `unitSymbol`?)",
        "locations": [{"line": 9, "column": 9}],
        "path": [
          "query LatestWeight",
          "biometrics",
          "nodes",
          "biometricType",
          "unit_symbol"
        ],
        "extensions": {
          "code": "undefinedField",
          "typeName": "BiometricType",
          "fieldName": "unit_symbol"
        }
      }
    ]
  }
  ~~~
  {: title="Error" }
---

This script reads the latest weight with [Otto's token](#authenticationotto). It uses [requests](https://pypi.org/project/requests/).

~~~ python
import requests

ACCESS_TOKEN = "0000000000000000000000000000000000000000000000000000000000000000"

query = """
query LatestWeight {
  biometrics(first: 1, type: weight) {
    nodes {
      timestamp
      value
      biometricType {
        name
        unitSymbol
      }
    }
  }
}
"""

response = requests.post(
    "https://memair.com/graphql",
    json={"query": query},
    headers={"Authorization": f"Bearer {ACCESS_TOKEN}"},
    timeout=30,
)
response.raise_for_status()
print(response.json())
~~~
{: title="Python" }

`raise_for_status()` raises on token and rate-limit failures, which come back as HTTP errors. GraphQL errors come back with HTTP `200`, so check the response for `errors` too ([Errors](#graphqlerrors)).

The Error tab shows the response when a field name is misspelled, here `unit_symbol` for `unitSymbol`.
