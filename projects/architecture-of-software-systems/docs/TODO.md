
### Homework questions:

- What type of database should we use for the application?
    TimescaleDB or Clickhouse; PostGIS

---
- Платформата трябва да поддържа автоматично архивиране на данните на всеки 6 часа: How should this be implemented? - sending docker volumes every 6 hours? Or something else?
    Dump the DB is a better approach
    ```terminal
    docker exec my-db pg_dump -U myuser -Fc mydb > /backups/mydb_$(date +%F_%H%M).dump
    ```
    automation: put the commands in a script; schedule with a cron job; compress, send to the target location; add retention (delete dumps older than 14 days); log failures and alert on them
    ---
    Archive: object storage + Parquet file format

---
- Данните трябва да се съхраняват и обработват съгласно GDPR и свързаните наредби: what does it consits of? На какви периоди се трият данните на потребителите?
    General data regulation protection
    personal data: any data that can identify you: name, phone number, username, ip address, location, sexual orientatiom, health data, political opinions
    - Maybe that means that we should have an endpoint where a user can delete his account (we need to think what happens to other entities referencing the user)

---
GDPR related: 
    Retention: don't keep logs and inactive accounts forever.

    use HTTPS

    removing the user related data from logs (for example when creating a FiledProblem, don't log the username; only log username on register, don't log it on login and logout, because it will create problems when we have to delete the logs)
    
    if you use third-party hosting or email, check that they have a DPA (Data Processing Agreement)
    
    put an email in the privacy notice where users can send requests.

    Endpoint related:
        Decide and note why you process the data. 
            For a login system it's usually "contract" (providing the service). 
            If you add anything optional (analytics, marketing emails), that needs consent.
        know who decides and how you'd notify users and the authority (72 hours) if something leaks. A few lines in a doc is enough.
        keep a short note of what data you store, where, and why. It also makes the privacy notice easy to write.

Може архивната ни база да е DataWarehouse (различна от работещата), което ще е доста подходящо за аналитичната функционалност 
    (трябва да се види дали може да се трие от нея и да се правят промени за GDPR related stuff)
