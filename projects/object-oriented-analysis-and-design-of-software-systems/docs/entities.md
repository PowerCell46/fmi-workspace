### User entity

```java
class User {

    private UUID id;

	private String email;

	private String username;

    private String password;

	private Portfolio portfolio;
}
```

---
### Portfolio

```java
class Portfolio {

    private UUID id;

	private List<Transaction> transactions; // ! При транзакция, трябва да се инкрементира/декрементира подходящия currencyAmount

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

	private Asset asset;

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

	private Asset Asset;

	private BigDecimal numberOfShares; // 2.14

	private Currency currency;

	private BigDecimal paidAmount;
}
```

---
## Asset

```java
class Asset { 

	// An entity in which we keep the tickers with which the system works with; send through the webSocket

	private String ticker;

	private String imageUrl; // The admin has to upload an image for the asset, so it can be visualised in the frontend; easier than looking up online an image by the ticker
}
```

For the other (metadata) fields, we can fetch it, keeping it up to date with some kind of cron job that activates each 10 min, goes through all assets,
looks for diffs and updates if something needs updating

```python
import yfinance as yf

ticker = yf.Ticker("NVDA")
info = ticker.info

print(info.get("longName"))
print(info.get("longBusinessSummary"))
print(info.get("sharesOutstanding"))
print(info.get("marketCap"))
print(info.get("dividendYield"))
print(info.get("sector"))
print(info.get("industry"))
```
