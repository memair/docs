---
title: Create an App
position: 3
---

An app that other people use needs its own OAuth client. To register one:

1. Sign in to [Memair]({{ site.app_url }}users/sign_in).
2. Open Developer Tools > [API Keys]({{ site.app_url }}oauth/applications) > [New Application]({{ site.app_url }}oauth/applications/new).
3. Enter a name, the app's redirect URIs (one per line), and the [scopes](#authenticationscopes) it needs.

The application's page then shows its Client ID and Client Secret. Keep the secret on your server.

Redirect URIs must use `https`, or a custom scheme such as `com.example.app:/oauth/callback`. Memair rejects `http` URIs, `http://localhost` included.

Apps registered this way are confidential clients. Their access tokens do not expire, and they get no refresh token. PKCE is optional for them, but a `code_challenge` must use the `S256` method.

Ask only for the scopes the app uses. The user sees them on the consent screen.
