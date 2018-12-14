---
title: Revoke Access Token
position: 7
right_code: |
  ~~~ json
  {
    "data": {
      "RevokeAccessToken": [
        {
          "revoked": true
        }
      ]
    }  
  }

  ~~~
  {: title="Response" }

  ~~~ json
  {
    "data": {
      "RevokeAccessToken": null
    }
    "errors": {
      "message": "Otto's token can not revoked, others may want to play with his data"
    }
  }
  ~~~
  {: title="Error" }
---

Revoked tokens will no longer work. It is good practice to revoke tokens when they are no longer needed or if they are exposed. Revoking an Access Token can be access though the GraphQL API (see [below](#graphqlabout) for more details on GraphQL).

Note: You can not revoke [Otto's access token](#authenticationotto)

~~~ graphql
mutation {
  RevokeAccessToken {
    revoked
  }
}

~~~
{: title="GraphQL" }

~~~ bash
curl \
  -H 'access_token: 0000000000000000000000000000000000000000000000000000000000000000' \
  -d 'mutation{RevokeAccessToken{revoked}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = "mutation{RevokeAccessToken{revoked}}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
