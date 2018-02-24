---
title: /biometrics
position: 1.1
type: get
description: List users biometrics
right_code: |
  ~~~ json
  {
    "biometrics": [
      {
        "application": null,
        "id": 5,
        "notes": "",
        "source": "",
        "timestamp": "2018-01-05T07:24:57.133Z",
        "weight": 100.0
      },
      ...
      {
        "application": "Greg's Test App",
        "id": 1,
        "internal_body_temp": 37.8,
        "notes": null,
        "source": null,
        "timestamp": "2017-12-23T15:57:53.014Z"
      }
    ],
    "details": {
      "current_page": 1,
      "last_page": true,
      "next_page": null,
      "total_pages": 1
    },
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
: Limits the number of biometrics returned per page (default 1000)

access_token
: access token with correct scopes for memories being accessed. See [Request Access Token](#authenticationrequest_access_token) for more details

Default ordering is by descending timestamp
{: .info }

Lists all the users biometrics. You can paginate by using the parameters listed above.

~~~ bash
curl \
  -d access_token=YOUR_ACCESS_TOKEN \
  -d page=1 \
  -d per_page=100 \
  -G GET {{ site.api_url }}v1/biometrics
~~~
{: title="Curl" }

~~~ python
r = requests.get("{{ site.api_url }}v1/biometrics?access_token=YOUR_APP_KEY")
print r.text
~~~
{: title="Python" }
