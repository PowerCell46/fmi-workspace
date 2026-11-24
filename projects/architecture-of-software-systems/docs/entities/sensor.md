
---
### Data sent from a IoT sensor

```java
class SensorReport {

    private Instant reportedAt;

    private Sensor sensor;

    private BigDecimal surfaceTemperature;

    private BigDecimal humidity;

    private BigDecimal slippernessDegree; // slippernessLevel
}
```

---
### Sensor

```java
class Sensor {

    private UUID id;

    private BigDecimal latitude;
    
    private BigDecimal longitude;

    private Integer reportAtSecond; // value from 0 to 29 indicating on which second the sensor should send its report; the name should be changed
}
```
