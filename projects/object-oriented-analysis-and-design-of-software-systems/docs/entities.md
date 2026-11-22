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

	private List<Transaction> transactions; // ! При транзакция, трябва да се инкрементира подходящия currentyAmount

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

```java
class Transaction { // заявка за закупуване/продаване

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
class Currency {

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

	private String industry; // could be an enum as well

	// private String imageUrl;

	// private String name;

	// private String description;

	private BigInteger totalNumberOfShares;

	private BigDecimal dividendYield;
}
```

---
## TranslationField

```java
class TranslationField {

	private Language language;

	private String tableName;

	private String fieldName;

	private String value;
}

// | EN | Company | name        | Meta                                                             |
// | EN | Company | description | Meta Platforms, Inc., headquartered in Menlo Park, California... |
// | BG | Company | name        | Meta                                                             |
// | BG | Company | description | Meta Platforms, Inc., със седалище в Менло Парк, Калифорния...   |

```

---
## Language

```java
class Language {

	private String name;
}
```
