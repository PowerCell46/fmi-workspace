### User entity

```java
class User {

    private UUID id;

	private String name;

    private String password;

	private Wallet wallet;
}
```

### Portfolio

```java
class Portfolio {

    private UUID id,

	private List<Transaction> transactions;

	private List<CurrencyAmount> currencyAmount;

	private Currency defaultCurrency; // EUR

	private List<Dividend> paidDividends; // ! При получаване на дивидент, трябва да се инкрементира подходящия currencyAmount

	// transient totalAmount
}
```

### Transaction

```java
class Transaction: { // заявка за закупуване/продаване

	private UUID id,

	private Instant at;

	private Comapny asset,

	private BigDecimal amount;

	private OperationType operationType;

	private Currency currencyId;

	private BigDecimal priceAt;
}
```

---
## OperationType

```java
enum OperationType {
	BUY,
	SELL
}
```

---

### Currency

```java
class Currency: {

	private int id,

    private String displayName
}
```

## CurrencyAmount
```java
class CurrencyAmount {

	private Portfolio portfolio;

	private Currency currency;
	
	private BigDecimal amount;
}
```

---
## Divident
```java
class Divident { // Occurrence

	private Portfolio portfolio;

	private Company company;

	private BigDecimal amountOfShared; // 2,14

	private Currency currency;

	private Instant paidAt;

	private BigDecimal paidAmount;
}
```

---
## Company 

```java
class Company {

	// TODO: Add the fields
}
