### Endpoint for initializing a new IoT sensor:
When a new sensor is installed, in order for it to be initialized it has to make a request to this endpoint

POST request
request format:
```json
{
    authenticationKey: "String", // This should be renamed
    
    latitude: "BigDecimal",
    
    longitude: "BigDecimal",
}
```

The server should receive this payload and create a new Sensor instance and persist it. There should be a calculation of the following:
// TODO: The idea is that when a init request is made, the server calculates where it should distribute the
// sensor in order for them to be evenly spread out in terms of exact second of a minute when a request is made to the system
response format:
```json
{
    id: "UUID"
}
```

---
### Endpoint for a sensor to submit its report data
Based on the persisted values reportedAtSecond and id the sensor sends its latest data
```json
{
    id: "UUID",
    // TODO: We should discuss whether the sensor should send reportedAt, basically the server can calculate it, based on the reportAtSecond + the timestamp at which the request is received
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
A new user wants to join our system

POST request
request format:
```json
{
    username: "String",
    password: "String"
}
```

We should make sure the username is not taken and that the username and password are valid, according to our validations.

response format:
TODO: We should discuss how the authentication works

---
### Endpoint for logging into the system
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
TODO: See Register

