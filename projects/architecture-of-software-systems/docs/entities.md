### User entity

```java
class User {

    private String username;

    private String password;

    private Role role;
}
```

----
### Role enumeration

```java
enum Role {

    CITIZEN, // (registered user)
 
    SUPPORT_OPERATOR,
 
    DATA_ANALYZER,
 
    ADMINISTRATOR, // admin
 
    //! AI_MODULE (виртуален асистент за анализ и предложения)????
}
```

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

    private Integer reportAtSecond; // value from 0 to 59 indicating on which second the sensor should send its report
}
```

---
### Filed problems

```java
class FiledProblem {

    private Instant filedAt; // It could be renamed

    private User user;

    private BigDecimal latitude;

    private BigDecimal longitude;    

    private FiledProblemType | String problemType; // TODO: We should discuss if it should be enum or free text

    private String imageUrl; // The idea is that the image is stored in an object storage, we don't persist it on the file system or in the database

    private FiledProblemStatus status;
}
```

---
### FiledProblemStatus enumeration

```java
enum FiledProblemStatus {

    PERSISTED, // The entry was successfully persisted when the user submitted it

    // TODO: Think of the statuses
}
```