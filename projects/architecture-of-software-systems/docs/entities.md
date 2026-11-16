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
 
    SUPPORT_OPERATOR, // (служител или външен партньор, отговарящ за инфраструктурата)
 
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

    private Integer reportAtSecond; // value from 0 to 29 indicating on which second the sensor should send its report; the name should be changed
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

    private FiledProblemType | String problemType; // TODO: We should discuss if it should be enum or free text, maybe a dropdown of enums is the best option

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

---
### FiledProblemType enumeration

```java
enum FiledProblemType {

    SURFACE_DAMAGE,

    SLIPPERY_SURFACE,

    FLOODED_SURFACE,

    OBSTRUCTION,

    DRAINAGE_ISSUE,

    DAMAGED_INFRASTRUCTURE,

    ACCESSIBILITY,

    OTHER
}
```