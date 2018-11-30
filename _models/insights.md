---
title: Insights
position: 10.0
type: alpha
right_code: |
  ~~~ json
  {
    "data": {
      "Insights": [
        {
          "timestamp": "2018-05-08T00:00:00Z",
          "chart": [
            {"x": "2018-05-01", "y": 4129, "label": "steps"},
            {"x": "2018-05-02", "y": 7621, "label": "steps"},
            {"x": "2018-05-03", "y": 1723, "label": "steps"},
            {"x": "2018-05-04", "y": 2372, "label": "steps"},
            {"x": "2018-05-05", "y": 3342, "label": "steps"},
            {"x": "2018-05-06", "y": 7983, "label": "steps", "detail": "Weekly Peak"},
            {"x": "2018-05-07", "y": 3130, "label": "steps"}
          ]
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
        "path": ["Insights"]
      }
    ]
  }
  ~~~
  {: title="Error" }
---

This model is used to surface insights to the user. Insights are represented as charts.

#### Model

Grain: each row contains a single insight.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| chart | json | non nullable |
| timestamp | timestamp | assigned by memair if null |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
query {
  Insights(first: 1, order: desc, order_by: timestamp) {
    timestamp
    chart
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  CreateInsight(
    chart: [
      {x: "2018-05-01", y: 4129, label: "steps"},
      {x: "2018-05-02", y: 7621, label: "steps"},
      {x: "2018-05-03", y: 1723, label: "steps"},
      {x: "2018-05-04", y: 2372, label: "steps"},
      {x: "2018-05-05", y: 3342, label: "steps"},
      {x: "2018-05-06", y: 7983, label: "steps", detail: "Weekly Peak"},
      {x: "2018-05-07", y: 3130, label: "steps"}
    ]
  ) {
    timestamp
    chart
  }
}

~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -H "access_token: 0000000000000000000000000000000000000000000000000000000000000000" \
  -d '{Insights(first: 1, order: desc, order_by: timestamp) {timestamp, chart}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = '{Insights(first: 1, order: desc, order_by: timestamp) {timestamp, chart}}'
response = user.query(query)
print(response)
~~~
{: title="Python" }
