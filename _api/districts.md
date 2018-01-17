---
title: /v1/districts/
position: 1
type: get
description: Provides various details regarding the status of all running districts.
right_code: |
  ~~~ python
  # https://pypi.python.org/pypi/requests
  import requests

  url = ('https://corporateclash.net/api/v1/districts/')

  r = requests.get(url)
  print(r.json())
  ~~~
  {: title="Python" }
---

Response Array

~~~ json
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
~~~
{: title="JSON" }

Response Fields

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
