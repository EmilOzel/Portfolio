---
title: "Uge 7 – REST og test"
date: 2026-10-02
weight: 7
draft: false
summary: "Test, fejlhåndtering og logging i Package Delivery Tracker."
tags: ["REST", "Test", "JUnit", "Testcontainers"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge arbejdede jeg med test og fejlhåndtering.

Jeg tilføjede:

- En central `ExceptionController`
- Ensartede JSON-fejlbeskeder
- Logging
- HTTP-requesteksempler
- DAO-tests
- REST-integrationstests
- Tests af password- og JWT-funktionalitet

## Hvordan ser en fejl ud?

API'et sender fejl som JSON:

```json
{
  "status": 404,
  "message": "Parcel not found",
  "path": "/api/parcels/999"
}
```

Det giver klienten et ensartet format, uanset hvor fejlen opstår.

## Hvilke statuskoder bruger API'et?

- `200` når en request lykkes
- `201` når noget bliver oprettet
- `204` når noget bliver slettet
- `400` ved ugyldige data
- `401` når authentication mangler eller fejler
- `403` når brugeren mangler den nødvendige rolle
- `404` når noget ikke findes
- `409` ved en ugyldig statusændring
- `500` ved en intern serverfejl
- `502` ved fejl fra OpenRouteService

## Hvordan tester jeg API'et?

Jeg bruger en `.http`-fil til at sende requests direkte fra IntelliJ.

De automatiske tests bruger:

- JUnit
- REST Assured
- Testcontainers
- PostgreSQL

Testcontainers starter en midlertidig PostgreSQL-database i Docker. Det betyder, at testene ikke ændrer data i min normale database.

## Hvad var svært?

Det var vigtigt at forstå forskellen mellem en DAO-test og en REST-test.

En DAO-test undersøger databaseadgangen. En REST-test undersøger hele flowet gennem routes, controller, service, DAO og database.