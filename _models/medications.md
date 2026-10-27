---
title: Medications
position: 26.0
right_code: |
  ~~~ json
  {
    "data": {
      "medications": {
        "nodes": [
          {
            "timestamp": "2026-10-27T08:00:00Z",
            "medicationName": "Ibuprofen",
            "dose": 400.0,
            "meta": {"dose_unit": "mg"},
            "medicationForm": {
              "name": "oral (tablet)"
            }
          }
        ]
      }
    }
  }
  ~~~
  {: title="Response" }
---

A medication record is one dose the user took. `medicationName` and `form` are required. `form` is how it was taken, such as `oral_tablet` or `inhaled_vapour`: `MedicationForms` lists the forms, and [medication_forms.yml](https://github.com/memair/data-types/blob/master/medication_forms.yml) defines them.

`dose` is a number with no unit. Memair's Apple Health import stores the unit in `meta`, as `dose_unit`.

Scopes: `medication_read` and `medication_write`. [Otto's token](#authenticationotto) has neither, so try these examples with [your own token](#authenticationquick_access). Lists filter by `form` instead of `type`.

~~~ graphql
query {
  medications(first: 5, form: oral_tablet) {
    nodes {
      timestamp
      medicationName
      dose
      meta
      medicationForm {
        name
      }
    }
  }
}
~~~
{: title="List" }

~~~ graphql
mutation {
  createMedication(input: {
    medicationName: "Ibuprofen"
    form: oral_tablet
    dose: 400
    meta: {dose_unit: "mg"}
    clientUuid: "0e0a70fd-de6b-4cfe-9a6c-03c5dcc00d6a"
  }) {
    medication {
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
