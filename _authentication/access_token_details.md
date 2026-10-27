---
title: Access Token Details
position: 8
right_code: |
  ~~~ json
  {
    "data": {
      "AccessToken": {
        "expired": false,
        "revoked": false,
        "expiresAt": null,
        "locationRead": true,
        "scopes": "location_read location_write"
      }
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "errors": [
      {
        "message": "No Access Token used to access this endpoint. You are likely accessing this endpoint through GraphiQL so are not using an Access Token",
        "locations": [{"line": 2, "column": 3}],
        "path": ["AccessToken"]
      }
    ],
    "data": {
      "AccessToken": null
    }
  }
  ~~~
  {: title="Error" }
---

The `AccessToken` query describes the token that sent the request: its scopes, when it expires, and whether it has been revoked. Each scope also has a Boolean field, such as `locationRead`.

GraphiQL runs as the signed-in user without a token, so this query fails there.

~~~ graphql
query {
  AccessToken {
    expired
    revoked
    expiresAt
    locationRead
    scopes
  }
}
~~~
{: title="GraphQL" }

~~~ bash
curl https://memair.com/graphql \
  -H 'Authorization: Bearer 0000000000000000000000000000000000000000000000000000000000000000' \
  -H 'Content-Type: application/json' \
  -d '{"query": "{ AccessToken { expired revoked expiresAt locationRead scopes } }"}'
~~~
{: title="Curl" }
