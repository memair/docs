---
title: Request Access Token
position: 4
type: post
right_code: |
  ~~~ json
  {
    "access_token": "de6780bc506a0446309bd9362820ba8aed28aa506c71eedbe1c5c4f9dd350e54",
    "token_type": "bearer",
    "created_at": 1457567765
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "error": true,
    "message": "Invalid score"
  }
  ~~~
  {: title="Error" }
---

To request the access token, you should use the returned code from above and exchange it for an access token.

~~~ bash
curl \
  -F grant_type=authorization_code \
  -F client_id=YOUR_CLIENT_ID \
  -F client_secret=YOUR_CLIENT_SECRET \
  -F code=USERS_CODE \
  -F redirect_uri=http://redirect.com \
  -X POST {{ site.app_url }}oauth/token
~~~
{: title="Curl" }
