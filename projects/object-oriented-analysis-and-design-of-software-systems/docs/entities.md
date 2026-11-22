### User entity

```java
class User {

    private UUID id;

	private String username;

    private String password;

	private Wallet wallet;
}
```

---
### User details
everything should be hashed - personal data (extracted from the pictures made of the personal document)

```java
class UserDetails {

	private String firstName;

	private String middleName;

	private String lastName;

	private String socialSecurityNumber;

	private String gender; // or boolean or enum

	private String nationality; // or enum

	private LocalDate birthdate;

	private LocalDate validity;

	private BigInteger documentNumber;

	private String placeOfBirth;

	private String residence;

	private Integer height;

	private String colorOfEyes; // or enum

	private LocalDate dateOfIssue;

	// private List<String> imageUrls; // taken images of the document
}
```

---
### Portfolio

```java
class Portfolio {

    private UUID id;

	private List<Transaction> transactions; // ! При транзакция, трябва да се инкрементира подходящия currentyAmount

	private List<CurrencyAmount> currencyAmounts;

	private Currency defaultCurrency; // EUR

	private List<Dividend> paidDividends; // ! При получаване на дивидент, трябва да се инкрементира подходящия currencyAmount

	// transient totalAmount: calculated by iterating through all currencyAmounts + converted to defaultCurrency
}
```

---
### Transaction

```java
class Transaction: { // заявка за закупуване/продаване

	private UUID id;

	private Instant timestamp; // TODO: Should be renamed

	private OperationType operationType;

	private Company company;

	private BigDecimal amount;

	private Currency currency;

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

	private int id;

    private String displayName;
}
```

---
## CurrencyAmount

```java
class CurrencyAmount {

	private Portfolio portfolio;

	private Currency currency;
	
	private BigDecimal amount;
}
```

---
## Dividend

```java
class Dividend { // Occurrence of a dividend

	private Instant paidAt;

	private Portfolio portfolio;

	private Company company;

	private BigDecimal numberOfShares; // 2.14

	private Currency currency;

	private BigDecimal paidAmount;
}
```

---
## Company 

```java
class Company {

	private String ticker;

	// private String imageUrl;

	// private String name;

	// private String description;

	private BigInteger totalNumberOfShares;

	private BigDecimal dividendYield;
}
