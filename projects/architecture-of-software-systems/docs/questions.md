### Questions for the lecturer:

1. Роля AI Модул (виртуален асистент за анализ и предложения): Kakwo se има предвид под това да имаме user role за AI module?
- можем да го премахнем, ако успеем да се обосновем, защо сме сметнали така.

2. "Регистрирани граждани могат да подават сигнали за проблеми" -> това означава ли че само граждани могат да подават сигнали за проблеми
- трябва да се обосновем, защо сме взели такова решение на база спецификацията

3. Да се осигури публичен API за използване на данните от трети страни, даващи следната информация -> are the endpoints authenticated or not? Should unauthorized users be able to access them or not?
- това се базира на база на другите изисквания

4. Централизиран облачен сървър за обработка: Какво се има предвид под облачен сървър?
скалируемост като качествено изискване; high availability

5. За архивирането на базата, има се предвид, че местим стари записи, с цел освобождаване на главната база, или че имаме някакъв стейт, от който можем да се върнем назад във времето?
    - да не архивираме юзър данните?

*трябва да имаме анализ на изискванията*
качествени изисквания
функционални и нефункционални изисквания

6. GDPR related: 
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