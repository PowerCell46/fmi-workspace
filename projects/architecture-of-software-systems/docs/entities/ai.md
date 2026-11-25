### AI assesment
Wrap-ваме FiledProblem и му добавяме приоритет, резултат от Priorization assesment service-a.

```java
class FiledProblemAssesment {

    private UUID id;

    private FiledProblem incident; // whole reference to FiledProblem or only id?

    private Priority priority;

    private Instant assessedAt;
    // TODO: could add reasoning fields like confidence and score
}
```

---
### AI priority status

```java
enum Priority  {

    LOW,

    MEDIUM,

    HIGH,

    CRITICAL
}
```
