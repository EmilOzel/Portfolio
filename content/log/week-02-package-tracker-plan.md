---
title: "Uge 2 – Planlægning af Package Delivery Tracker API"
date: 2026-08-26
weight: 2
draft: false
summary: "Valg af applikationsidé og planlægning af API, datamodel, sikkerhed og de første udviklingstrin."
tags: ["Planlægning", "REST API", "Java", "PostgreSQL"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad tilføjede jeg i denne uge?

Jeg valgte at bygge et Package Delivery Tracker API. Formålet med applikationen er, at brugere kan oprette pakker, følge dem med et trackingnummer og se hvert trin i leveringsprocessen.

Jeg planlagde også den første version af domænemodellen, API-endpoints, brugerroller og forretningsregler, før implementeringen begynder.

## Hvilke nye teknologier vil jeg bruge?

Backenden skal bygges med Java og et REST API-framework. Jeg planlægger at bruge PostgreSQL til vedvarende data, Hibernate/JPA til databasemapping og senere tilføje autentificering med rollebaseret adgangskontrol.

## Hvorfor strukturerede jeg det sådan?

Jeg vil opdele applikationen i controllere, services, repositories, entities, DTO'er og sikkerhedskonfiguration. Controllere håndterer HTTP-requests, services indeholder forretningsreglerne, og repositories kommunikerer med databasen. Det gør API'et lettere at teste og udvide.

De centrale entities bliver:

- `User` – kontooplysninger og en rolle som `USER`, `EMPLOYEE` eller `ADMIN`.
- `Package` – trackingnummer, afsender, modtager, adresse, nuværende status og oprettelsesdato.
- `DeliveryEvent` – en tidsstemplet opdatering med status, lokation og en besked.

Hver pakke kan have mange delivery events, men hvert delivery event tilhører én pakke. Pakken gemmer den nuværende status, så den hurtigt kan findes, mens events gemmer hele leveringshistorikken.

## Planlagte API-endpoints

```text
POST   /api/auth/register
POST   /api/auth/login

POST   /api/packages
GET    /api/packages
GET    /api/packages/{trackingNumber}

POST   /api/packages/{id}/events
GET    /api/packages/{id}/events
PUT    /api/packages/{id}/status
```

## Planlagte forretningsregler

- Trackingnumre skal være unikke.
- En bruger må kun se pakker, som brugeren ejer.
- Kun medarbejdere og administratorer må tilføje delivery events eller ændre en pakkes status.
- En pakke, der er leveret, må ikke ændres tilbage til en tidligere leveringsstatus.
- Hver statusændring skal oprette et delivery event, så pakkens historik forbliver komplet.

## Hvad fungerede godt?

At vælge en mindre applikationsidé gjorde det lettere at identificere tydelige entities og forretningsregler. Projektet understøtter CRUD-operationer fra starten, men giver stadig plads til autentificering, validering, test og mere avancerede funktioner senere.

## Hvad var svært eller forvirrende?

Det sværeste var at afgøre, hvilken information der skal ligge på `Package`, og hvilken der skal ligge i `DeliveryEvent`. Jeg valgte at gemme den nuværende status på pakken og alle tidligere ændringer som events, fordi API'et både skal kunne finde den aktuelle status hurtigt og have en pålidelig historik.

## Hvad vil jeg forbedre næste gang?

Før jeg implementerer endpoints, vil jeg lave et simpelt entity-relationship-diagram og skrive eksempler på request- og response-bodies. Det bør gøre databaserelationer og API-validering tydeligere, før kodningen begynder.
