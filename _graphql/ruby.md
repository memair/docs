---
title: Ruby Example
position: 5.0
description: A request with Ruby's standard library
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
        "locations": [{"line": 8, "column": 9}],
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

This script reads the latest weight with [Otto's token](#authenticationotto). It needs only Ruby's standard library.

~~~ ruby
require "json"
require "net/http"

access_token = "0000000000000000000000000000000000000000000000000000000000000000"

query = <<~GRAPHQL
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
GRAPHQL

response = Net::HTTP.post(
  URI("https://memair.com/graphql"),
  { query: query }.to_json,
  "Authorization" => "Bearer #{access_token}",
  "Content-Type" => "application/json"
)
response.value
puts JSON.parse(response.body)
~~~
{: title="Ruby" }

`response.value` raises on token and rate-limit failures, which come back as HTTP errors. GraphQL errors come back with HTTP `200`, so check the result for `errors` too ([Errors](#graphqlerrors)).

The Error tab shows the response when a field name is misspelled, here `unit_symbol` for `unitSymbol`.
