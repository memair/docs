---
title: Recommendations
position: 11.0
type: beta
right_code: |
  ~~~ json
  {
    "data": {
      "Recommendations": [
        {
          "type": "Watch video",
          "url": "https://youtu.be/LQCoHLQkFxw",
          "timestamp": "2018-11-19T15:49:03Z",
          "expires_at": "2018-11-20T05:00:00Z",
          "is_expired": false,
          "actioned_at": null,
          "is_actioned": false
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
        "path": ["Recommendations"]
      }
    ]
  }
  ~~~
  {: title="Error" }
---

This model is used to give the user recommendations. Insights are represented as charts. A full list of recommendation types can be accessed using the `RecommendationTypes` endpoint or inspecting the [data-types repo](https://github.com/memair/data-types/blob/master/recommendation_types.yml). Please create a [pull request](https://github.com/memair/data-types/blob/master/recommendation_types.yml) or [contact us](https://blog.memair.com/community/contact) to add recommendation types.

#### Model

Grain: each row contains a single recommendation.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| recommendation_type | recommendation type | required |
| title | string | nullable |
| description | string | nullable |
| url | string | nullable |
| priority | float | required (0-100) |
| timestamp | timestamp | assigned by memair if null |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
query {
  Recommendations(
    first: 1
    expired: false
    actioned: false
    type: video
    order: desc
    order_by: priority
  )
  {
    type
    url
    timestamp
    expires_at
    is_expired
    actioned_at
    is_actioned
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  CreateRecommendation(
    priority: 90
    expires_at: tomorrow
    type: video
    url: "https://youtu.be/LQCoHLQkFxw"
  ) {
    type
    url
    timestamp
    expires_at
    is_expired
    actioned_at
    is_actioned
  }
}

~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -F query='{Recommendations(first: 1 expired: false actioned: false type: video order: desc order_by: priority){type url timestamp expires_at is_expired actioned_at is_actioned}' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('YOUR_ACCESS_TOKEN')
query = "{Recommendations(first: 1 expired: false actioned: false type: video order: desc order_by: priority){type url timestamp expires_at is_expired actioned_at is_actioned}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
