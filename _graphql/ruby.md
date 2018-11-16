---
title: Ruby Example
position: 5.0
description: Example Ruby queries for Memair
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

Memiar offers a [Ruby gem](https://rubygems.org/gems/memair) to simplify GraphQL queries and mutations.

~~~ ruby
require 'memair'

user = Memair.new('YOUR_ACCESS_TOKEN')
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
puts response
~~~
{: title="Ruby" }
