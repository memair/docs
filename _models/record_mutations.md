---
title: Create, Update and Delete
position: 2.0
right_code: |
  ~~~ json
  {
    "data": {
      "createEmotion": {
        "emotion": {
          "id": "5820117",
          "timestamp": "2026-10-27T08:15:00Z",
          "intensity": 7.0,
          "emotionType": {"name": "Happy"}
        },
        "errors": []
      }
    }
  }
  ~~~
  {: title="Create response" }

  ~~~ json
  {
    "data": {
      "createEmotion": {
        "emotion": null,
        "errors": [
          {
            "field": "intensity",
            "message": "Intensity must be less than or equal to 10"
          }
        ]
      }
    }
  }
  ~~~
  {: title="Validation error" }

  ~~~ json
  {
    "data": {
      "deleteEmotion": {
        "deletedId": null,
        "errors": [
          {"field": null, "message": "Emotion not found"}
        ]
      }
    }
  }
  ~~~
  {: title="Unknown id" }
---

Each kind of record has three mutations that act on one record and answer at once: `createEmotion(input:)`, `updateEmotion(id:, input:)` and `deleteEmotion(id:)`, and the same for `Biometric`, `DigitalActivity`, `Journal`, `Location`, `Medication`, `PhysicalActivity` and `Recommendation`. All three need the record's write scope.

Each answers with a payload that holds the record (`deletedId` for a delete) and `errors`. A validation failure leaves the record `null` and adds a `FieldError` for each problem, naming the input field it belongs to. An id the user does not have gives an error with `field: null`. See [Errors](#graphqlerrors).

#### Safe retries

Send a random UUID as `clientUuid` with every create, generated once when the user saves. If the response is lost and the client sends the create again, Memair answers with the record it already stored instead of storing a second one.

#### Partial updates

An update changes the fields named in `input` and keeps the rest. Send `null` to clear an optional field such as `notes`. A record keeps the `clientUuid` it was created with.

~~~ graphql
mutation {
  createEmotion(input: {
    type: happy
    intensity: 7
    timestamp: "2026-10-27T08:15:00Z"
    source: "Example app"
    clientUuid: "ff47e3c3-067b-42ca-8626-97e52406b0d6"
  }) {
    emotion {
      id
      timestamp
      intensity
      emotionType {
        name
      }
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
  updateEmotion(id: "5820117", input: {
    intensity: 5
    notes: null
  }) {
    emotion {
      id
      intensity
      notes
    }
    errors {
      field
      message
    }
  }
}
~~~
{: title="Update" }

~~~ graphql
mutation {
  deleteEmotion(id: "5820117") {
    deletedId
    errors {
      field
      message
    }
  }
}
~~~
{: title="Delete" }
