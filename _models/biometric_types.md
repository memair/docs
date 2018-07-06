---
title: Biometric Types
position: 1.1
type: gamma
right_code: |
  ~~~ json
  {
    "data": {
      "BiometricTypes": [
        {
          "slug": "diastolic_pressure"
        },
        {
          "slug": "internal_body_temp"
        },
        {
          "slug": "systolic_pressure"
        },
        {
          "slug": "weight"
        }
      ]
    }
  }
  ~~~
  {: title="Response" }
---

The records in this model are prescribed by Memair. Request new biometric types [here](http://blog.memair.com/contact).

#### Model

Grain: 1 row per biometric type

| Name | Type | Notes |
|-------|--------|---------|
| name | string |  |
| slug | string | used when creating & querying biometrics |
| unit | string |  |
| unit_symbol | string |  |
| about | string | nullable |


~~~ graphql
{
  BiometricTypes {
    slug
  }
}
~~~
{: title="GraphQL Query" }

~~~ bash
curl \
  -F query='{BiometricTypes{slug}}' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
data = {
  'query' : '{BiometricTypes{slug}}',
  'access_token': 'YOUR_ACCESS_TOKEN'
}
import requests
r = requests.post("{{ site.app_url }}graphql", data)
print(r.text)
~~~
{: title="Python" }
