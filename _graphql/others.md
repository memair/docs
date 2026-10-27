---
title: Other Languages
position: 99.0
description: Any HTTP or GraphQL client works
---

Any language that can send an HTTPS POST with a JSON body can use the API. The [curl](#graphqlcurl), [Python](#graphqlpython) and [Ruby](#graphqlruby) examples show the whole request. GraphQL client libraries, such as those listed on [graphql.org](https://graphql.org/community/tools-and-libraries/), work too: point them at `https://memair.com/graphql` and add the `Authorization` header.

The endpoint answers introspection queries, so tools that generate client code from a schema can read it with any valid token.

To add an example for another language, open a [pull request](https://github.com/memair/docs/pulls).
