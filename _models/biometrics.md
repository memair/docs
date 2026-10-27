---
title: Biometrics
position: 21.0
right_code: |
  ~~~ json
  {
    "data": {
      "biometrics": {
        "nodes": [
          {
            "id": "34117181",
            "timestamp": "2026-10-27T07:00:00Z",
            "value": 72.0,
            "biometricType": {
              "name": "Heart rate",
              "unitSymbol": "bpm"
            }
          }
        ]
      }
    }
  }
  ~~~
  {: title="Response" }
---

A biometric is one measurement of a defined type, such as weight, blood pressure or heart rate. `value` is a number in the type's unit. `BiometricTypes` lists each type's `unit` and `unitSymbol`, and [biometric_types.yml](https://github.com/memair/data-types/blob/master/biometric_types.yml) defines them.

Types whose slug starts with `daily_`, such as `daily_steps`, are totals for one day, recorded at the start of that day.

Scopes: `biometric_read` and `biometric_write`. Besides the [list arguments](#modelspagination) every record has, `biometrics` can sort by `VALUE`.

~~~ graphql
query {
  biometrics(first: 10, type: heart_rate, fromTimestamp: "last 7 days") {
    nodes {
      id
      timestamp
      value
      biometricType {
        name
        unitSymbol
      }
    }
  }
}
~~~
{: title="List" }

~~~ graphql
mutation {
  createBiometric(input: {
    type: weight
    value: 80.2
    timestamp: "2026-10-27T07:00:00Z"
    clientUuid: "b922d55f-244b-4113-930a-e497bb38fca0"
  }) {
    biometric {
      id
      value
    }
    errors {
      field
      message
    }
  }
}
~~~
{: title="Create" }
