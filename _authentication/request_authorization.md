---
title: Request Authorization
position: 5
---

Send the user to Memair's authorization page in a browser:

~~~
{{ site.app_url }}oauth/authorize?response_type=code&client_id=YOUR_CLIENT_ID&redirect_uri=https%3A%2F%2Fexample.com%2Fcallback&scope=location_read+location_write&state=RANDOM_VALUE
~~~

response_type
: `code`. The authorization code grant is the only one Memair supports.

client_id
: the app's Client ID

redirect_uri
: one of the app's registered redirect URIs, URL-encoded

scope
: the [scopes](#authenticationscopes) the app needs, separated by spaces (`+` in a URL). Each must be one the app registered. Without `scope`, the token gets only `public`.

state
: a random value the app keeps and compares when the user comes back, which protects the redirect against cross-site request forgery ([RFC 6749 §10.12](https://www.rfc-editor.org/rfc/rfc6749.html#section-10.12))

code_challenge, code_challenge_method
: optional for apps registered through API Keys. When sent, the method must be `S256` ([RFC 7636](https://www.rfc-editor.org/rfc/rfc7636.html)).

The user signs in if needed and approves the scopes. Memair then redirects to `redirect_uri` with `code` and `state` in the query string. If the user declines, the redirect carries `error=access_denied` instead.

A code is valid for 10 minutes and can be exchanged once. [Request an Access Token](#authenticationrequest_access_token) describes the exchange.
