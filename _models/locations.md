---
title: Locations
position: 2.0
type: gamma
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

This model is used to store user location data.

#### Model

Grain: 1 row per location type per timestamp. Duplicates will be deleted leaving the latest version.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| lat | integer | required |
| lon | integer | required |
| timestamp | timestamp | assigned by memair if null |
| altitude | integer | in meters & nullable |
| altitude_accuracy | integer | in meters & nullable |
| heading | integer | nullable |
| point_accuracy | integer | in meters & nullable |
| timezone | string | assigned by memair |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
{
  Locations(first: 50, order: timestamp_desc) {
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
  -X POST {{ site.app_url }}/graphql
~~~
{: title="Curl" }
