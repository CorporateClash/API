---
title: /v1/login/:username
position: 0
type: post
description: Responds with a JSON object detailing the status of the login request, along with a temporary gameserver token.
right_code: |
  ~~~ python
  # https://pypi.python.org/pypi/requests
  import requests

  jsonData = {'password' : 'your_password'}
  url = ('https://corporateclash.net/api/v1/login/' + 'your username')

  r = requests.post(url, json=jsonData)
  print(r.json())
  ~~~
  {: title="Python" }
---
password
: The users password.

Response Object

~~~ json
{
  "status": true,
  "reason": 0,
  "friendlyreason": "",
  "token": ""
}
~~~
{: title="JSON" }

Response Fields

| Field | Type        | Description                      |
|------|-------------|----------------------------------|
| status  | boolean   | Whether there were any issues when logging in. |
| reason  | integer   | Unique identifier for why the login was rejected/accepted. |
| friendlyreason   | string | Human-readable message detailing why the login was rejected/accepted.  |
| token  | string | Temporary game token that is valid for 2 minutes (60 seconds) after being served. |

Callback

| Status | Reason        | Reason                      |
|------|-------------|----------------------------------|
| true  | 0   | Welcome back to Toontown!     |
| false  | 2          | There are several accounts with the similar identifiers.                          |
| false  | 3     | The user has been HWID checked and banned.           |
| false  | 4 | User did not meet the login requisites. (access level, etc) |
| false  | 5   | The users playertoken was either not found or corrupted.     |

The login API only works over Secure HTTPS connections with TLS v1.1 or 1.2, and clients must support elliptic curve cryptography (ECC) and SNI. Key pinning is not supported at this time.
