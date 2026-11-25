### Filed problems

```java
class FiledProblem {

    private Instant filedAt; // It could be renamed

    private User user;

    private BigDecimal latitude;

    private BigDecimal longitude;    

    private FiledProblemType problemType;

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
