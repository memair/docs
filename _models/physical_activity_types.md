---
title: Physical Activity Types
position: 3.1
type: beta
right_code: |
  ~~~ json
  {
    "data": {
      "PhysicalActivityTypes": [
        {
          "slug": "acroyoga"
        },
        ...
        {
          "slug": "zumba"
        }
      ]
    }
  }
  ~~~
  {: title="Response" }
---

The records in this model are prescribed by Memair. Request new physical activity types [here](http://blog.memair.com/contact).

#### Model

Grain: 1 row per physical activity type

| Name | Type | Notes |
|-------|--------|---------|
| name | string |  |
| slug | string | used when creating & querying physical activities |
| about | string | nullable |


~~~ graphql
{
  PhysicalActivityTypes {
    slug
  }
}
~~~
{: title="GraphQL Query" }

~~~ bash
curl \
  -F query='{PhysicalActivityTypes{slug}}' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.app_url }}/graphql
~~~
{: title="Curl" }

~~~ python
data = {
  'query' : '{PhysicalActivityTypes{slug}}',
  'access_token': 'YOUR_ACCESS_TOKEN'
}
import requests
r = requests.post("{{ site.app_url }}graphql", data)
print(r.text)
~~~
{: title="Python" }
