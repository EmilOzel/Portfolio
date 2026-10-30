---
title: "Uge 9 – DevOps og deployment"
date: 2026-10-23
weight: 9
draft: false
summary: "Docker, GitHub Actions og deployment af Package Delivery Tracker."
tags: ["DevOps", "Docker", "GitHub Actions", "DigitalOcean"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge gjorde jeg projektet klar til deployment og fik API'et udgivet.

Jeg arbejdede med:

- Miljøvariabler
- Maven-build
- Docker
- Docker Compose
- Docker Hub
- GitHub Actions
- DigitalOcean
- Caddy og HTTPS

## Miljøvariabler

Databaseoplysninger, API-nøgler og JWT-hemmeligheden må ikke ligge direkte i Java-koden.

Projektet bruger blandt andet:

```text
PORT
DB_NAME
DB_USERNAME
DB_PASSWORD
CONNECTION_STR
OPENROUTESERVICE_API_KEY
JWT_SECRET
HIBERNATE_DDL_AUTO
```

Lokalt kan projektet læse fra `config.properties`. I Docker og på serveren bruges miljøvariabler.

## Docker

Projektets `Dockerfile` bruger et multi-stage build.

Første trin bygger applikationen med Maven og Java 25. Andet trin opretter et mindre image, som kun indeholder Java runtime og den færdige JAR-fil.

Docker Compose kan starte:

- Package Delivery Tracker API
- PostgreSQL

API'et og databasen kører som separate containers.

## GitHub Actions

Når der pushes til `main`, udfører GitHub Actions følgende:

1. Henter projektet.
2. Installerer Java 25.
3. Kører `mvn clean verify`.
4. Bygger et Docker-image, hvis testene består.
5. Sender imaget til Docker Hub.

Pull requests til `main` kører testjobbet, men udgiver ikke et nyt Docker-image.

## Deployment

API'et er deployet på en DigitalOcean Droplet.

På serveren kører:

- Java-API'et i en Docker-container
- PostgreSQL i en separat container
- Caddy som reverse proxy

Caddy forbinder domænet med API-containeren og håndterer HTTPS.

API'et kan tilgås på:

```text
https://api.ozeldemo.dk/api/
```

Deployment på serveren opdateres manuelt fra Docker Hub. Projektet bruger ikke Watchtower.

## Health checks

API'et har et simpelt endpoint:

```http
GET /api/health
```

Den lokale Docker Compose-konfiguration har desuden et health check til PostgreSQL. Der er ikke konfigureret et automatisk health check til API-containeren.

## Hvad var svært?

Det var svært at forstå forskellen mellem:

- Maven-buildet
- Docker-imaget
- Docker Hub
- Containerne på serveren
- Domænet og Caddy
- PostgreSQL lokalt og i produktion

Jeg lærte, at deployment består af flere separate trin, som tilsammen gør API'et tilgængeligt over HTTPS.