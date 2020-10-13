# CapCabin2 Rest API
----------

## Intro
Current Rest api provides basic set CRUD operations to the dynamically generated JSON-server database. The server is running on port: `9200` and supports relevant HTTP methods e.g `POST, GET, PUT, DELETE`
</br>
</br>
## Endpoints:
Following endpoints are available:

```
CABINS:       http://localhost:9200/cabins
USERS:        http://localhost:9200/users
RESERVATIONS: http://localhost:9200/reservations
```
</br>

#### NOTE:
- When you make POST, PUT, PATCH or DELETE requests, changes will be automatically and safely saved to `db.json`
- Your request body JSON should be object enclosed, just like the GET output. (for example `{"name": "Foobar"}`)
- A POST, PUT or PATCH request should include a `Content-Type: application/json` header to use the JSON in the request body. Otherwise it will return a 2XX status code, but without changes being made to the data.
</br>
</br>

## EXAMPLES:
</br>

#### Fething data (HTTP GET CALLS)
</br>

1. To get a list of `users, cains` or `reservations` simply execute an HTTP `GET` request to any of the endpoints:
```
Request -> GET: http://localhost:9200/users
----------

Response <-: Array of users
[
  {
    "uid": 210,
    "firstName": "Anette",
    "lastName": "Normann",
    "role": "admin"
  },
  {
    "uid": 211,
    "firstName": "Ola",
    "lastName": "Normann",
    "role": "admin"
  },
  {
    "uid": 200,
    "firstName": "Jonas",
    "lastName": "Johannes",
    "role": "user"
  },
  {
    "uid": 201,
    "firstName": "Siri",
    "lastName": "Stormberg",
    "role": "user"
  }

...

]
```
</br>

2. To get data about specific user or cabin, execute `GET` request with an object specific *id* provided as a url query string, a such as `http://localhost:9200/users?uid=200` will return data of a user with `uid:` 200.

#### NOTE:
- `User` object uses field name `uid` as ID
- `Cabin` object uses field name `cid` as ID
</br>

```
Request -> GET: http://localhost:9200/users?uid=200
----------

Response <-: Array of users matching provided UID
[
  {
    "uid": 200,
    "firstName": "Jonas",
    "lastName": "Johannes",
    "role": "user"
  }
]
```
or in the case of cabins the request might look like:
```
Request -> GET: http://localhost:9200/cabins?cid=110
----------

Response <-: Array of cabins matching provided CID
[
  {
    "cid": 110,
    "name": "Ulvik Resort",
    "address": "Havnegata 41, 7500 Stjørdal",
    "description": "Ulvik Resort is 1 km from Stjørdal, the island's main area, and offers air-conditioned accommodation. Free WiFi access is available. The nearest kebab place is 1.5 km away.",
    "imageUrl": "https://source.unsplash.com/320x240/?villa,hotel,house,vacation",
    "googleMapsUrl": "https://www.google.com/maps/@63.3563844,9.6467183,17z",
    "rank": 5,
    "price": "3800 NOK"
  }
]
```
</br>

#### Updating data (HTTP PUT CALLS)
