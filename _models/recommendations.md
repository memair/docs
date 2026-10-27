---
title: Recommendations
position: 28.0
right_code: |
  ~~~ json
  {
    "data": {
      "recommendations": {
        "nodes": [
          {
            "id": "771204",
            "title": "How GraphQL pagination works",
            "url": "https://graphql.org/learn/pagination/",
            "priority": 80.0,
            "expiresAt": "2026-10-28T04:00:00Z",
            "recommendationType": {
              "name": "Read Article"
            }
          }
        ]
      }
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "data": {
      "ActionRecommendation": true
    }
  }
  ~~~
  {: title="Action response" }
---

A recommendation suggests something to the user: a video, an article, a book, a person to contact. An app creates it, and the user acts on it or ignores it. `RecommendationTypes` lists the types, and [recommendation_types.yml](https://github.com/memair/data-types/blob/master/recommendation_types.yml) defines them.

A new recommendation needs a `type`, a `priority` from 0 to 100, an `expiresAt` in the future, and at least one of `title`, `url`, `description`, `thumbnailUrl`, `duration` (in seconds) and `publishedAt`.

`ActionRecommendation(id:)` marks a recommendation as acted on, or as ignored with `ignored: true`. It needs the `recommendation_action` scope. `isActioned`, `isIgnored` and `isExpired` report the state.

Scopes: `recommendation_read` and `recommendation_write`. Besides the [list arguments](#modelspagination) every record has, `recommendations` filters by `expired`, `actioned` and `ignored`, and can sort by `PRIORITY`.

~~~ graphql
query {
  recommendations(first: 5, expired: false, actioned: false, orderBy: PRIORITY) {
    nodes {
      id
      title
      url
      priority
      expiresAt
      recommendationType {
        name
      }
    }
  }
}
~~~
{: title="List" }

~~~ graphql
mutation {
  createRecommendation(input: {
    type: article
    title: "How GraphQL pagination works"
    url: "https://graphql.org/learn/pagination/"
    priority: 80
    expiresAt: "tomorrow"
    clientUuid: "dab82bc1-6e15-4993-843c-8abcd408098b"
  }) {
    recommendation {
      id
      expiresAt
    }
    errors {
      field
      message
    }
  }
}
~~~
{: title="Create" }

~~~ graphql
mutation {
  ActionRecommendation(id: 771204)
}
~~~
{: title="Action" }
