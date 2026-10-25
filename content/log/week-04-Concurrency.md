---
title: "Uge 4 – Concurrency"
date: 2026-09-11
weight: 4
draft: false
summary: "Arbejde med samtidige forbindelser og live tracking."
tags: ["Java", "Concurrency", "WebSocket", "Javalin"]
---

[⌂ Til forsiden](/Portfolio/)

## Hvad arbejdede jeg med?

I denne uge arbejdede jeg med concurrency.

Concurrency betyder, at et program kan håndtere flere opgaver samtidig. Det er relevant i et API, fordi flere brugere kan sende requests på samme tid.

Jeg undersøgte også, hvordan WebSockets kan bruges til live tracking.

## Hvordan bruges WebSocket?

En klient kan oprette forbindelse til en bestemt pakke:

```text
ws://localhost:7070/api/parcels/{trackingNumber}/live
```

Når pakkens status ændres, kan serveren sende det nye delivery event direkte til klienten.

Klienten behøver derfor ikke hele tiden at spørge serveren efter nye oplysninger.

## Hvordan gemmes forbindelserne?

`TrackingSocket` gemmer forbindelser efter trackingnummer:

```text
Trackingnummer → WebSocket-forbindelser
```

Jeg bruger `ConcurrentHashMap`, fordi flere forbindelser kan blive tilføjet eller fjernet samtidig.

## Hvad var svært?

Det var vigtigt at forstå forskellen mellem:

- Java-koden på serveren
- JavaScript-koden i browseren
- Almindelige HTTP-requests
- En vedvarende WebSocket-forbindelse

Det var også vigtigt, at routes og services bruger den samme `TrackingSocket`.

## Hvad vil jeg arbejde videre med?

Jeg vil koble WebSocket-funktionen sammen med pakkens statusændringer.