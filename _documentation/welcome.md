---
title: Welcome
position: 1
---

Memair stores a person's quantified-self data: biometrics, emotions, journals, locations, medications, physical and digital activities, recommendations and insights. Apps read and write that data through one GraphQL API, `https://memair.com/graphql`, with an OAuth 2.0 access token that the person grants.

To start:

1. Get a token. [Quick Access](#authenticationquick_access) gives you a temporary one for your own account, and [Otto](#authenticationotto) is a sandbox account anyone can use.
2. Send a query. The [curl example](#graphqlcurl) runs as written with Otto's token.
3. Register an app before other people use it. [Create an App](#authenticationcreate_an_app) starts the OAuth flow.

These pages explain how the API works and give one or two examples for each kind of record. For every field and argument, use the documentation explorer in [GraphiQL](#graphqlgraphiql), which reads the live schema.

Paste a token into "add to examples" in the sidebar to put it into every example on the page.

Found a mistake? Open an [issue](https://github.com/memair/docs/issues) or a [pull request](https://github.com/memair/docs/pulls).
