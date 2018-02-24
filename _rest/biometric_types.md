---
title: /biometric_types
position: 1.0
type: get
description: Lists all Biometric Types
right_code: |
  ~~~ json
  {
    "biometric_types": [
      {
        "about": null,
        "id": 1,
        "name": "Body Weight",
        "slug": "weight",
        "unit": "Kilogram",
        "unit_symbol": "kg"
      },
      ...
      {
        "about": "Internal Body Temperature",
        "id": 4,
        "name": "Internal Body Temperature",
        "slug": "internal_body_temp",
        "unit": "Celsius",
        "unit_symbol": "°C"
      }
    ]
  }
  ~~~
  {: title="Response" }
---

This endpoint requires no authentication
{: .info }

~~~ bash
curl {{ site.api_url }}v1/biometric_types
~~~
{: title="Curl" }

~~~ python
import requests
r = requests.get("{{ site.api_url }}v1/biometric_types")
print(r.text)
~~~
{: title="Python" }