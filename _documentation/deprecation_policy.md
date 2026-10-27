---
title: Deprecation Policy
position: 3
---

Memair adds to the API without notice, and removes from it only after a deprecation period of at least six months.

#### Additive changes

A new type, field, optional argument or enum value ships when it is ready. Write clients that ignore fields and enum values they do not know.

#### Breaking changes

A breaking change removes or renames a type, field, argument or enum value, makes an argument required, or narrows what a field returns or an argument accepts. It goes through deprecation:

1. Memair adds the replacement and marks the old element deprecated. The deprecation reason names the replacement and the earliest removal date.
2. The earliest removal date is six months after the deprecation reaches production.
3. Memair removes the element after that date, once it has had no use in the previous 30 days and no supported release of Memair's iOS app uses it.

Memair counts each use of a deprecated field, argument or enum value per OAuth application, which is how it knows when an element has gone quiet. GraphiQL's documentation explorer marks deprecated elements and shows their reasons. Introspection returns them with `isDeprecated` and `deprecationReason`.

### Notices

These are deprecated, with removal after 2027-05-01.

| Deprecated | Use instead |
|------------|-------------|
| `Biometrics`, `DigitalActivities`, `Emotions`, `Journals`, `Locations`, `Medications`, `PhysicalActivities`, `Recommendations` | `biometrics`, `digitalActivities`, `emotions`, `journals`, `locations`, `medications`, `physicalActivities`, `recommendations`, which page by cursor ([Pagination](#modelspagination)) |
| `CreateBiometric`, `CreateDigitalActivity`, `CreateEmotion`, `CreateJournal`, `CreateLocation`, `CreateMedication`, `CreatePhysicalActivity`, `CreateRecommendation` | `createBiometric` and the other single-record creates, which answer validation failures as field errors ([Create, Update and Delete](#modelsrecord_mutations)) |
| `DeleteRecommendation` | `deleteRecommendation` |
