---
title: API Limits
position: 5
right_code: |
  ~~~ json
  {
    "error": {
      "message": "Rate limit exceeded"
    },
    "data": {}
  }
  ~~~
  {: title="429 Response" }
---

Memair limits how often each access token can call the API and how much one request can ask for. A request over a rate limit gets HTTP `429`.

#### Rate limits

| Endpoint | Limit | Counted per |
|----------|-------|-------------|
| `POST /graphql` | 20 requests in 10 seconds, and 300 in 5 minutes | access token |
| `POST /oauth/token`, exchanging a code | 10 requests a minute | IP address |
| `POST /oauth/token`, refreshing a token | 10 requests a minute | refresh token |
| GraphiQL | 60 requests a minute | signed-in user |

A request without a token counts against its IP address.

#### Request size

- A record list returns at most 1,000 records per page, and 25 when `first` is not given ([Pagination](#modelspagination)).
- `Create` accepts up to 10,000 records per request. Send at most 1,000 ([Bulk Create](#modelscreate_status)).
- A query may nest fields at most 13 levels deep, and select at most 300 fields in total. A query over either limit fails without running.
