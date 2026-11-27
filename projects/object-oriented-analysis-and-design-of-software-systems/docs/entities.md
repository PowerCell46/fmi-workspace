### User entity

```java
class User {

    private UUID id;

	private String username;

    private String password;

	private Portfolio portfolio;
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

	private Gender gender;

	private String nationality; // or enum

	private LocalDate birthdate;

	private LocalDate validity;

	private BigInteger documentNumber;

	private String placeOfBirth;

	private String residence;

	private Integer height;

	private String colorOfEyes; // or enum

	private LocalDate dateOfIssue;

	private List<String> personalDocumentImageUrls; // 2 pictures - from the two sides of the document
}
```

---
## Gender
```java
enum Gender {

	MALE,

	FEMALE,

	OTHER
}
```

---
### Portfolio

```java
class Portfolio {

    private UUID id;

	private List<Transaction> transactions; // ! При транзакция, трябва да се инкрементира подходящия currencyAmount

	private List<CurrencyAmount> currencyAmounts;

	private Currency defaultCurrency; // EUR

	private List<Dividend> paidDividends; // ! При получаване на дивидент, трябва да се инкрементира подходящия currencyAmount

	public BigDecimal getTotalAmount() {
		return currencyAmounts
			.stream()
			.map(currencyAmount -> {
				// TODO: you get the currencyAmount.getAmount(), convert it to the defaultCurrency (by the current ratio) and return the value
			})
			.sum(); // not sure if we had such operation in Java
	}
}
```

---
### Transaction
Заявка за закупуване/продаване

```java
class Transaction {

	private UUID id;

	private Instant executedAt;

	private OperationType operationType;

	private Company company;

	private BigDecimal sharesAmount;

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
class Currency {

	private int id;

    private String name;
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

	private UUID id;

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
class Company { // TODO: rename to Instrument or Asset

	private String ticker;

	private Sector sector;

	private StockExchange stockExchange;

	// private String imageUrl;

	// private String name;

	// private String description;

	private BigInteger totalNumberOfShares; // TODO: If it's an index then do we have this field? It should probably be an optional field; in that case the entity should probable be renamed?

	private BigDecimal dividendYield;
}
```

---
## Sector

```java
enum Sector {

	ENERGY,

	MATERIALS,

	INDUSTRIALS,

	CONSUMER_DISCRETIONARY,

	CONSUMER_STAPLES,

	HEALTH_CARE,

	FINANCIALS,

	INFORMATION_TECHNOLOGY,

	COMMUNICATION_SERVICES,

	UTILITIES,

	REAL_ESTATE
}
```

---
## Stock Exchange

```java
class StockExchange {

	private String marketIdentifierCode;

	// private String name;

	// private String description;

	private Integer startWorkingHour; // for example 9 a.m.
	// TODO: Зимно и Лятно часово време имат значение, при зимно се пушват 1 час: 10 a.m. and 18:30 p.m.
	private Integer endWorkingHour; // for example 17:30 p.m.
	
	// TODO: also holidays should be considered
}
```

TODO: An entity in which we keep tickers that the system works with; active: boolean field; manages by the admin (кои тикери поддържа нашата система - трябва ни при web socket connection-а да ги подаваме)