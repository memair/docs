---
title: Curl Example
position: 3.0
description: A request from the command line
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
        "locations": [{"line": 1, "column": 85}],
        "path": ["query", "biometrics", "nodes", "biometricType", "unit_symbol"],
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

This request reads the latest weight with [Otto's token](#authenticationotto).

~~~ bash
curl https://memair.com/graphql \
  -H 'Authorization: Bearer 0000000000000000000000000000000000000000000000000000000000000000' \
  -H 'Content-Type: application/json' \
  -d '{"query": "{ biometrics(first: 1, type: weight) { nodes { timestamp value biometricType { name unitSymbol } } } }"}'
~~~
{: title="Curl" }

The Error tab shows the response when a field name is misspelled, here `unit_symbol` for `unitSymbol`.
