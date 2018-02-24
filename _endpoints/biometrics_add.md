---
title: /biometrics
position: 1.2
type: post
description: Create Biometric
right_code: |
  ~~~ json
  {
    "weight": {
      "status": "saved",
      "value": 5.0,
      "timestamp": "2018-01-01T00:00:00.000Z"
    },
    "internal_body_temp": {
      "status": "saved",
      "value": 8.1,
      "timestamp": "2018-01-01T00:00:00.000Z"
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "weight": {
      "status": "saved",
      "value": 5.0,
      "timestamp": "2018-01-01T00:00:00.000Z"
    },
    "internal_body_temp": {
      "status": "not saved",
      "errors": {
        "value": ["is not a number"]
      }
    }
  }
  ~~~
  {: title="Error" }
---

**Deprecation Notice:** This endpoint will deprecated and replaced with a [GraphQL](/#graphqlgraphql) equivalent.

*biometric slug*
: Biometric slug with reading (see biometric types endpoint for available slugs)

timestamp
: Timestamp of biometric (default now)

source
: Source of biometric

notes
: Additional notes regarding the biometric

access_token
: access token with correct scopes for memories being accessed. See [Request Access Token](#authenticationrequest_access_token) for more details

Adds a biometric reading to users memair.

~~~ bash
curl \
  -F 'weight=5.0' \
  -F 'internal_body_temp=36.9' \
  -F 'timestamp=2018-01-01 00:00:00' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.api_url }}v1/biometrics
~~~
{: title="Curl" }

~~~ python
data = {
  'weight' : 80,
  'internal_body_temp': 36.9,
  'timestamp': '2018-01-01 00:00:00',
  'access_token': 'YOUR_APP_KEY'
}
import requests
r = requests.post("{{ site.api_url }}v1/biometrics", data)
print(r.text)
~~~
{: title="Python" }
