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

> Important Note

```python
# Our web-server and all accompanying APIs only work over
# Secure HTTPS connections with TLS v1.1 or 1.2, and clients
# must support elliptic curve cryptography (ECC) and SNI.
# Key pinning is not supported at this time, howerver you
# may confirm that the certificate is issued by the following
# Certificate Authorities (or check against our CAA records):
# comodoca.com
# digicert.com
# globalsign.com
# letsencrypt.org
# Our code samples are specifically made for Python 3.
```

Welcome to the official Toontown: Corporate Clash API!

You may use this API document at your own expense, we have no liability over the third-party applications that are built with our software. You can find more on this, stated specifically in our <a href="https://corporateclash.net/help/terms">Terms of Service</a>.

For bug reporting, feedback, and support please <a href="mailto:support@corporateclash.net">contact our support team</a>.

# Launcher

## Login API (v1)

> Generic Request

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
  "reason": 1000,
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

### Reason 1000: Successful Login
The submitted credentials were verified as correct.

### Reason 1002: Account Termination
The account has been terminated as result of 10 or more moderation points.

### Reason 1003: Account Ban
The account has an an active ban delimited by the hours left.

### Reason 1004: Server Maintenance
The account is locked out of the server due to pending maintenance.

### Reason 1005: Invalid Token
The account token submitted doesn't exist.

## Manifest API (v1)

> Generic Request

```python
# https://pypi.python.org/pypi/requests
import requests

url = ('https://corporateclash.net/api/v1/launcher/manifest/')
headers = {'user-agent': 'TTCC-Launcher'}

r = requests.post(url, headers=headers)
print(r.json())
```

* `https://corporateclash.net/api/v1/launcher/manifest/`
* Responds with a nested JSON object detailing all files required to power the game on an operational level, along with the base URL of where those resources are hosted.


### API Response

> JSON Response

```json
{
  "files": {
    "win32": [
      {
        "path": "win32/cg.dll",
        "hash": "ae87223e882670029450b3f86e8e9300",
        "file": "cg.dll"
      }
    ],
    "game": [
      {
        "path": "game/ttcc.bin",
        "hash": "f6959e45e56a8c5368111b29d257219a",
        "file": "ttcc.bin"
      }
    ],
    "darwin": [
      {
        "path": "darwin/Cg",
        "hash": "007be4a7fcb7c8eacb80f0572b2658d1",
        "file": "Cg"
      }
    ],
    "resources": [
      {
        "path": "resources/phase_10.mf",
        "hash": "771cddc5f5a8f3cc8f4fa7b3a91e511f",
        "file": "phase_10.mf"
      }
    ]
  },

  "base": "https://cdn.clash.lol/"
}
```

### Main JSON Object

| Field | Type        | Description                      |
|------|-------------|----------------------------------|
| base  | string   | The base URL which is prepended to each asset's path field. |

| JSON | Type        | Description                      |
|------|-------------|----------------------------------|
| files  | array   | Holds the 4 nested JSON arrays that represent the four major categories of assets. |
| win32  | array   | Holds all the required dependencies for the windows platform. |
| game  | array   | Holds all the game binaries required for all supported platforms. |
| darwin  | array   | Holds all the required dependencies for the macintosh platform. |
| resources  | array   | Holds all the game resources required for all supported platforms. |

### Nested JSON Objects / Items

| Field | Type        | Description                      |
|------|-------------|----------------------------------|
| path  | string   | The path of the asset which is appended to the base URL. |
| hash  | string <md5>   | The MD5 hash of the asset. |
| file  | string   | The raw name of the asset. |

## Blog API (v1)

> Generic Request

```python
# https://pypi.python.org/pypi/requests
import requests

url = ('https://corporateclash.net/api/v1/launcher/news/')

r = requests.get(url)
print(r.json())
```

> Specific Request

```python
# https://pypi.python.org/pypi/requests
import requests

# :id = 1 to specifically get the first article
url = ('https://corporateclash.net/api/v1/launcher/news/1')

r = requests.get(url)
print(r.json())
```

* `https://corporateclash.net/api/v1/launcher/news/:id`
* Responds with an array of JSON objects representing news items.

### API Response

> JSON Response

```json
[
  {
    "id": 1,
    "author": "The Team",
    "posted": "2018-03-29 21:38:50",
    "title": "First Article!",
    "summary": "See what this blog post has in store!",
    "category": "alpha-updates"
  }
]
```

| Field | Type        | Description                      |
|------|-------------|----------------------------------|
| id  | integer   | The article identifier. |
| author  | string   | Who posted this article. |
| posted  | timestamp  | When this article was posted. |
| title  | string   | The title of the article. |
| summary   | string | A brief description of the article.  |
| category   | string | What this article is categorized as.  |


## Version API (v1)

> Generic Request

```python
# https://pypi.python.org/pypi/requests
import requests

url = ('https://corporateclash.net/api/v1/launcher/version/')

r = requests.get(url)
print(r.json())
```

* `https://corporateclash.net/api/v1/launcher/version/`
* Responds with a single JSON object representing the official launcher version.

### API Response

> JSON Response

```json
{
  "version": "1.x.x"
}
```

| Field | Type        | Description                      |
|------|-------------|----------------------------------|
| version  | string   | Number representing the current version of the official launcher. |

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


# Restrictions

## Rate Limiting

* You may send 10 requests to any public API every 60 seconds.
* If the origin of the requests are rate limited too often, it will be temporarily blocked.


### API Response

> JSON Response

```json
{
  "status": false,
  "reason": 429,
  "friendlyreason": "",
  "token": ""
}
```

| Field | Type        | Description                      |
|------|-------------|----------------------------------|
| status  | boolean: false   | Your API request failed. |
| reason  | integer   | Code regarding the status of your request. |
| friendlyreason   | string | Human-readable message detailing why the login was rate limited.  |
| token  | string | Empty, API request reject. |

### Reason 429: Rate Limit
You're trying to send that request too fast!
