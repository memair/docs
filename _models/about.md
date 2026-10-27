---
title: About the Models
position: 0.0
---

Memair stores eight kinds of records: biometrics, digital activities, emotions, journals, locations, medications, physical activities and recommendations. All eight have the same shape in the API, so what these pages show for one kind works for the others:

- a cursor-paged list, such as `emotions`, and a by-id field, such as `emotion(id:)` ([Pagination](#modelspagination))
- `createEmotion`, `updateEmotion` and `deleteEmotion` ([Create, Update and Delete](#modelsrecord_mutations))
- an argument of the bulk `Create` mutation, such as `emotions` ([Bulk Create](#modelscreate_status))
- a read scope and a write scope, such as `emotion_read` and `emotion_write` ([Scopes](#authenticationscopes))

[Insights](#modelsinsights) are older and work differently.

#### Fields every record has

id
: assigned by Memair

timestamp
: when it happened. Memair uses the time of the request when it is left out.

source
: free text naming where the record came from, such as an app or a device

clientUuid
: a UUID the client generated, which makes creates safe to retry

updatedAt
: when the record last changed

All but locations also have `notes`. Digital activities, journals, medications and physical activities have `meta`, a JSON object for details the model has no field for.

#### Types

Most records have a type chosen by its slug: a biometric's `type: weight`, an emotion's `type: happy`, a medication's `form: oral_tablet`. The slugs are GraphQL enum values. `BiometricTypes`, `DigitalActivityTypes`, `EmotionTypes`, `JournalTypes`, `MedicationForms`, `PhysicalActivityTypes` and `RecommendationTypes` list them with their names, and units where they have them. Their definitions are in the [data-types repo](https://github.com/memair/data-types), and many say which Apple Health samples they correspond to (`healthKit`).

To suggest a new type, open a pull request on data-types or [contact us](https://blog.memair.com/contact).

#### Describing the records

The `recordResources` query describes each kind of record: its list and by-id fields, its mutations, and the fields of its form, with labels, kinds, units, ranges and choices. It also says whether the token may read and write each kind. Memair's phone apps draw their record screens from it.
