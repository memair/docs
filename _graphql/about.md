---
title: About the API
position: 1.0
description: One GraphQL endpoint reads and writes a user's data
---

Memair's API is GraphQL at one endpoint: `POST https://memair.com/graphql`. A request sends a JSON body with a `query` and, optionally, `variables` and `operationName`. The response is JSON with `data`, and with `errors` when something failed ([GraphQL over HTTP](https://graphql.org/learn/serving-over-http/)). New to GraphQL? [graphql.org/learn](https://graphql.org/learn/) covers the query language.

~~~ json
{
  "query": "query RecentEmotions($first: Int) { emotions(first: $first) { nodes { timestamp intensity emotionType { name } } } }",
  "variables": { "first": 5 }
}
~~~
{: title="Request body" }

#### Names

- Arguments and object fields are camelCase: `fromTimestamp`, `biometricType`, `recordsTotal`.
- The older top-level fields keep capitalised names: `Create`, `CreateStatus`, `AccessToken`, `BiometricTypes`. Newer ones are camelCase: `biometrics`, `createEmotion`.
- Type slugs are snake_case enum values, such as `weight`, `happy` and `oral_tablet`. The `orderBy` and `direction` values of record lists are upper case: `TIMESTAMP`, `DESC`.

#### Scalars

DateTime
: returned in UTC as ISO 8601, such as `2026-10-27T14:03:00Z`. Accepted as ISO 8601, epoch seconds, epoch milliseconds, `"now"`, `"today"`, `"yesterday"`, `"tomorrow"`, or `"last 14 days"` (with `seconds`, `minutes`, `hours`, `days`, `weeks`, `months` or `years`). The relative values count from midnight in the user's time zone, except `"now"`.

JSON
: an object, written either as a GraphQL object literal, `{distance_m: 5000}`, or as a string of JSON

UUID
: a UUID in its 36-character form, such as `1b9d6bcd-bbfd-4b2d-9b5d-ab8dfbbd4bed`. A malformed UUID fails the whole request.

ID
: a record's id, sent as a string or an integer

Every field and argument is described in [GraphiQL](#graphqlgraphiql).
