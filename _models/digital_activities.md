---
title: Digital Activities
position: 22.0
type: gamma
description: Models defined digital activities
right_code: |
  ~~~ json
  {
    "data": {
      "DigitalActivities": [
        {
          "timestamp": "2018-05-19T03:55:10Z",
          "digital_activity_type": {
            "name": "Opened app"
          }
        }
        ...
        {
          "timestamp": "2018-05-123T03:24:55Z",
          "digital_activity_type": {
            "name": "Took photo"
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
        "path": ["DigitalActivities"]
      }
    ]
  }
  ~~~
  {: title="Error" }
---

This model is used to store user data for defined digital activity types like blood pressure, weight, body temperature. A full list of digital activity types can be accessed using the `DigitalActivityTypes` endpoint or inspecting the [data-types repo](https://github.com/memair/data-types/blob/master/digital_activity_types.yml). Please create a [pull request](https://github.com/memair/data-types/blob/master/digital_activity_types.yml) or [contact us](https://blog.memair.com/community/contact) to add digital activity types.

#### Model

Grain: 1 row per digital activity type per timestamp. Duplicates will be deleted leaving the latest version.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| digital_activity_type | digital activity type | required |
| duration | integer | in seconds & nullable |
| timestamp | timestamp | assigned by memair if null |
| ended_at | timestamp | assigned by memair based on duration |
| meta | json | nullable |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
query {
  DigitalActivities(
    first: 50
    order: desc
    order_by: timestamp
    type: all
  ) {
    timestamp
    digital_activity_type {
      name
    }
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  Create(
    digital_activities: [
      {
        type: opened_app
        meta: {
          app_name: "cat calendar"
        }
      }
    ]
  )
  {
    id
    records_total
  }
}
~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -H 'access-token: 0000000000000000000000000000000000000000000000000000000000000000' \
  -d '{DigitalActivities(first: 50, order: desc, order_by: timestamp, type: all) {timestamp, digital_activity_type {name}}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = "{DigitalActivities(first: 50, order: desc, order_by: timestamp, type: all) {timestamp, digital_activity_type {name}}}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
