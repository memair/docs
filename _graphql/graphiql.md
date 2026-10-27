---
title: GraphiQL
position: 2.0
description: An in-browser console for the API, and its full reference
---

[GraphiQL]({{ site.app_url }}graphiql) is an in-browser console for the API. Sign in to Memair to use it. Queries run as the signed-in user with every scope, so they need no token.

GraphiQL is also the API's full reference. Its documentation explorer reads the live schema and lists every query, mutation, type, field and argument, with descriptions and deprecation reasons. These docs explain concepts and give examples; look up field details there.

GraphiQL sends requests with the browser's session, not a token, so the token queries `AccessToken` and `RevokeAccessToken` fail in it. It allows 60 requests a minute.
