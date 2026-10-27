---
title: Digital Activities
position: 22.0
right_code: |
  ~~~ json
  {
    "data": {
      "digitalActivities": {
        "nodes": [
          {
            "timestamp": "2026-10-27T09:12:00Z",
            "duration": 300.0,
            "url": "https://docs.memair.com",
            "title": "Memair Docs"
          }
        ]
      }
    }
  }
  ~~~
  {: title="Response" }
---

A digital activity is something the user did on a device, such as opening an app, visiting a website or watching a video. `DigitalActivityTypes` lists the types, and [digital_activity_types.yml](https://github.com/memair/data-types/blob/master/digital_activity_types.yml) defines them.

`duration` is in seconds, and `endedAt` is `timestamp` plus `duration`. `meta` holds any details; `url` and `title` return `meta.url` and `meta.title`.

Scopes: `digital_activity_read` and `digital_activity_write`.

~~~ graphql
query {
  digitalActivities(first: 20, type: visited_website) {
    nodes {
      timestamp
      duration
      url
      title
    }
  }
}
~~~
{: title="List" }

~~~ graphql
mutation {
  createDigitalActivity(input: {
    type: visited_website
    duration: 300
    meta: {url: "https://docs.memair.com", title: "Memair Docs"}
    clientUuid: "d06fc445-9bec-4d06-85ca-ba23c2ad7ea5"
  }) {
    digitalActivity {
      id
      url
    }
    errors {
      field
      message
    }
  }
}
~~~
{: title="Create" }
