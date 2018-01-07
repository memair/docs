---
title: /emotion_types
position: 2.0
type: get
description: List all Emotion Types
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

Lists all emotion types.

This endpoint requires no authentication
{: .info }

~~~ bash
curl -X GET {{ site.api_url }}v1/emotion_types
~~~
{: title="Curl" }

~~~ python
r = requests.get("{{ site.api_url }}v1/emotion_types")
print r.text
~~~
{: title="Python" }
