---
title: Scopes
position: 4
---

Each access token carries scopes, and each part of the API checks for one. A request outside the token's scopes gets the error `Access Token does not have permission for requested scope`, with no data for that field.

| Scope | Allows |
|-------|--------|
| `biometric_read`, `biometric_write` | reading, or creating, changing and deleting, biometrics |
| `digital_activity_read`, `digital_activity_write` | the same for digital activities |
| `emotion_read`, `emotion_write` | the same for emotions |
| `journal_read`, `journal_write` | the same for journals |
| `location_read`, `location_write` | the same for locations |
| `medication_read`, `medication_write` | the same for medications |
| `physical_activity_read`, `physical_activity_write` | the same for physical activities |
| `recommendation_read`, `recommendation_write` | the same for recommendations |
| `recommendation_action` | marking a recommendation actioned or ignored with `ActionRecommendation` |
| `recommendation_delete` | the deprecated `DeleteRecommendation` only; `deleteRecommendation` needs `recommendation_write` |
| `insight_read`, `insight_write` | reading and creating insights |
| `preset_read` | listing the user's presets with `presets` and running one with `runPreset`; a preset runs with the token's other scopes, so it writes only what the token may write |
| `user_details` | the `UserDetails` query: the user's email, time zone and record counts |
| `public` | granted to every token; nothing checks it |

A write scope covers `Create`, `createX`, `updateX` and `deleteX` for its records. It does not include the read scope: a token with `emotion_write` alone can create emotions but not list them.

The `AccessToken` query, the `*Types` queries, `MedicationForms`, `recordResources`, `RevokeAccessToken` and `CreateStatus` need no scope. `CreateStatus` returns only imports that the same app started. `recordResources` reports, for each record resource, whether the token may read (`readable`) and write (`writable`) it.
