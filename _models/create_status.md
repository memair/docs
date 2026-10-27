---
title: Bulk Create
position: 3.0
right_code: |
  ~~~ json
  {
    "data": {
      "Create": {
        "id": "123456",
        "recordsTotal": 3
      }
    }
  }
  ~~~
  {: title="Create response" }

  ~~~ json
  {
    "data": {
      "CreateStatus": {
        "hasFinished": true,
        "finishedAt": "2026-10-27T08:20:02Z",
        "recordsProcessed": 3,
        "recordsTotal": 3,
        "importErrors": [
          {
            "emotion": {
              "type": "content",
              "intensity": 42.0,
              "client_uuid": "ed25b45f-e909-4f79-8dfb-38b7e3f67fcf"
            },
            "errors": {
              "intensity": ["must be less than or equal to 10"]
            }
          }
        ]
      }
    }
  }
  ~~~
  {: title="Create Status response" }
---

The `Create` mutation imports many records, of any kinds, in one request. It answers as soon as the import is queued, with a `CreateStatus` whose `id` you then poll. Use it for imports and offline queues. Use [createEmotion and the other single-record mutations](#modelsrecord_mutations) when a person saves one record and waits for the answer.

`Create` takes a list for each kind of record: `biometrics`, `digitalActivities`, `emotions`, `journals`, `locations`, `medications`, `physicalActivities` and `recommendations`. The token needs the write scope of every kind it sends. One request may hold up to 10,000 records, but send at most 1,000: the whole payload goes into one background job.

Poll `CreateStatus(id:)`, with the id as an integer, until `hasFinished` is true. `recordsProcessed` counts up to `recordsTotal`. `importErrors` lists each record that failed validation, echoed as it was sent (with snake_case keys) next to its errors. Only the app that started an import can read its status.

Give every record a `clientUuid`. A record whose `clientUuid` the user already has is skipped: it is not stored twice and not reported as an error. So a batch can be sent again safely, and it should be when its status has not finished after a few minutes, because `Create` answers before the records are stored and a queued import can be lost.

`CreateStatus` also has a list for each kind of record (`biometrics`, `locations` and so on), which returns every record the import created. Leave them out of large imports.

~~~ graphql
mutation {
  Create(
    biometrics: [
      {type: weight, value: 80.2, timestamp: "2026-10-27T07:00:00Z", clientUuid: "0787aab5-2c74-4a77-b316-ed5f8178adfc"}
    ]
    emotions: [
      {type: happy, intensity: 8, clientUuid: "fc7e2be5-61eb-4a8b-86d2-77cf6da1b3a6"}
      {type: content, intensity: 42, clientUuid: "ed25b45f-e909-4f79-8dfb-38b7e3f67fcf"}
    ]
  ) {
    id
    recordsTotal
  }
}
~~~
{: title="Create" }

~~~ graphql
query {
  CreateStatus(id: 123456) {
    hasFinished
    finishedAt
    recordsProcessed
    recordsTotal
    importErrors
  }
}
~~~
{: title="Create Status" }
