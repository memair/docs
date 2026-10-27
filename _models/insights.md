---
title: Insights
position: 30.0
right_code: |
  ~~~ json
  {
    "data": {
      "Insights": [
        {
          "id": "9112",
          "timestamp": "2026-10-27T06:00:00Z",
          "chart": {
            "title": "Daily steps",
            "type": "line",
            "category_axis": ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
            "series": [
              {
                "label": "Steps",
                "data": [4129.0, 7621.0, 1723.0, 2372.0, 3342.0, 7983.0, 3130.0]
              }
            ]
          }
        }
      ]
    }
  }
  ~~~
  {: title="Response" }
---

An insight is a chart that an app made from the user's data. Memair shows insights on the user's Insights page.

Insights are older than the eight record kinds and work differently. `Insights` returns a plain list: `first` (10 by default) sets its length, and `after` takes the `id` of the last insight on the previous page. `CreateInsight` adds one, and there is no update or delete. Scopes: `insight_read` and `insight_write`.

The chart is a line chart. `categoryAxis` labels the x axis, and each `series` has a `label` and one `data` value per category. `title`, `min` and `max` are optional. The stored chart is returned with snake_case keys, as `category_axis`.

~~~ graphql
query {
  Insights(first: 1) {
    id
    timestamp
    chart
  }
}
~~~
{: title="List" }

~~~ graphql
mutation {
  CreateInsight(
    source: "Example app"
    chart: {
      title: "Daily steps"
      type: line
      categoryAxis: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
      series: [{label: "Steps", data: [4129, 7621, 1723, 2372, 3342, 7983, 3130]}]
    }
  ) {
    id
    timestamp
  }
}
~~~
{: title="Create" }
