---
title: Medications
position: 26.0
type: beta
right_code: |
  ~~~ json
  {
    "data": {
      "Medications": [
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
        "path": ["Medications"]
      }
    ]
  }
  ~~~
  {: title="Error" }
---

This model is used to store user medication usage data. A full list of medication forms can be accessed using the `MedicationForms` endpoint or inspecting the [data-types repo](https://github.com/memair/data-types/blob/master/medication_forms.yml). Please create a [pull request](https://github.com/memair/data-types/blob/master/medication_forms.yml) or [contact us](https://blog.memair.com/community/contact) to add new medication forms.

#### Model

Grain: 1 row per medication usage. Duplicates will be deleted leaving the latest version.

| Name | Type | Notes |
|-------|--------|---------|
| id | integer | assigned by memair |
| medication_form | medication form | required |
| dose | float | required |
| medication_name | string | required |
| timestamp | timestamp | assigned by memair if null |
| source | string | nullable |
| notes | string | nullable |
| updated_at | timestamp | assigned by memair |

#### Example interactions

See the [Documentation Explorer]({{ site.app_url }}graphiql) for full list of mutations and query filters.

~~~ graphql
query {
  Medications(
    first: 1
    order: desc
    order_by: timestamp
    form: oral_tablet
  ) {
    timestamp
    dose
    medication_name
  }
}
~~~
{: title="GraphQL Query" }

~~~ graphql
mutation {
  Create(
    medications: [
      {
        dose: 0.2
        form: oral_tablet
        medication_name: "ibuprofen"
      }
    ]
  )
  {
    id
    records_total
  }
}
~~~
{: title="GraphQL Mutation" }

~~~ bash
curl \
  -H 'access-token: 0000000000000000000000000000000000000000000000000000000000000000' \
  -d '{Medications(first: 1 order: desc order_by: timestamp form: oral_tablet) {timestamp dose medication_name}}' \
  -X POST {{ site.app_url }}graphql
~~~
{: title="Curl" }

~~~ python
from memair import Memair

user = Memair('0000000000000000000000000000000000000000000000000000000000000000')
query = "{Medications(first: 1 order: desc order_by: timestamp form: oral_tablet) {timestamp dose medication_name}}"
response = user.query(query)
print(response)
~~~
{: title="Python" }
