
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
- Преглеждане и избиране на тема по Обектно ориентиран анализ и моделиране
    Virtual Stock Market
