- Currency interest

- integrated AI portfolio analyzer

- проверка, че клиентът не е част от блеклисти (издирван от ГДБОП, ЕС например)

- no autoinvesting

- no pots

- no commodities

- multilanguage of the system
Here's a snippet taken from the entities.md of how it should be implemented

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
