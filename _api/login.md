---
title: /api/v1/login/
position: 0
type: post
description: Responds with a JSON object detailing the status of the login request, along with a temporary gameserver token.
right_code: |
  ~~~ python
  # https://pypi.python.org/pypi/requests
  import requests
  import urllib

  params = urllib.urlencode({'password' : 'your_password'})
  url = ('https://corporateclash.net/api/v1/login/%s' % ('your_username'))

  r = requests.post(url, data=params)
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

Callback

| Status | Reason        | Reason                      |
|------|-------------|----------------------------------|
| true  | 0   | Welcome back to Toontown!     |
| false  | 2          | There are several accounts with the similar identifiers.                          |
| false  | 3     | The user has been HWID checked and banned.           |
| false  | 4 | Insufficient access level. |
| false  | 5   | The users playertoken was either not found or corrupted.     |
