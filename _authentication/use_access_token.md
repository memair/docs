---
title: Use an Access Token
position: 7
right_code: |
  ~~~ json
  {
    "error": {
      "message": "Invalid access token provided, please see docs.memair.com for more details"
    },
    "data": {}
  }
  ~~~
  {: title="401 Response" }
---

Send the token in the `Authorization` header of every API request:

~~~
Authorization: Bearer 0000000000000000000000000000000000000000000000000000000000000000
~~~

Memair also reads the token from an `Access-Token` header, and from an `access_token` or `bearer_token` parameter, which older clients use. Prefer the `Authorization` header. A token in a URL can end up in logs and browser history ([RFC 6750 §5.3](https://www.rfc-editor.org/rfc/rfc6750.html#section-5.3)).

A missing, unknown, revoked or expired token gets HTTP `401` and a `WWW-Authenticate` header ([RFC 6750 §3.1](https://www.rfc-editor.org/rfc/rfc6750.html#section-3.1)):

- no token: `WWW-Authenticate: Bearer`
- any other token problem: `WWW-Authenticate: Bearer error="invalid_token"`

A valid token that lacks a scope gets HTTP `200` and a GraphQL error instead. See [Errors](#graphqlerrors).
