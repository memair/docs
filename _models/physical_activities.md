---
title: Physical Activities
position: 27.0
right_code: |
  ~~~ json
  {
    "data": {
      "physicalActivities": {
        "nodes": [
          {
            "timestamp": "2026-10-26T17:30:00Z",
            "duration": 1800.0,
            "endedAt": "2026-10-26T18:00:00Z",
            "meta": {"distance_m": 5000},
            "physicalActivityType": {
              "name": "Running"
            }
          }
        ]
      }
    }
  }
  ~~~
  {: title="Response" }
---

A physical activity is something the user did with their body over a period, from running and yoga to deep sleep. `PhysicalActivityTypes` lists the types, and [physical_activity_types.yml](https://github.com/memair/data-types/blob/master/physical_activity_types.yml) defines them.

`duration` is in seconds, and `endedAt` is `timestamp` plus `duration`. `meta` holds any details. Memair's Apple Health import records a workout's distance and energy there, as `distance_m` and `active_energy_kcal`.

Scopes: `physical_activity_read` and `physical_activity_write`.

~~~ graphql
query {
  physicalActivities(first: 5, type: running) {
    nodes {
      timestamp
      duration
      endedAt
      meta
      physicalActivityType {
        name
      }
    }
  }
}
~~~
{: title="List" }

~~~ graphql
mutation {
  createPhysicalActivity(input: {
    type: running
    timestamp: "2026-10-26T17:30:00Z"
    duration: 1800
    meta: {distance_m: 5000}
    clientUuid: "ceb8f9de-cbc4-432b-b490-e382b5a70bac"
  }) {
    physicalActivity {
      id
      endedAt
    }
    errors {
      field
      message
    }
  }
}
~~~
{: title="Create" }
