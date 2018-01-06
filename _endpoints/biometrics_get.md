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
      "email": "greg@gho.st",
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
page
: Page number

per_page
: Limits the number of biometrics returned per page

This call will return a maximum of 100 biometrics per page
{: .info }

Lists all the users biometrics. You can paginate by using the parameters listed above.

~~~ python
r = requests.get("https://herokuapps.memair.com/api/v1/biometrics", token="YOUR_APP_KEY")
print r.text
~~~
{: title="Python" }

~~~ bash
curl \
  -F access_token=YOUR_APP_KEY \
  -F page=1 \
  -F per_page=100 \
  -X GET https://herokuapps.memair.com/api/v1/biometrics
~~~
{: title="Curl" }
