---
title: Biometrics
position: 1.0
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
---

This model is used to store user data for defined [biometric types](/#modelsbiometric_types) like blood pressure, weight, body temperature.

#### Model

Grain: 1 row per biometric type per timestamp. Duplicates will be deleted leaving the latest version.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| biometric_type | [biometric type](/#modelsbiometric_types) | required |
| value | integer | required |
| timestamp | timestamp | assigned by memair if null |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
{
  Biometrics(first: 1, order: timestamp_desc, type: weight) {
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
  -F query='{Biometrics(first: 1 order: timestamp_desc type: weight) {timestamp value biometric_type {name unit}}}' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }
