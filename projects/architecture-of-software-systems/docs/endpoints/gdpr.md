### Endpoint where we allow a user to delete their account
In the UI we should have some option where the user could delete his account. In order to do it, he/she has to click confirm at least once
+ write down the username exactly matching. If that's the case we make a request to this endpoint

DELETE request

the system hard deletes the user from the database, we should also make sure that their data is deleted from the archive/backup. All relational entities
should set their user_id to NULL.
IMPORTANT: **Erasure also means the data has to go from everywhere: DB, logs, search indexes, and backups on a retention schedule.**

---
### Endpoint where we allow a user to export their data
In the same place in the UI as the delete account, we should allow the option to the user to export their data in a structured way (JSON for example);
All user related data + related entity entries (FiledProblem).

GET request

---
### Endpoint for fetching the privacy notice
In order to comply with the GDPR rules we should have the following: **"a short page saying what you store, why, and for how long."**
This endpoint should be the source of that. If a change is made on how we store data, FE should be decoupled from the BA's structure. It could be a static
HTML or txt file we read & send out, update the file when we have to.

GET request
could be accessed without authentication/freely accessed

---
### Endpoint where a registered user files a report
подават сигнали за проблеми, които се включват в приоритизацията на обработка от операторите по поддръжка

POST request
```json
{
    latitude: "BigDecimal",
    longitude: "BigDecimal",
    filedAt: "Date",
    problemType: "Enum",
    image: "String" // TODO: We should discuss how the image is being sent
}

The server receives the request, validates the data, persist the image in the object storage and then persists the entry in the database
