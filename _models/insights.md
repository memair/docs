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
          "timestamp": "2018-12-14T20:55:14Z",
          "chart": {
            "type": "line",
            "title": "Time spent",
            "series": [
              {
                "data": [
                  1340,
                  1440,
                  1200,
                  1440,
                  1400,
                  1380,
                  1440
                ],
                "label": "Steps"
              }
            ],
            "category_axis": [
              "Saturday",
              "Sunday",
              "Monday",
              "Tuesday",
              "Wednesday",
              "Thursday",
              "Friday"
            ]
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
  Insights(
    first: 1
    order: desc
    order_by: timestamp
  ) {
    timestamp
    chart
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  CreateInsight(
    source: "Daily insights"
    chart: {
      title: "Daily Steps"
      type: line
      category_axis: ["Saturday", "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
      series: [
        {
          label: "Steps"
          data: [4129, 7621, 1723, 2372, 3342, 7983, 3130]
        }
      ]
    }
  )
  {
    timestamp
    chart
  }
}
~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -H 'access-token: 0000000000000000000000000000000000000000000000000000000000000000' \
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
