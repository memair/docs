---
title: Revoke an Access Token
position: 9
right_code: |
  ~~~ json
  {
    "data": {
      "RevokeAccessToken": {
        "revoked": true
      }
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "errors": [
      {
        "message": "Otto's token can not revoked, others may want to play with his data",
        "locations": [{"line": 2, "column": 3}],
        "path": ["RevokeAccessToken"]
      }
    ],
    "data": {
      "RevokeAccessToken": null
    }
  }
  ~~~
  {: title="Error" }
---

Revoke a token when the app no longer needs it or when it may have leaked. A revoked token stops working at once.

The `RevokeAccessToken` mutation revokes the token that sends it. [Otto's token](#authenticationotto) cannot be revoked.

~~~ graphql
mutation {
  RevokeAccessToken {
    revoked
  }
}
~~~
{: title="GraphQL" }

~~~ bash
curl https://memair.com/graphql \
  -H 'Authorization: Bearer 0000000000000000000000000000000000000000000000000000000000000000' \
  -H 'Content-Type: application/json' \
  -d '{"query": "mutation { RevokeAccessToken { revoked } }"}'
~~~
{: title="Curl" }

Memair also has the standard revocation endpoint, `POST {{ site.app_url }}oauth/revoke` ([RFC 7009](https://www.rfc-editor.org/rfc/rfc7009.html)). Send the `token` with the app's `client_id` and `client_secret`.

Users can revoke an app's tokens themselves under Account > [Installed]({{ site.app_url }}oauth/authorized_applications).
