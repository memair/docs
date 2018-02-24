---
title: /emotions
position: 2.2
type: post
description: Create Emotion
right_code: |
  ~~~ json
  {
    "happy": {
      "status": "saved",
      "intensity": 5.0,
      "timestamp": "2018-01-01T00:00:00.000Z"
    },
    "anguish": {
      "status": "saved",
      "intensity": 4.5,
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

*emotion slug*
: Emotion slug with reading (see emotion types endpoint for available slugs)

timestamp
: Timestamp of emotion (default now)

source
: Source of emotion

notes
: Additional notes regarding the emotion

access_token
: access token with correct scopes for memories being accessed. See [Request Access Token](#authenticationrequest_access_token) for more details

Adds a emotion reading to users memair.

~~~ bash
curl \
  -F 'happy=5.0' \
  -F 'anguish=4.5' \
  -F 'timestamp=2018-01-01 00:00:00' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.api_url }}v1/emotions
~~~
{: title="Curl" }

~~~ python
data = {
  'happy' : 5.0,
  'anguish': 4.5,
  'timestamp': '2018-01-01 00:00:00',
  'access_token': 'YOUR_APP_KEY'
}
r = requests.post("{{ site.api_url }}v1/emotions", data)
print r.text
~~~
{: title="Python" }
