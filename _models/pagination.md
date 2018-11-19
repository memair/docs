---
title: Pagination
position: 1.0
right_code: |
  ~~~ json
  {
    "data": {
      "Locations": [
        {
          "id": "42864610",
          "timestamp": "2018-11-19T10:44:00Z"
        },
        {
          "id": "42864609",
          "timestamp": "2018-11-19T10:36:38Z"
        },
        {
          "id": "42864608",
          "timestamp": "2018-11-19T10:33:38Z"
        },
        {
          "id": "42864607",
          "timestamp": "2018-11-19T10:28:38Z"
        },
        {
          "id": "42864606",
          "timestamp": "2018-11-19T10:23:38Z"
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
        "path": ["Locations"]
      }
    ]
  }
  ~~~
  {: title="Error" }
---

Memair uses cursor based pagination where `after` is the last id of the previous page.


~~~ graphql
query {
  Locations(
    first: 5
    after: 42864606
    order: desc
    order_by: timestamp
  )
  {
    id
    timestamp
  }
}

~~~
{: title="GraphQL Query" }
