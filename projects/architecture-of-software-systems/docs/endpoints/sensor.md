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
