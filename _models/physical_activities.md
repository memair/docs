---
title: Physical Activities
position: 26.0
type: gamma
description: Models defined physical activities
right_code: |
  ~~~ json
  {
    "data": {
      "PhysicalActivities": [
        {
          "timestamp": "2018-05-19T03:55:10Z",
          "physical_activity_type": {
            "name": "Skating"
          }
        }
        ...
        {
          "timestamp": "2018-05-123T03:24:55Z",
          "physical_activity_type": {
            "name": "Polo"
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
        "path": ["PhysicalActivities"]
      }
    ]
  }
  ~~~
  {: title="Error" }
---

This model is used to store user data for defined physical activity types like blood pressure, weight, body temperature. A full list of physical activity types can be accessed using the `PhysicalActivityTypes` endpoint or inspecting the [data-types repo](https://github.com/memair/data-types/blob/master/physical_activity_types.yml). Please create a [pull request](https://github.com/memair/data-types/blob/master/physical_activity_types.yml) or [contact us](https://blog.memair.com/community/contact) to add physical activity types.

#### Model

Grain: 1 row per physical activity type per timestamp. Duplicates will be deleted leaving the latest version.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| physical_activity_type | physical activity type | required |
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
  PhysicalActivities(
    first: 50
    order: desc
    order_by: timestamp
    type: all
  ) {
    timestamp
    physical_activity_type {
      name
    }
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  Create(
    physical_activities: [
      {
        type: acroyoga
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
  -H 'access_token: 0000000000000000000000000000000000000000000000000000000000000000' \
  -d '{PhysicalActivities(first: 50, order: desc, order_by: timestamp, type: all) {timestamp, physical_activity_type {name}}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = "{PhysicalActivities(first: 50, order: desc, order_by: timestamp, type: all) {timestamp, physical_activity_type {name}}}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
