---
title: "Uge 4 – Concurrency"
date: 2026-09-11
weight: 4
draft: false
summary: "Arbejde med tråde, samtidige requests og databaseforbindelser."
tags: ["Java", "Concurrency", "Javalin", "JPA"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge arbejdede jeg med concurrency i Java.

Jeg undersøgte blandt andet:

- `Runnable`
- `Callable`
- Threads
- Executors
- `CompletableFuture`

## Hvordan er concurrency relevant for projektet?

Javalin kan behandle flere HTTP-requests samtidig. Derfor skal databasekoden kunne fungere, selvom flere brugere anvender API'et på samme tid.

Projektet deler én `EntityManagerFactory`, men hver DAO-metode opretter sin egen `EntityManager`.

```text
EntityManagerFactory
→ opret EntityManager
→ udfør databaseoperation
→ luk EntityManager
```

En `EntityManager` bliver dermed ikke delt mellem forskellige requests.

## Skal projektet oprette egne threads?

Jeg valgte ikke at tilføje manuel multithreading til pakkelogikken.

Javalin håndterer allerede requests samtidigt, og kaldet til OpenRouteService er forholdsvis enkelt. Ekstra threads ville derfor gøre projektet sværere uden at løse et konkret problem.

## Hvad var svært?

Det var svært at skelne mellem:

- Concurrency i webserveren
- Egne Java-threads
- Databaseforbindelser
- Asynkrone API-kald

Jeg lærte, at concurrency skal bruges, når der er et konkret behov, og ikke kun for at tilføje flere teknologier.