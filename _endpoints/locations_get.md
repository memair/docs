---
title: /locations
position: 3.1
type: get
description: List users locations
right_code: |
  ~~~ json
  {
    "details": {
      "current_page": 1,
      "last_page": true,
      "next_page": null,
      "total_pages": 1
    },
    "locations": [
      {
        "altitude": 1000.0,
        "altitude_accuracy": 42.0,
        "application": null,
        "created_at": "2018-01-07T12:03:34.685Z",
        "heading": null,
        "id": 2132,
        "lat": 42.0,
        "lon": 42.0,
        "point_accuracy": 4.2,
        "source": "",
        "speed": 0.0,
        "timestamp": "2018-01-01T00:00:00.000Z",
        "updated_at": "2018-01-07T12:03:34.685Z",
        "url": "http://localhost:3000/locations/2132",
        "user_id": 1
      }
    ],
    "user": {
      "email": "otto@gmeow.com",
      "id": 1
    },
    "within": {
      "distance": 1000.0,
      "latitude": 42.0,
      "longitude": 42.0
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "docs": "http://memair.com/docs",
    "error": "Not authorized",
    "info": "Token was unauthorized"
  }
  ~~~
  {: title="Error" }
---
page
: Page number (default 1)

per_page
: Limits the number of locations returned per page (default 1000)

lat
: Latitude for geo queries (must be used with lon and distance)

lon
: Longitude for geo queries (must be used with lat and distance)

distance
: Distance in meters for geo queries (must be used with lat and lon)

Default ordering is by descending timestamp
{: .info }

Lists all the users locations meeting the given parameters. You can paginate by using the parameters listed above. Get the latest location by setting per_page to 1 (with page remaining defaulted to 1).

~~~ bash
curl \
  -d access_token=YOUR_ACCESS_TOKEN \
  -d lat=42.0 \
  -d long=42.0 \
  -d distance=1000 \
  -d page=1 \
  -G GET {{ site.api_url }}v1/locations
~~~
{: title="Curl" }

~~~ python
r = requests.get("{{ site.api_url }}v1/locations", token="YOUR_APP_KEY")
print r.text
~~~
{: title="Python" }
