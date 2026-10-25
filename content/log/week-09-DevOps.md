---
title: "Uge 9 – DevOps"
date: 2026-10-23
weight: 9
draft: false
summary: "Klargøring af Package Delivery Tracker til deployment."
tags: ["DevOps", "Deployment", "Docker", "PostgreSQL"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge arbejdede jeg med at gøre projektet klar til deployment.

Applikationen bruger PostgreSQL og OpenRouteService. Databaseoplysninger og API-nøgler må derfor ikke stå direkte i Java-koden.

## Miljøvariabler

Projektet kan bruge miljøvariabler som:

```text
DB_NAME
DB_USERNAME
DB_PASSWORD
CONNECTION_STR
OPENROUTESERVICE_API_KEY
HIBERNATE_DDL_AUTO
```

Lokalt kan projektet bruge `config.properties`. Ved deployment skal oplysningerne komme fra hosting-platformen.

## Build med Maven

Maven bruges til at kompilere projektet og køre testene:

```bash
mvn clean test
mvn package
```

Projektet skal kunne bygges uden fejl, før det bliver deployed.

## Docker

Docker kan bruges til at pakke Java-applikationen i en container.

Det giver et ensartet miljø lokalt og på serveren.

Java-applikationen og PostgreSQL bør køre som separate services.

## Logging og health check

Logging bruges til at registrere fejl og vigtige hændelser.

API'et har også et health endpoint:

```http
GET /api/health
```

Det kan bruges til at kontrollere, om serveren kører.

## Hvad var svært?

Det var svært at forstå forskellen mellem:

- At bygge applikationen
- At oprette en container
- At deploye applikationen
- At forbinde til en produktionsdatabase

## Hvad vil jeg arbejde videre med?

Jeg vil senere arbejde med:

- GitHub Actions
- Docker
- Automatisk test
- Deployment
- En ekstern PostgreSQL-database
- Sikre miljøvariabler