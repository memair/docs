---
title: Python Example
position: 4.0
description: Example Python queries for Memair
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

Memiar offers a [Python3 package](https://pypi.org/project/memair/) to simplify GraphQL queries and mutations.

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = """
{
  Biometrics(
    first: 1
    order: desc
    order_by: timestamp
    type: weight
  )
  {
    timestamp
    value
    biometric_type {
      name
      unit
    }
  }
}"""
response = user.query(query)
print(response)
~~~
{: title="Python" }
