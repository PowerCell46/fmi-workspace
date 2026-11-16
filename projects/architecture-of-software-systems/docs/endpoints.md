### Endpoint for initializing a new IoT sensor:
When a new sensor is installed, in order for it to be initialized it has to make a request to this endpoint.

POST request
request format:
```json
{
    authenticationKey: "String", // TODO: This should be renamed
    
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

We should make sure the username is not taken and that the username and password are valid, according to our validations. Password needs to be encrypted.

response format:
TODO: We should discuss how the authentication works
Probably we should return the JWT token in a cookie or some error.

---
### Endpoint for logging into the system:
The session of the user has timed out and he has to log in once again (or has logged out, if we add such functionality)

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
### Endpoint where an admin can alter the role of the users
It's important to discuss here whether the relationship is ManytoOne between User and Role or Many to many

```json
{
    username: "String", // or id
    role: "Role"
}
```

response format:
either successful operation or not (error)

---
### Endpoint where a registered user files a report
подават сигнали за проблеми, които се включват в приоритизацията на обработка от операторите по поддръжка

POST request
```json
{
    latitude: "BigDecimal",
    longitude: "BigDecimal",
    filedAt: "String", // new Date().toISOString() or however it was in JS
    problemType: "", // TODO: 1. Should it be enum or free text; 2. We should rename the field for sure
    image: "String" // TODO: We should discuss how the image is being sent
}

The server receives the request, validates the data, persist the image in the object storage and then persists the entry in the database

---
