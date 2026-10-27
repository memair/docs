---
title: Request an Access Token
position: 6
right_code: |
  ~~~ json
  {
    "access_token": "Yq3nC0bW1u7mH2xvJk9TzR4pL8sQe6dAfG5hN0oVwXc",
    "token_type": "Bearer",
    "scope": "location_read location_write",
    "created_at": 1793111916
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "error": "invalid_grant",
    "error_description": "The provided authorization grant is invalid, expired, revoked, does not match the redirection URI used in the authorization request, or was issued to another client."
  }
  ~~~
  {: title="Error" }
---

Exchange the code from the redirect for an access token. Make this request from your server, because it carries the client secret.

~~~ bash
curl https://memair.com/oauth/token \
  -d grant_type=authorization_code \
  -d client_id=YOUR_CLIENT_ID \
  -d client_secret=YOUR_CLIENT_SECRET \
  -d code=CODE_FROM_THE_REDIRECT \
  -d redirect_uri=https://example.com/callback
~~~
{: title="Curl" }

grant_type
: `authorization_code`

client_id, client_secret
: the app's credentials from API Keys

code
: the `code` from the redirect

redirect_uri
: the same redirect URI the authorization request used

code_verifier
: required when the authorization request sent a `code_challenge`

Store the `access_token` for the user. A token issued to an app registered through API Keys does not expire, so the response has no `expires_in` and no `refresh_token`.

The token endpoint allows 10 requests a minute from one IP address.
