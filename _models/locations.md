---
title: Locations
position: 25.0
type: gamma
description: Models user geospatially
right_code: |
  ~~~ json
  {
    "data": {
      "Locations": [
        {
          "lat": 42,
          "lon": 42,
          "timestamp": "2018-05-26T11:52:23Z"
        },
        ...
        {
          "lat": 42,
          "lon": 42,
          "timestamp": "2018-05-26T11:52:21Z"
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

lat
: Latitude

lon
: Longitude

timestamp
: Timestamp of location

altitude
: Altitude (meters)

point_accuracy
: Point Accuracy (meters)

altitude_accuracy
: Altitude Accuracy (meters)

heading
: Heading (degrees from north)

speed
: Speed (meters per second)

source
: Source of location

Grain: 1 row per location type per timestamp. Duplicates will be deleted leaving the latest version.

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
query {
  Locations(
    first: 50
    order: desc
    order_by: timestamp
    within: "42,42,100"
  ) {
    lat
    lon
    timestamp
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  Create(
    locations: [
      {
        lat: 42
        lon: 42
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
  -d '{Locations(first: 50, order: desc, order_by: timestamp) {lat, lon, timestamp}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = "{Locations(first: 50, order: desc, order_by: timestamp) {lat, lon, timestamp}}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
