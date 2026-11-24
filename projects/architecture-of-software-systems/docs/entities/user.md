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
 
    ADMINISTRATOR // admin
}
```
