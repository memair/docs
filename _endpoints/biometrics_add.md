---
title: /biometrics
position: 1.2
type: post
description: Create Biometric
right_code: |
  ~~~ json
  {
    "weight": {
      "status": "saved",
      "value": 5.0,
      "timestamp": "2018-01-01T00:00:00.000Z"
    },
    "internal_body_temp": {
      "status": "saved",
      "value": 8.1,
      "timestamp": "2018-01-01T00:00:00.000Z"
    }
  }
  ~~~
  {: title="Response" }

  ~~~ json
  {
    "weight": {
      "status": "saved",
      "value": 5.0,
      "timestamp": "2018-01-01T00:00:00.000Z"
    },
    "internal_body_temp": {
      "status": "not saved",
      "errors": {
        "value": ["is not a number"]
      }
    }
  }
  ~~~
  {: title="Error" }
---
*biometric slug*
: Biometric slug with reading (see biometric types endpoint for available slugs)

timestamp
: Timestamp of biometric

source
: Source of biometric

notes
: Additional notes regarding the biometric

Adds a biometric reading to users memair.

~~~ python
r = requests.get("https://herokuapps.memair.com/api/v1/biometrics", token="YOUR_APP_KEY")
print r.text
~~~
{: title="Python" }

~~~ bash
curl \
  -F 'weight=5.0' \
  -F 'internal_body_temp=8.1' \
  -F 'timestamp=2018-01-01 00:00:00' \
  -F access_token=YOUR_APP_KEY \
  -X POST https://herokuapps.memair.com/api/v1/biometrics
~~~
{: title="Curl" }
