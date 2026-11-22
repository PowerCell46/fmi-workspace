### Endpoint for initializing a new IoT sensor:
When a new sensor is installed, in order for it to be initialized it has to make a request to this endpoint.

POST request
request format:
```json
{
    internalSecretKey: "String", // TODO: We could name this better
    
    latitude: "BigDecimal",
    
    longitude: "BigDecimal"
}
```

The server should receive this payload and create a new Sensor instance and persist it. There should be a calculation of the following:
The idea is that when a init request is made, the server calculates where it should distribute the sensor in order for them to be evenly 
spread out in terms of exact second of a minute when a request is made to the system (Jitter)

response format:
```json
{
    id: "UUID",
    reportAtSecond: "Integer"
}
```
Or some error

---
### Endpoint for a sensor to submit its report data:
Based on the persisted values reportedAtSecond and id the sensor sends its latest data report.

POST request
request format:
```json
{
    id: "UUID",
    // TODO: We should discuss whether the sensor should send reportedAt, basically the server can calculate it, 
    // based on the reportAtSecond + the timestamp at which the request is received on the server
    surfaceTemperature: "BigDecimal",
    humidity: "BigDecimal",
    slippernessDegree: "BigDecimal"
}
```

The server validates that the id exists, and persists the entry; TODO: what happens after that

response:
success or failure

---
### Endpoint for registering a user:
A new user wants to join our system.

POST request
request format:
```json
{
    username: "String",
    password: "String"
}
```

We should make sure the username is not taken and that the username and password are valid, according to our validations. Password needs to be hashed (bcrypt/argon2).

response format:
TODO: We should discuss how the authentication works
Probably we should return the JWT token in a cookie or some error.

---
### Endpoint for logging into the system:
The session of the user has timed out and he has to log in once again or has logged out

POST request
request format:
```json
{
    username: "String",
    password: "String"
}
```

We should validate the data and check whether the credentials are correct. If they are we log him/her into the system.

response format:
Same as register basically

---
### Endpoint for logging out of the system:
The user wants to sign out of his account

POST request (or DELETE)
no request body

response format:
either success or failure

---
### Endpoint where an admin can alter the role of the users
It's important to discuss here whether the relationship is ManytoOne between User and Role or Many to many

PATCH request
```json
{
    id: "String",
    role: "Role"
}
```

response format:
either successful operation or not (error)

---
### Endpoint where we allow a user to delete their account
In the UI we should have some option where the user could delete his account. In order to do it, he/she has to click confirm at least once
+ write down the username exactly matching. If that's the case we make a request to this endpoint

DELETE request

the system hard deletes the user from the database, we should also make sure that their data is deleted from the archive/backup. All relational entities
should set their user_id to NULL.
IMPORTANT: **Erasure also means the data has to go from everywhere: DB, logs, search indexes, and backups on a retention schedule.**

---
### Endpoint where we allow a user to export their data
In the same place in the UI as the delete account, we should allow the option to the user to export their data in a structured way (JSON for example);
All user related data + related entity entries (FiledProblem).

GET request

---
### Endpoint for fetching the privacy notice
In order to comply with the GDPR rules we should have the following: **"a short page saying what you store, why, and for how long."**
This endpoint should be the source of that. If a change is made on how we store data, FE should be decoupled from the BA's structure. It could be a static
HTML or txt file we read & send out, update the file when we have to.

GET request

---
### Endpoint where a registered user files a report
подават сигнали за проблеми, които се включват в приоритизацията на обработка от операторите по поддръжка

POST request
```json
{
    latitude: "BigDecimal",
    longitude: "BigDecimal",
    filedAt: "Date",
    problemType: "Enum",
    image: "String" // TODO: We should discuss how the image is being sent
}

The server receives the request, validates the data, persist the image in the object storage and then persists the entry in the database

---
