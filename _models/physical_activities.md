---
title: Physical Activities
position: 3.0
type: beta
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
---

This model is used to store user data for defined [physical activity types](/#modelsphysical_activity_types) like blood pressure, weight, body temperature.

#### Model

Grain: 1 row per physical activity type per timestamp. Duplicates will be deleted leaving the latest version.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| physical_activity_type | [physical activity type](/#modelsphysical_activity_types) | required |
| duration | integer | in seconds & nullable |
| timestamp | timestamp | assigned by memair if null |
| ended_at | timestamp | assigned by memair based on duration |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
{
  PhysicalActivities(first: 50, order: timestamp_desc, type: all) {
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
  CreatePhysicalActivity(type: acroyoga) {
    timestamp
    physical_activity_type {
      name
    }
  }
}
~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -F query='{PhysicalActivities(first: 50, order: timestamp_desc, type: all) {timestamp, physical_activity_type {name}}}' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.app_url }}/graphql
~~~
{: title="Curl" }
