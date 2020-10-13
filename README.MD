# CapCabin2 Rest API
----------

## Intro
Current Rest API provides basic set CRUD operations to the dynamically generated JSON-server database. The server is running on port: `9200` and supports relevant HTTP methods e.g `POST, GET, PUT, DELETE`
</br>
</br>
To start the server:
  1. Clone the repo & make sure you have latest NodeJS installed
  2. Navigate to the capcabin2 folder via your favourite CLI
  3. Run `npm i` command to install dependencies
  4. Run `npm start` to start the JSON server
</br>
</br>
## Endpoints:
JSON server exposes following endpoints on the port **9200**:

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

### Fething data (HTTP GET CALLS)
</br>

- To get a list of `users`, `cains` or `reservations` simply execute an HTTP `GET` request to the appropriate endpoint:
```
Request -> GET: http://localhost:9200/users
----------

Response <-: Array of users
[
  {
    "id": 210,
    "firstName": "Anette",
    "lastName": "Normann",
    "role": "admin"
  },
  {
    "id": 211,
    "firstName": "Ola",
    "lastName": "Normann",
    "role": "admin"
  },
  {
    "id": 200,
    "firstName": "Jonas",
    "lastName": "Johannes",
    "role": "user"
  },
  {
    "id": 201,
    "firstName": "Siri",
    "lastName": "Stormberg",
    "role": "user"
  }

...

]
```
</br>

- To get data about specific `user`, `cabin` or `reservation`, execute HTTP `GET` request to the appropriate endpoint with an object specific **id** provided at the end of the url, a such as `http://localhost:9200/users/200` will return data of a user with `id:` 200.
</br>

Get specific user data:
```
Request -> GET: http://localhost:9200/users/200
----------

Response <-:  A User object matching provided ID
{
  "id": 200,
  "firstName": "Jonas",
  "lastName": "Johannes",
  "role": "user"
}
```
</br>

Get specific cabin data:
```

Request -> GET: http://localhost:9200/cabins/110
----------

Response <-: A Cabin object matching provided ID
{
  "id": 110,
  "name": "Ulvik Resort",
  "address": "Havnegata 41, 7500 Stjørdal",
  "description": "Ulvik Resort is 1 km from Stjørdal, the island's main area, and offers air-conditioned accommodation. Free WiFi access is available. The nearest kebab place is 1.5 km away.",
  "imageUrl": "https://source.unsplash.com/320x240/?villa,hotel,house,vacation",
  "googleMapsUrl": "https://www.google.com/maps/@63.3563844,9.6467183,17z",
  "rank": 5,
  "price": "3800 NOK"
}
```
</br>

Get specific Reservation data:
```
Request -> GET: http://localhost:9200/reservations/3036
----------

Response <-: A Reservation object matching provided ID
{
  "id": 3036,
  "cid": 103,
  "uid": 203,
  "from": "19/10/2020",
  "to": "09/11/2020"
}
```
</br>

### Updating data (HTTP PUT CALLS)
- To update specific  `user`, `cabin` or `reservation`, execute HTTP `PUT` request to the appropriate endpoint with an object specific **id** provided at the end of the url, such as `http://localhost:9200/users/205`, and data object provided in the body of the request:

```
HTTP PUT

CABINS:       http://localhost:9200/cabins/{id}
USERS:        http://localhost:9200/users/{id}
RESERVATIONS: http://localhost:9200/reservations/{id}
```

User before update:
```
{
  "id": 210,
  "firstName": "Anette",
  "lastName": "Normann",
  "role": "admin"
}
```
```
Request -> PUT: http://localhost:9200/users/210
Body: 
{
  "firstName": "Leeroy",
  "lastName": "Jenkins",
  "role": "user"
}
----------

Response <-: Updated user
{
  "id": 210,
  "firstName": "Leeroy",
  "lastName": "Jenkins",
  "role": "user"
}
```
</br>

### Creating new data (HTTP POST CALLS)
- To push new object to the `user`, `cabin` or `reservation` database, execute HTTP `POST` request to the appropriate endpoint with the respective object provided as a HTTP request body.

```
HTTP POST

- CABINS:       http://localhost:9200/cabins
  body: 
  {
    "name": string,
    "address": string,
    "description": string,
    "imageUrl": string,
    "googleMapsUrl": string,
    "rank": number,
    "price": string
  }

- USERS:        http://localhost:9200/users
  body:
  {
    "firstName": string,
    "lastName": string,
    "role": string<"user" | "admin">
  }

- RESERVATIONS: http://localhost:9200/reservations
  body:
  {
    "cid": number,  // cabin id
    "uid": number,  // user id
    "from": string, // DD/MM/YYYY
    "to": string    // DD/MM/YYYY
  }
```

Creating a new user:
```
Request -> POST: http://localhost:9200/user
Body: 
{
  "firstName": "Betty",
  "lastName": "Blue",
  "role": "admin"
}
----------

Response <-: Created user
{
    "id": 212,
    "firstName": "Betty",
    "lastName": "Blue",
    "role": "admin",
}
```
</br>

### DELETING new data (HTTP DELETE CALLS)
- To delete `user`, `cabin` or `reservation` from the database, execute HTTP `DELETE` request to the appropriate endpoint with an object specific **id** provided at the end of the url, such as `http://localhost:9200/cabins/107`.

```
HTTP DELETE

CABINS:       http://localhost:9200/cabins/{id}
USERS:        http://localhost:9200/users/{id}
RESERVATIONS: http://localhost:9200/reservations/{id}
```

Deleting a cabin:
```
Request -> POST: http://localhost:9200/cabin/107
----------

Response <-: Empty object
```

