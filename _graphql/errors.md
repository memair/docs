---
title: Errors
position: 6.0
description: Where the API reports each kind of failure
right_code: |
  ~~~ json
  {
    "error": {
      "message": "Rate limit exceeded"
    },
    "data": {}
  }
  ~~~
  {: title="HTTP error" }

  ~~~ json
  {
    "errors": [
      {
        "message": "Access Token does not have permission for requested scope, please see docs.memair.com for more details",
        "locations": [{"line": 1, "column": 3}],
        "path": ["medications"]
      }
    ],
    "data": null
  }
  ~~~
  {: title="GraphQL error" }

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
  {: title="Field error" }
---

The API reports a failure in one of three places, so a client checks all three.

#### HTTP status

`401` means the token is missing, unknown, revoked or expired ([Use an Access Token](#authenticationuse_access_token)). `429` means a rate limit ([API Limits](#documentationapi_rate_limits)). `400` means the request had no query. These responses carry `error.message` and no GraphQL result.

#### GraphQL errors

Everything else answers HTTP `200`. A query that does not match the schema, an argument the server refuses, or a field outside the token's [scopes](#authenticationscopes) adds an entry to the top-level `errors` list, with the `path` of the field. The failed field returns `null`. When that field cannot be null, the `null` moves up to its parent, as far as `data` itself.

#### Field errors in mutation payloads

`createEmotion`, `updateEmotion`, `deleteEmotion` and the same mutations for every other record report validation failures in the payload's `errors` list, not in the top-level `errors`. Each `FieldError` has the input `field` it belongs to, or `null` when it concerns the whole record, and a `message` to show the user. The record in the payload is `null` whenever `errors` is not empty. Read `errors` on every mutation, even when the response has no top-level errors.

`Create` imports in the background, so its validation failures appear later, in `CreateStatus.importErrors` ([Bulk Create](#modelscreate_status)).
