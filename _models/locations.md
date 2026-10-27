---
title: Locations
position: 25.0
right_code: |
  ~~~ json
  {
    "data": {
      "locations": {
        "nodes": [
          {
            "timestamp": "2026-10-27T12:01:00Z",
            "lat": 45.4215,
            "lon": -75.6972,
            "pointAccuracy": 12.0,
            "timezone": "America/Toronto"
          }
        ]
      }
    }
  }
  ~~~
  {: title="Response" }
---

A location is a point where the user was. Locations have no type.

lat, lon
: latitude from -90 to 90 and longitude from -180 to 180, in degrees

pointAccuracy, altitude, altitudeAccuracy
: in meters

heading
: degrees clockwise from north, at least 0 and less than 360. Send `null` when the device reports no heading; a negative value fails the record.

speed
: in meters per second

timezone
: the time zone at the point, which Memair works out

Scopes: `location_read` and `location_write`. Besides the [list arguments](#modelspagination) every record has, `locations` takes `within: "latitude,longitude,meters"`, which keeps the points within that distance of a place.

A phone that records points while offline should send them in batches through [Bulk Create](#modelscreate_status).

~~~ graphql
query {
  locations(first: 50, within: "45.4215,-75.6972,500") {
    nodes {
      timestamp
      lat
      lon
      pointAccuracy
      timezone
    }
  }
}
~~~
{: title="List" }

~~~ graphql
mutation {
  createLocation(input: {
    lat: 45.4215
    lon: -75.6972
    pointAccuracy: 12
    timestamp: "2026-10-27T12:01:00Z"
    clientUuid: "dca469ef-3996-490b-a45a-ab81e0538998"
  }) {
    location {
      id
      timezone
    }
    errors {
      field
      message
    }
  }
}
~~~
{: title="Create" }
