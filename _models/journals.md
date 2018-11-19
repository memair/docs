---
title: Journals
position: 24.0
type: gamma
right_code: |
  ~~~ json
  {
    "data": {
      "Journals": [
        {
          "timestamp": "2018-01-01T00:00:00Z",
          "document": 80,
          "journal_type": {
            "name": "Idea"
          }
        }
      ]
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "data": None,
    "errors": [
      {
        "message": "Please limit requests to 10000 records",
        "locations": [{"line": 3, "column": 3}],
        "path": ["Journals"]
      }
    ]
  }
  ~~~
  {: title="Error" }
---

This model is used to store user data for defined journal types like concept, idea, or thought. A full list of journal types can be accessed using the `JournalTypes` endpoint or inspecting the [data-types repo](https://github.com/memair/data-types/blob/master/journal_types.yml). Please create a [pull request](https://github.com/memair/data-types/blob/master/journal_types.yml) or [contact us](https://blog.memair.com/community/contact) to add journal types.

#### Model

Grain: 1 row per journal type per timestamp. Duplicates will be deleted leaving the latest version.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| journal_type | journal type | required |
| document | integer | required |
| timestamp | timestamp | assigned by memair if null |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
query {
  Journals(first: 1, order: desc, order_by: timestamp, type: idea) {
    timestamp
    document
    journal_type {
      name
    }
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  CreateJournal(document: "Cat barbershop, not sure if it's for cats of just has cats running around", type: idea) {
    timestamp
    document
    journal_type {
      name
    }
  }
}

~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -F query='{Journals(first: 1 order: desc order_by: timestamp type: idea) {timestamp document journal_type {name}}}' \
  -F access_token=YOUR_ACCESS_TOKEN \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('YOUR_ACCESS_TOKEN')
query = "{Journals(first: 1 order: desc order_by: timestamp type: idea) {timestamp document journal_type {name}}}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
