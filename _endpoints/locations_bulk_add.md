---
title: /bulk/locations
position: 3.2
type: post
description: Create Bulk Locations
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
    "docs": "http://memair.com/docs",
    "error": "Not authorized",
    "info": "Token was unauthorized"
  }
  ~~~
  {: title="Error" }
---

json
: JSON blob containing list of locations using parameters as above

access_token
: access token with correct scopes for memories being accessed. See [Request Access Token](#authenticationrequest_access_token) for more details

Adds multiple locations to users memair.

~~~ bash
curl \
  -F 'json=[{"latitude": 42, "longitude": 42, "timestamp": "2018-01-01 00:00:00"}, {"latitude": 42, "longitude": 42, "timestamp": "2018-01-01 00:05:00", "point_accuracy": 100}]' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.api_url }}v1/bulk/locations
~~~
{: title="Curl" }

~~~ python
data = {
  'json' : '[{"latitude": 42, "longitude": 42, "timestamp": "2018-01-01 00:00:00"}, {"latitude": 42, "longitude": 42, "timestamp": "2018-01-01 00:05:00", "point_accuracy": 100}]',
  'access_token': 'YOUR_APP_KEY'
}
import requests
r = requests.post("{{ site.api_url }}v1/bulk/locations", data)
print(r.text)
~~~
{: title="Python" }
