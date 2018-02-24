---
title: /emotions
position: 2.1
type: get
description: List users emotions
right_code: |
  ~~~ json
  {
    "details": {
      "current_page": 1,
      "last_page": true,
      "next_page": null,
      "total_pages": 1
    },
    "emotions": [
      {
        "application": "Greg's Test App",
        "emotion_type": "Anguish",
        "id": 2,
        "intensity": 4.5,
        "notes": null,
        "source": null,
        "timestamp": "2018-01-01T00:00:00.000Z"
      },
      {
        "application": "Greg's Test App",
        "emotion_type": "Happy",
        "id": 1,
        "intensity": 5.0,
        "notes": null,
        "source": null,
        "timestamp": "2018-01-01T00:00:00.000Z"
      }
    ],
    "user": {
      "email": "otto@gmeow.com",
      "id": 1
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

**Deprecation Notice:** This endpoint will deprecated and replaced with a [GraphQL](/#graphqlgraphql) equivalent.

page
: Page number (default 1)

per_page
: Limits the number of emotions returned per page (default 1000)

access_token
: access token with correct scopes for memories being accessed. See [Request Access Token](#authenticationrequest_access_token) for more details

Default ordering is by descending timestamp
{: .info }

Lists all the users emotions. You can paginate by using the parameters listed above.

~~~ bash
curl \
  -d access_token=YOUR_ACCESS_TOKEN \
  -d page=1 \
  -d per_page=100 \
  -G GET {{ site.api_url }}v1/emotions
~~~
{: title="Curl" }

~~~ python
r = requests.get("{{ site.api_url }}v1/emotions?access_token=YOUR_APP_KEY")
print r.text
~~~
{: title="Python" }
