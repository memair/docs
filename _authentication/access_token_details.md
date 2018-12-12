---
title: Access Token Details
position: 6
right_code: |
  ~~~ json
  {
    "data": {
      "AccessTokenDetails": [
        {
          "expired": false,
          "revoked": false,
          "location_read": true,
          "scopes": "location_read location_write public"
        }
      ]
    }  
  }

  ~~~
  {: title="Response" }

  ~~~ json
  {
    "data": {
      "AccessToken": null
    }
    "errors": {
      "message": "No Access Token used to access this endpoint. You are likely accessing this endpoint through GraphiQL so are not using an Access Token"
    }
  }
  ~~~
  {: title="Error" }
---

Access Token details can be access though the GraphQL API (see [below](#graphqlabout) for more details on GraphQL). Accessible details include expire & revoke status, scopes, and associated user's details.

~~~ graphql
query {
  AccessToken {
    expired
    revoked
    location_read
    scopes
  }
}

~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -H 'access_token: 0000000000000000000000000000000000000000000000000000000000000000' \
  -d '{AccessToken{expired revoked location_read scopes}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = "{AccessToken{expired revoked location_read scopes}}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
