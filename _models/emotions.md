---
title: Emotions
position: 23.0
type: gamma
right_code: |
  ~~~ json
  {
    "data": {
      "Emotions": [
        {
          "timestamp": "2018-01-01T00:00:00Z",
          "intensity": 80,
          "emotion_type": {
            "name": "Happy"
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
        "path": ["Emotions"]
      }
    ]
  }
  ~~~
  {: title="Error" }
---

This model is used to store user data for defined emotion types like blood pressure, happy, or body temperature. A full list of emotion types can be accessed using the `EmotionTypes` endpoint or inspecting the [data-types repo](https://github.com/memair/data-types/blob/master/emotion_types.yml). Please create a [pull request](https://github.com/memair/data-types/blob/master/emotion_types.yml) or [contact us](https://blog.memair.com/community/contact) to add emotion types.

#### Model

Grain: 1 row per emotion type per timestamp. Duplicates will be deleted leaving the latest version.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| emotion_type | emotion type | required |
| intensity | integer | required |
| timestamp | timestamp | assigned by memair if null |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
query {
  Emotions(first: 1, order: desc, order_by: timestamp, type: happy) {
    timestamp
    intensity
    emotion_type {
      name
    }
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  CreateEmotion(intensity: 80, type: happy) {
    timestamp
    intensity
    emotion_type {
      name
    }
  }
}

~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -H 'access_token: 0000000000000000000000000000000000000000000000000000000000000000' \
  -d '{Emotions(first: 1 order: desc order_by: timestamp type: happy) {timestamp intensity emotion_type {name}}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = "{Emotions(first: 1 order: desc order_by: timestamp type: happy) {timestamp intensity emotion_type {name}}}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
