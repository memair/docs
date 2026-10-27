---
title: Pagination
position: 1.0
right_code: |
  ~~~ json
  {
    "data": {
      "locations": {
        "totalCount": 4821,
        "pageInfo": {
          "hasNextPage": true,
          "endCursor": "WyJ0aW1lc3RhbXAiLCIyMDI2LTEwLTI2VDE4OjQ0OjAwLjAwMDAwMFoiLDQyODY0NjA2XQ"
        },
        "nodes": [
          {"id": "42864610", "timestamp": "2026-10-26T19:04:00Z"},
          {"id": "42864609", "timestamp": "2026-10-26T18:59:00Z"},
          {"id": "42864608", "timestamp": "2026-10-26T18:54:00Z"},
          {"id": "42864607", "timestamp": "2026-10-26T18:49:00Z"},
          {"id": "42864606", "timestamp": "2026-10-26T18:44:00Z"}
        ]
      }
    }
  }
  ~~~
  {: title="First page response" }
---

Record lists are connections. Each returns a page of `nodes`, a `pageInfo` for fetching the next page, and `totalCount`, the number of records that match the filters across every page. Every kind of record takes the same list arguments:

first
: page size: 25 when not given, at most 1,000. A larger value returns 1,000.

after
: the `pageInfo.endCursor` of the previous page

orderBy
: `TIMESTAMP` (the default) or `UPDATED_AT`. Biometrics can also sort by `VALUE`, emotions by `INTENSITY` and recommendations by `PRIORITY`.

direction
: `DESC` (the default) or `ASC`

fromTimestamp, toTimestamp, fromUpdatedAt, toUpdatedAt
: time bounds, inclusive

source
: only records with exactly this `source`

type
: only records of this type (`form` for medications)

To read every record, request pages until `hasNextPage` is false, and pass each page's `endCursor` as the next `after`. A cursor holds the last record's sort value and id, so records added while you page do not shift the pages. A cursor works only with the `orderBy` that gave it out.

Lists page forwards only. To see records added since, start again from the first page.

To sync changes, list with `orderBy: UPDATED_AT` and `fromUpdatedAt` set to the time of the last sync. Deleted records do not appear in any list.

Lists also have `edges { cursor node }`, for clients that expect the Relay connection shape.

~~~ graphql
query {
  locations(first: 5) {
    totalCount
    pageInfo {
      hasNextPage
      endCursor
    }
    nodes {
      id
      timestamp
    }
  }
}
~~~
{: title="First page" }

~~~ graphql
query {
  locations(first: 5, after: "WyJ0aW1lc3RhbXAiLCIyMDI2LTEwLTI2VDE4OjQ0OjAwLjAwMDAwMFoiLDQyODY0NjA2XQ") {
    pageInfo {
      hasNextPage
      endCursor
    }
    nodes {
      id
      timestamp
    }
  }
}
~~~
{: title="Next page" }
