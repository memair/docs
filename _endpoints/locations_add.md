---
title: /locations
position: 3.2
type: post
description: Create Location
right_code: |
  ~~~ json
  {
    "altitude": null,
    "altitude_accuracy": null,
    "application": "Greg's Test App",
    "created_at": "2018-01-07T12:14:34.416Z",
    "email": "otto@gmeow.com",
    "heading": null,
    "id": 2134,
    "latitude": 42.0,
    "longitude": 42.0,
    "point_accuracy": null,
    "source": null,
    "speed": null,
    "timestamp": "2018-01-01T00:00:00.000Z",
    "tzid": "UTC",
    "updated_at": "2018-01-07T12:14:34.416Z"
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "errors": {
      "longitude": [
        "is not a number"
      ]
    },
    "status": "not saved"
  }
  ~~~
  {: title="Error" }
---

latitude
: Latitude

longitude
: Longitude

timestamp
: Timestamp of location

altitude
: Altitude (meters)

point_accuracy
: Point Accuracy (meters)

altitude_accuracy
: Altitude Accuracy (meters)

Heading
: heading (degrees from north)

Speed
: speed (meters per second)

source
: Source of location

Adds a location to users memair.

~~~ bash
curl \
  -F latitude=42 \
  -F longitude=42 \
  -F 'timestamp=2018-01-01 00:00:00' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.api_url }}v1/locations
~~~
{: title="Curl" }

~~~ python
r = requests.get("{{ site.api_url }}v1/locations", token="YOUR_APP_KEY")
print r.text
~~~
{: title="Python" }
