### User entity

```java
class UserProfile {

    private UUID id,

	private String name,

    private String password,

	private Wallet wallet,

	private List<Transaction> transactions
}
```

### Wallet

```java
class Wallet {

    private UUID id,

	private BigDecimal balance
}
```

### Transaction

```java
class Transaction: { // заявка за закупуване/продаване

	private UUID id,

	private string asset,

 	private BigDecimal buy, // да се види механизма

	private BigDecimal sell,

	private Currency currencyId
}
```

### Currency

```java
class Currency: {

	private int id,

    private String displayName
}
```