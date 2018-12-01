---
title: Biometrics
position: 21.0
type: gamma
right_code: |
  ~~~ json
  {
    "data": {
      "Biometrics": [
        {
          "timestamp": "2018-01-01T00:00:00Z",
          "value": 80,
          "biometric_type": {
            "name": "Body Weight",
            "unit": "Kilogram"
          }
        }
      ]
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "data": None,
    "errors": [
      {
        "message": "Please limit requests to 10000 records",
        "locations": [{"line": 3, "column": 3}],
        "path": ["Biometrics"]
      }
    ]
  }
  ~~~
  {: title="Error" }
---

This model is used to store user data for defined biometric types like blood pressure, weight, or body temperature. A full list of biometric types can be accessed using the `BiometricTypes` endpoint or inspecting the [data-types repo](https://github.com/memair/data-types/blob/master/biometric_types.yml). Please create a [pull request](https://github.com/memair/data-types/blob/master/biometric_types.yml) or [contact us](https://blog.memair.com/community/contact) to add biometric types.

#### Model

Grain: 1 row per biometric type per timestamp. Duplicates will be deleted leaving the latest version.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| biometric_type | biometric type | required |
| value | integer | required |
| timestamp | timestamp | assigned by memair if null |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
query {
  Biometrics(first: 1, order: desc, order_by: timestamp, type: weight) {
    timestamp
    value
    biometric_type {
      name
      unit
    }
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  CreateBiometric(value: 80, type: weight) {
    timestamp
    value
    biometric_type {
      name
      unit
    }
  }
}

~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -H 'access_token: 0000000000000000000000000000000000000000000000000000000000000000' \
  -d '{Biometrics(first: 1 order: desc order_by: timestamp type: weight) {timestamp value biometric_type {name unit}}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = "{Biometrics(first: 1 order: desc order_by: timestamp type: weight) {timestamp value biometric_type {name unit}}}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
