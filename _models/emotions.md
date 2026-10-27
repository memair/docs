---
title: Emotions
position: 23.0
right_code: |
  ~~~ json
  {
    "data": {
      "emotions": {
        "nodes": [
          {
            "timestamp": "2026-10-27T08:15:00Z",
            "intensity": 7.0,
            "emotionType": {
              "name": "Happy",
              "emoji": "😀"
            }
          }
        ]
      }
    }
  }
  ~~~
  {: title="Response" }
---

An emotion is a feeling of a defined type with an `intensity` from 0 to 10. `EmotionTypes` lists the types with their emoji, and [emotion_types.yml](https://github.com/memair/data-types/blob/master/emotion_types.yml) defines them.

Scopes: `emotion_read` and `emotion_write`. Besides the [list arguments](#modelspagination) every record has, `emotions` can sort by `INTENSITY`.

~~~ graphql
query {
  emotions(first: 5) {
    nodes {
      timestamp
      intensity
      emotionType {
        name
        emoji
      }
    }
  }
}
~~~
{: title="List" }

~~~ graphql
mutation {
  createEmotion(input: {
    type: happy
    intensity: 7
    clientUuid: "4c007994-6335-40fb-a14c-0c12f006daf7"
  }) {
    emotion {
      id
    }
    errors {
      field
      message
    }
  }
}
~~~
{: title="Create" }
