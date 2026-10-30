---
title: "Uge 6 – REST API med Javalin"
date: 2026-09-25
weight: 6
draft: false
summary: "Implementering af routes, controllers og REST-endpoints."
tags: ["REST", "Javalin", "HTTP", "Jackson"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge gjorde jeg projektets funktioner tilgængelige gennem et REST API.

Jeg oprettede:

- `Routes`
- `AuthRoutes`
- `ParcelRoutes`
- `AuthController`
- `ParcelController`
- Request- og response-DTO'er
- Javalin-konfiguration

## Hvilke endpoints har API'et?

```text
POST   /api/auth/register
POST   /api/auth/login

POST   /api/parcels
GET    /api/parcels
GET    /api/parcels/tracking/{trackingNumber}
GET    /api/parcels/{id}/events
POST   /api/parcels/{id}/events
DELETE /api/parcels/{id}
```

API'et har også et simpelt status-endpoint:

```text
GET /api/health
```

## Hvordan behandles en request?

En request bevæger sig gennem projektet sådan:

```text
Request
→ Route
→ Controller
→ Service
→ DAO
→ Database
```

Routes forbinder URL'er med controller-metoder. Controlleren læser requesten, servicen kontrollerer reglerne, og DAO'en kommunikerer med databasen.

## Hvordan bruges Jackson?

Javalin og Jackson oversætter JSON til Java-objekter:

```java
CreateParcelDTO request =
        ctx.bodyAsClass(CreateParcelDTO.class);
```

Jackson bruges også til at sende DTO'er tilbage til klienten som JSON.

## Hvad var svært?

Det var vigtigt at holde controllerne enkle.

Forretningsreglerne ligger derfor i serviceklasserne i stedet for controllerne. Det gør ansvarsfordelingen tydeligere og reglerne lettere at teste.