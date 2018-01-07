---
title: /physical_activity_types
position: 4.0
type: get
description: List all Physical Activity Types
right_code: |
  ~~~ json
  {
    "emotion_types": [
      {
        "id": 1,
        "name": "Acroyoga",
        "slug": "acroyoga",
        "about": "Acrobatic Yoga"
      },
      ...
      {
        "id": 118,
        "name": "Zumba",
        "slug": "zumba",
        "about": null
      }
    ]
  }
  ~~~
  {: title="Response" }
---

Lists all physical activity types.

This endpoint requires no authentication
{: .info }

~~~ python
r = requests.get("{{ site.api_url }}v1/physical_activity_types")
print r.text
~~~
{: title="Python" }

~~~ bash
curl -X GET {{ site.api_url }}v1/physical_activity_types
~~~
{: title="Curl" }
