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
- `ParcelRoutes`
- `ParcelController`
- Request- og response-DTO'er
- Javalin-konfiguration

## Hvilke endpoints har API'et?

```text
POST   /api/parcels
GET    /api/parcels
GET    /api/parcels/tracking/{trackingNumber}
GET    /api/parcels/{id}/events
POST   /api/parcels/{id}/events
DELETE /api/parcels/{id}
```

Der findes også et health endpoint:

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

Controlleren læser requesten. Servicen kontrollerer reglerne. DAO'en kommunikerer med databasen.

## Hvordan bruges Jackson?

Jackson oversætter JSON til Java-objekter:

```java
CreateParcelDTO request =
        ctx.bodyAsClass(CreateParcelDTO.class);
```

Jackson bruges også til at sende Java-objekter tilbage som JSON.

## Hvad var svært?

Det var vigtigt at holde controlleren enkel.

Forretningsregler skal ikke ligge i controlleren. De skal ligge i servicen, så de er lettere at teste og genbruge.