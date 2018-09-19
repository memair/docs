---
title: Request Authorization
position: 4
---

Send user to;

```
{{ site.app_url }}oauth/authorize?client_id=YOUR_CLIENT_ID&redirect_uri=http://redirect.com&response_type=code&scope=location_read+location_write
```

And collect `USER_CODE` in the call back url
