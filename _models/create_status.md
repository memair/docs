---
title: Create Status
position: 2.0
type: gamma
right_code: |
  ~~~ json
  {
    "data": {
      "Create": {
        "id": "123456"
      }
    }
  }
  ~~~
  {: title="Create Response" }
  ~~~ json
  {
    "data": {
      "CreateStatus": {
        "records_processed": 4,
        "records_total": 4,
        "has_finished": true,
        "finished_at": "2019-05-28T18:04:05Z",
        "import_errors": [
          {
            "errors": {
              "intensity": [
                "must be less than or equal to 10"
              ]
            },
            "emotion": {
              "type": "content",
              "intensity": 42
            }
          }
        ],
        "biometrics": [
          {
            "id": "131",
            "value": 37,
            "biometric_type": {
              "name": "Internal Body Temperature"
            }
          }
        ],
        "emotions": [
          {
            "emotion_type": {
              "name": "Happy"
            },
            "intensity": 8
          },
          {
            "emotion_type": {
              "name": "Anxious"
            },
            "intensity": 2
          }
        ]
      }
    }
  }
  ~~~
  {: title="Create Status Response" }
---

The `CreateStatus` query gives you details about a `Create` mutation. `Create` mutations are processed in the background. Background processing times are dependant on the size of the job, current queue, and database load. Currently jobs take an average of 1.18 seconds to complete.

~~~ graphql
mutation {
  Create(
    biometrics: [
      {type: internal_body_temp, value: 37}
    ]
    emotions: [
      {type: happy, intensity: 8}
      {type: anxious, intensity: 2}
      {type: content, intensity: 42}
    ]
  ) {
    id
  }
}
~~~
{: title="Create" }

~~~ graphql
query {
  CreateStatus(id: 123456) {
    records_processed
    records_total
    has_finished
    finished_at
    import_errors
    biometrics {
      id
      value
      biometric_type {
        name
      }
    }
    emotions {
      emotion_type {
        name
      }
      intensity
    }
  }
}
~~~
{: title="Create Status" }
