---
title: /emotion_types
position: 2.0
type: get
description: Lists all Emotion Types
right_code: |
  ~~~ json
  {
    "emotion_types": [
      {
        "id": 1,
        "name": "Happy",
        "slug": "happy",
        "adjective": null,
        "noun": null,
        "about": null,
        "emoji": "😀"
      },
      ...
      {
        "id": 13,
        "name": "Anguish",
        "slug": "anguish",
        "adjective": null,
        "noun": null,
        "about": null,
        "emoji": "😧"
      }
    ]
  }
  ~~~
  {: title="Response" }
---

This endpoint requires no authentication
{: .info }

~~~ bash
curl {{ site.api_url }}v1/emotion_types
~~~
{: title="Curl" }

~~~ python
import requests
r = requests.get("{{ site.api_url }}v1/emotion_types")
print(r.text)
~~~
{: title="Python" }
