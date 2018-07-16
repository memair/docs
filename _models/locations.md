---
title: Locations
position: 2.0
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
{
  Locations(first: 50, order: timestamp_desc, , within: "42,42,100") {
    lat
    lon
    timestamp
  }
}

~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  CreateLocation(lat: 42, lon: 42) {
    lat
    lon
    timestamp
  }
}
~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -F query='{Locations(first: 50, order: timestamp_desc) {lat, lon, timestamp}}' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }
