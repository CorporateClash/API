---
title: API Documentation

language_tabs:
  - python

toc_footers:
  - <a href='https://github.com/CorporateClash/API'>Made with &hearts; by TTCC developers.</a>

includes:
  - errors

search: true
---

# Introduction

```python
# Our web-server and all accompanying APIs only work over
# Secure HTTPS connections with TLS v1.1 or 1.2, and clients
# must support elliptic curve cryptography (ECC) and SNI.
# Key pinning is not supported at this time. You will need a
# Python 3.x build to successfully run our code samples.
```

Welcome to the official Toontown: Corporate Clash API!

You may use this API document at your own expense, we have no liability over the third-party applications that are built with our software. You can find more on this, stated specifically in our <a href="https://corporateclash.net/help/terms">Terms of Service</a>.

For bug reporting, feedback, and support please <a href="mailto:support@corporateclash.net">contact our support team</a>.

# Authentication

## Login API (v1)

> General Login

```python
# https://pypi.python.org/pypi/requests
import requests

credentials = {
    'username' : 'your_username',
    'password' : 'your_password',
}

url = ('https://corporateclash.net/api/v1/login/')

r = requests.post(url, json=credentials)
print(r.json())
```

* `https://corporateclash.net/api/v1/login/`
* Responds with a JSON object detailing the status of the login request, along with temporary gameserver information utilized by the TTCC client.


| Params     | Description                                           |
|------------|-------------------------------------------------------|
| username   | The account username.   |
| password   | The account password.   |


### API Response

> JSON Response

```json
{
  "status": true,
  "reason": 0,
  "friendlyreason": "",
  "token": ""
}
```

| Field | Type        | Description                      |
|------|-------------|----------------------------------|
| status  | boolean   | Whether there were any issues when logging in. |
| reason  | integer   | Unique identifier for why the login was rejected/accepted. |
| friendlyreason   | string | Human-readable message detailing why the login was rejected/accepted.  |
| token  | string | Temporary game token that is valid for 2 minutes (60 seconds) after being served. |

### Reason 0: Successful login
The submitted credentials were verified as correct.

### Reason 2: Confusion
There are several accounts with the similar identifiers.

### Reason 3: User ban
The user has been HWID checked and banned.

### Reason 4: Unmet requisites
User did not meet the login requisites. (access level, etc)

### Reason 5: Invalid playertoken
The users playertoken was either not found or corrupted.

# Gameserver

## District API (v1)

> Fetch Districts

```python
# https://pypi.python.org/pypi/requests
import requests

url = ('https://corporateclash.net/api/v1/districts/')

r = requests.get(url)
print(r.json())
```

* `https://corporateclash.net/api/v1/districts/`
* Provides various details regarding the status of all running districts.
* Responds in JSON format.


### API Response

> JSON Response

```json
[
    {
        "name": "",
    	"population": 0,
    	"invasion_online": "true",
    	"last_update": "",
    	"cogs_attacking": "",
    	"count_defeated": 0,
    	"count_total": 0,
    	"remaining_time": 0
    },

    {
        "name": "",
    	"population": 0,
    	"invasion_online": "true",
    	"last_update": "",
    	"cogs_attacking": "",
    	"count_defeated": 0,
    	"count_total": 0,
    	"remaining_time": 0
    }
]
```

| Field | Type        | Description                      |
|------|-------------|----------------------------------|
| name  | string   | Name of the district. |
| population  | integer   | Total population of the district. |
| invasion_online   | string | Whether or not there is an active invasion on the district.  |
| last_update  | string | The last point at which the districts' data was updated. |
| cogs_attacking  | string   | The type of cog that is invading the district. Left empty if no active invasion. |
| count_defeated  | integer   | Total amount of cogs defeated. Left empty if no active invasion. |
| count_total   | integer | Total amount of cogs invading. Left empty if no active invasion. |
| remaining_time  | integer | The last point at which the districts' data was updated. |
