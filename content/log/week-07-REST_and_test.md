---
title: "Uge 7 – REST og test"
date: 2026-10-02
weight: 7
draft: false
summary: "Test, fejlhåndtering og logging i Package Delivery Tracker."
tags: ["REST", "Test", "HTTP", "Logging"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge arbejdede jeg med test og fejlhåndtering.

Jeg tilføjede:

- En central `ExceptionController`
- Ensartede JSON-fejlbeskeder
- Logging
- HTTP-requesteksempler
- Integrationstest

## Hvordan ser en fejl ud?

API'et sender fejl som JSON:

```json
{
  "status": 404,
  "message": "Parcel not found",
  "path": "/api/parcels/999"
}
```

Det gør fejlene lettere at forstå for klienten.

## Hvilke statuskoder bruger API'et?

- `200` når en request lykkes
- `201` når noget bliver oprettet
- `204` når noget bliver slettet
- `400` ved ugyldige data
- `404` når noget ikke findes
- `409` ved en ugyldig statusændring
- `500` ved en intern serverfejl
- `502` ved fejl fra OpenRouteService

## Hvordan tester jeg API'et?

Jeg bruger en `.http`-fil til at teste endpoints direkte fra IntelliJ.

Jeg har også forberedt integrationstest med JUnit og Testcontainers. Testcontainers kan starte en midlertidig PostgreSQL-database i Docker.

## Hvad var svært?

Det var vigtigt at forstå forskellen mellem enhedstest og integrationstest.

En integrationstest undersøger flere dele samlet, eksempelvis API, service, DAO og database.