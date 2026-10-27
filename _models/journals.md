---
title: Journals
position: 24.0
right_code: |
  ~~~ json
  {
    "data": {
      "journals": {
        "nodes": [
          {
            "timestamp": "2026-10-20T21:00:00Z",
            "document": "Grow catnip in the garden to attract more cats",
            "journalType": {
              "name": "Idea"
            }
          }
        ]
      }
    }
  }
  ~~~
  {: title="Response" }
---

A journal entry is a piece of text, `document`, of a defined type such as an idea, a dream or a gratitude. `JournalTypes` lists the types, and [journal_types.yml](https://github.com/memair/data-types/blob/master/journal_types.yml) defines them.

Scopes: `journal_read` and `journal_write`.

~~~ graphql
query {
  journals(first: 5, type: idea) {
    nodes {
      timestamp
      document
      journalType {
        name
      }
    }
  }
}
~~~
{: title="List" }

~~~ graphql
mutation {
  createJournal(input: {
    type: idea
    document: "Grow catnip in the garden to attract more cats"
    clientUuid: "e1feb553-0619-495e-af31-d87fb12e07d3"
  }) {
    journal {
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
